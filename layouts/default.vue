<template>
    <div class="ml-4">
       <div>
          <Header />
          <nav class="text-l font-light font-thin flex space-x-40 pt-4 align-middle justify-center ">
             <NuxtLink to="/" class="hover:text-blue-500 ">Beranda</NuxtLink>
             <NuxtLink :to="{ name: 'jadwal_shalat' }" class="hover:text-blue-500 ">Jawal Shalat</NuxtLink>
             <NuxtLink :to="{ name: 'reciter_sound' }" class="hover:text-blue-500 ">Mp3 </NuxtLink>
             <div class="dropdown">
                <button class="dropdown-toggle px-2 box-border">sdffs</button>
             </div>
          </nav>
       </div>
       <slot></slot>
    </div>
 </template>
 
 <script lang="ts" setup>
 </script>
 