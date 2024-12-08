<script lang="ts" setup>
import { navigateTo } from 'nuxt/app';

let surah = ref<string>('');
// let edisi=ref<string>('');
let response_Quran = ref<any>(null)

const quran = await $fetch('https://equran.id/api/v2/surat');
// let quran = await $fetch('https://equran.id/api/v2/surat');https://equran.id/apidev/v2

let ListSurats = []
let namaLa = []
for (let index = 0; index < quran.data.length; index++) {
   const item = quran.data[index];
   namaLa.push((index + 1) + '. ' + item.namaLatin)
   ListSurats.push(item)

}
const fetch_Quran = async () => {
   let res = 0
   if (!surah.value) {
      res = 0;
   } else {
      res = namaLa.indexOf(surah.value)
   }
   await navigateTo({
    path: '/detail_surat', 
    query: { nomerSurah: (res+1) }
  });
}

const detailSurah=async (nomerSurah: any)=> {
   console.log(nomerSurah)
   // this.$router.push({ name: 'detail_surat', params: { nomerSurah } });
   await navigateTo({
    path: '/detail_surat', 
    query: { nomerSurah: nomerSurah }
  });

}
</script>

<template>
   <div class="flex align-middle justify-center justify-items-center">
      <div class="pt-4">
         <div class="max-w-screen-2xl mx-auto">
            <v-card class=" md:w-96 w-full">
               <v-img class=" h-auto object-cover w-96"  aspect-ratio="4/3"
                        src="/public/img/quran-islam.jpeg">
                     </v-img>
            </v-card>
         </div>
      </div>
   </div>
   <div class="pl-4 pt-5 flex align-middle">
      <label class="mr-6">Tampilkan : </label>
      <v-select v-model="surah" label="Surah" :items="namaLa" item-text="namaLatin" item-value="id" variant="underlined"
         class="max-w-32"> </v-select>
      <!-- <v-select v-model="edisi" label="Edisi" :items="['M Asad', 'Ustmani']" variant="underlined" class="max-w-36 pl-7"> </v-select> -->
      <!-- <v-menu :location="'end'">
            <v-list>
               <v-list-item v-for="(item, index) in items"> </v-list-item>
            </v-list>
         </v-menu> -->
      <v-btn color="info" dark variant="outlined" @click="fetch_Quran">
         Set
      </v-btn>
   </div>
   <v-divider :thickness="3"></v-divider>

   <v-container>
      <v-row dense>
         <v-col v-for="(ListSurat, i) in ListSurats" :key="i" cols="12" md="4">
            <v-card class="mx-6 hover:text-blue-500" variant="outlined" @click="detailSurah(ListSurat.nomor)">
               <v-card-item :title="ListSurat.namaLatin">
                  <template v-slot:subtitle>
                     <div class="py-0">
                        <v-row no-gutters align="center">
                           <v-col class="md:flex">
                              <div>
                                 {{ ListSurat.arti + ' ' }}&bull;

                              </div>
                              <div>

                                 {{ ' ' + ListSurat.jumlahAyat + ' Ayat' }}
                              </div>
                           </v-col>
                        </v-row>
                     </div>
                  </template>
                  <template v-slot:prepend>
                     <v-img class="bg-transparent text-black w-60 md:w-10"  aspect-ratio="1/1"
                        src="/public/img/nomor1.png">
                        <div class="d-flex align-center justify-center text-l md:text-sm " style="height: 100%;">
                           {{ ListSurat.nomor }}
                        </div>
                     </v-img>
                  </template>
                  <template v-slot:append>
                     <v-col class="text-right font-serif text-h5">{{ ListSurat.nama }}</v-col>
                  </template>
               </v-card-item>
            </v-card>
         </v-col>
      </v-row>
   </v-container>
</template>
