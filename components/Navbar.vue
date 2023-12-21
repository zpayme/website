<template>
  <div class="bg-black">
    <div class="m-auto max-w-6xl">
      <div class="flex items-center justify-between h-10 py-12 px-4 uppercase md:text-lg font-bold text-white">
        <NuxtLink to="/" class="text-3xl flex flex-row items-center">
          <img src="/logo.png" class="h-16" />
        </NuxtLink>
        <div class="flex items-center space-x-4">
          <div class="flex items-center space-x-2 md:space-x-4 text-sm md:text-lg">
            <NuxtLink to="/faq">FAQs</NuxtLink>
            <NuxtLink to="/about">About</NuxtLink>
            <NuxtLink to="/contact">Contact</NuxtLink>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
