<template>
  <div class="min-h-screen w-screen bg-black text-gray-200 font-sans">
     <NuxtLayout>
        <NuxtLoadingIndicator />
        <v-app class="bg-transparent">
           <div>
              <NuxtPage />
           </div>

        </v-app>
     </NuxtLayout>
  </div>
</template>
