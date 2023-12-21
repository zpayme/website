<template>
  <section class="max-w-7xl m-auto my-8 md:my-40">
    <div class="flex flex-wrap">
      <div class="w-full md:w-1/2 p-8">
        <h1 class="mb-10 text-3xl md:text-7xl font-extrabold">
          Discover streamlining recurring payments on the blockchain.
        </h1>
        <p class="mb-16 text-lg text-gray-900">
          Experience unparalleled security, transparency, and efficiency in
          collecting payments. Join the future of finance with ZPAY's innovative
          solution.
        </p>
        <div class="flex flex-wrap -m-2.5 mb-20">
          <div class="w-full md:w-auto p-2.5">
            <div class="flex justify-center items-center">
              <NuxtLink
                to="/create"
                class="py-4 px-6 text-center w-full text-white font-semibold border border-indigo-700 rounded-xl focus:ring focus:ring-indigo-300 bg-indigo-600 hover:bg-indigo-700 transition ease-in-out duration-200"
                type="button"
              >
                Create Subscription
              </NuxtLink>
            </div>
          </div>
          <div class="w-full md:w-auto p-2.5">
            <a target="_blank" href="https://www.npmjs.com/package/zpayme">
              <button
                class="py-4 px-9 w-full font-semibold border border-gray-300 hover:border-gray-400 rounded-xl focus:ring focus:ring-gray-50 bg-transparent hover:bg-gray-100 transition ease-in-out duration-200"
                type="button"
              >
                <div class="flex flex-wrap justify-center items-center">
                  <div class="w-auto"></div>
                </div></button
            ></a>
          </div>
        </div>
      </div>
      <div class="w-full md:w-1/2 p-0 md:p-8 hidden md:block">
        <img
          class="transform hover:-translate-y-2 transition duration-500"
          src="/tokens.png"
          alt=""
        />
      </div>
    </div>
  </section>
</template>
