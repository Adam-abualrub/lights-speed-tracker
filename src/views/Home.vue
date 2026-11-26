<script setup>
</script>

<template>
  <main class="flex flex-col gap-4 bg-gray-100 text-black max-w-[420px] mx-auto p-4 rounded-3xl">
    <h1 class="m-0 text-3xl font-bold">Remaining</h1>
    <p class="m-0 text-[#8c8c8c]">This week · ends in 4 days</p>

    <section class="bg-white flex flex-col p-4 rounded-2xl">
      <h2 class="text-3xl text-green-600 m-0">Rp 325.000</h2>
      <p class="m-0 text-[#8c8c8c]">of Rp 500.000 · 3 spent</p>
    </section>

    <h2 class="m-0 text-[#8c8c8c] text-[0.9rem] font-bold">QUICK LOG</h2>

    <section class="bg-white flex flex-col gap-3 p-4 rounded-2xl">
      <input 
        class="bg-gray-200 border-none rounded-xl p-3 focus:outline-none" 
        type="text" 
        placeholder="Title · e.g. Nasi goreng" 
      />
      
      <div class="flex gap-2">
        <button 
          class=" bg-green-600 border-none rounded-full py-2 px-4 bg-[#3e6b5e] text-white cursor-pointer" 
          type="button"
        >
          Food
        </button>
        <button 
          class="  border-none rounded-full py-2 px-4 bg-[#ebebe8] cursor-pointer" 
          type="button"
        >
          Housing
        </button>
        <button 
          class="border-none rounded-full py-2 px-4 bg-[#ebebe8] cursor-pointer" 
          type="button"
        >
          Health
        </button>
      </div>

      <div class=" bg-gray-200 flex gap-3">
        <input 
          class="bg-gray-200 border-none rounded-xl p-3 w-1/2 focus:outline-none" 
          type="text" 
          placeholder="25.000" 
        />
        <button 
          class=" bg-green-600  border-none rounded-xl bg-[#3e6b5e] text-white w-1/2 cursor-pointer" 
          type="button"
        >
          Save
        </button>
      </div>
    </section>
<div class=""><h2 class="text-base m-auto  font-normal flex self-start text-[0.9rem] font-bold ">RECENT</h2></div>

    <section class="flex flex-col gap-3">
      <div class="bg-white p-3 rounded-lg flex justify-between">
        <p class="m-0">Nasi goreng · Food</p>
        <span>25.000</span>
      </div>
      <div class="bg-white p-3 rounded-lg flex justify-between">
        <p class="m-0">Bus fare · Transport</p>
        <span>15.000</span>
      </div>
    </section>
  </main>
</template>