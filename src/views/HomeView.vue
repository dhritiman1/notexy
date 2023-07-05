<template>
  <div class="min-h-screen flex justify-center items-center overflow-hidden">
    <textarea
      v-if="showform"
      v-model="text"
      type="text"
      @keydown="submit($event)"
      :style="{ top: y + 'px', left: x + 'px' }"
      :class="'absolute bg-transparent focus:outline-none focus:border-b border-gray-400 px-1 resize-none scrollbar scrollbar-w-1 scrollbar-track-rounded-md scrollbar-track-transparent scrollbar-thumb-zinc-700'"
      autofocus
    />
    <textarea
      v-if="showUpdateForm"
      type="text"
      v-model="text"
      @keydown="update($event)"
      :style="{ top: y + 'px', left: x + 'px' }"
      :class="'absolute bg-transparent focus:outline-none border-b border-gray-400 px-1 resize-none scrollbar scrollbar-w-1 scrollbar-track-rounded-md scrollbar-track-transparent scrollbar-thumb-zinc-700'"
      autofocus
    />
    <div
      class="min-h-[calc(100vh-30px)] w-[calc(100vw-30px)]"
      @click="
        showform = true;
        setCoord($event);
      "
    />
    <div
      v-for="note in notes"
      :key="note.x + '-' + note.y"
      :style="{ top: note.y + 'px', left: note.x + 'px' }"
      class="absolute w-[12rem] p-1 cursor-pointer"
    >
      <p
        v-if="note.disp"
        @click="triggerUpdate(note.x, note.y, note.text, notes.indexOf(note))"
      >
        {{ note.text }}
      </p>
    </div>
  </div>
</template>

<script setup lang="ts">
import { Ref, ref } from "vue";

type Note = {
  text: string;
  x: number;
  y: number;
  disp: boolean;
};

//form display control
let showform = ref(false);
let showUpdateForm = ref(false);

// position
let x: Ref<number> = ref(0);
let y: Ref<number> = ref(0);

let text = ref("");
let notes: Ref<Note[]> = ref([]);

// index
let toUpdateNote = ref(-1);

const setCoord = (e: MouseEvent) => {
  const { clientX, clientY } = e as PointerEvent;
  x.value = clientX;
  y.value = clientY;
  console.log(x.value, y.value);
  text.value = "";
};

const submit = (event: KeyboardEvent) => {
  if (event.key === "Enter") {
    notes.value.push({ text: text.value, x: x.value, y: y.value, disp: true });

    showform.value = false;
    text.value = "";
  }
};

const update = (event: KeyboardEvent) => {
  notes.value[toUpdateNote.value].text = text.value;
  if (event.key === "Enter") {
    notes.value[toUpdateNote.value].disp = true;

    showUpdateForm.value = false;
    text.value = "";
    toUpdateNote.value = -1;
  }
};

const triggerUpdate = (
  posX: number,
  posY: number,
  txt: string,
  index: number
) => {
  showUpdateForm.value = true;
  notes.value[index].disp = false;

  text.value = txt;
  x.value = posX;
  y.value = posY;
  toUpdateNote.value = index;
};
</script>
