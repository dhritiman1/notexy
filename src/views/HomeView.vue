<template>
  <div class="min-h-screen flex justify-center items-center overflow-hidden">
    <div
      class="min-h-[calc(100vh-30px)] w-[calc(100vw-30px)]"
      @click="
        showform = true;
        setCoord($event);
      "
    >
      <input
        v-if="showform"
        v-model="text"
        type="text"
        @keydown="submit($event)"
        :style="{ top: y + 'px', left: x + 'px' }"
        :class="'absolute bg-transparent focus:outline-none focus:border-b px-1'"
        autofocus
      />
      <div
        v-for="note in notes"
        :key="note.x + '-' + note.y"
        :style="{ top: note.y + 'px', left: note.x + 'px' }"
        class="absolute w-[12rem] p-1"
      >
        <div>{{ note.text }}</div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { Ref, ref } from "vue";

type Note = {
  text: string;
  x: number;
  y: number;
};

let showform = ref(false);
let x: Ref<number> = ref(0);
let y: Ref<number> = ref(0);
let text = ref("");
let notes: Ref<Note[]> = ref([]);

const setCoord = (e: MouseEvent) => {
  const { clientX, clientY } = e as PointerEvent;
  x.value = clientX;
  y.value = clientY;
  console.log(x.value, y.value);
  text.value = "";
};

function submit(event: KeyboardEvent) {
  if (event.key === "Enter") {
    console.log("submit");

    notes.value.push({ text: text.value, x: x.value, y: y.value });

    showform.value = false;
    text.value = "";
  }
}
</script>
