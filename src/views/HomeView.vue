<template>
  <div class="w-full min-h-screen flex justify-center items-center select-none">
    <div
      class="w-full md:w-[38rem] px-9 mb-24 flex flex-col gap-4 text-lg font-normal text-justify"
    >
      <p class="text-4xl font-light">notexy</p>
      <p class="text-zinc-400">
        make notes at any random place in the screen. have fun with the layout
        and make minimal short notes as per your needs.
      </p>
      <div>
        <p>how to use notexy:</p>
        <ul class="pl-7 text-zinc-400 list-disc">
          <li>tap any where you want</li>
          <li>write the note</li>
          <li>press enter</li>
        </ul>
      </div>
      <div>
        <p>you can also update the notes you make</p>
        <p>to do so:</p>
        <ul class="pl-7 text-zinc-400 list-disc">
          <li>click on the notes</li>
          <li>make the changes</li>
          <li>press enter</li>
        </ul>
      </div>
      <router-link
        to="/note"
        class="font-normal text-lg hover:text-white ease-in duration-300"
        ><p>start writing →</p></router-link
      >
    </div>
  </div>
</template>
