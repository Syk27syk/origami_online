<template>
  <div>
    <header class="grid grid-cols-2 bg-black text-white font-bold">
      <div id="logo" class="flex flex-row">
        <img src="/logo.png" class="h-20 w-20 m-5" alt="" />
        <p class="text-3xl font-bold my-auto">Origami Online</p>
      </div>
      <div id="navigation" class="grid grid-cols-4 my-auto text-2xl font-bold">
        <span>nav item 1</span>
        <span>nav item 2</span>
        <span>nav item 3</span>
        <span>nav item 4</span>
      </div>
    </header>
    <div class="flex h-screen h-[100vh] bg-[url('/hero-bg.jpg')] bg-cover bg-center align-middle text-white text-center">
      <div class="m-auto p-60 bg-black bg-opacity-30 rounded-full">
        <h1 class="text-5xl">Origami Online</h1>
        <p class="mt-5 text-3xl font-bold">fold origami virtually</p>
      </div>
    </div>
    <footer class="bg-black text-white m-auto text-center">
      <p class="py-5 text-2xl font-bold">Made in Malaysia 2022</p>
    </footer>
  </div>
</template>
