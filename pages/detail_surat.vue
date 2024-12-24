<script lang="ts" setup>
const route = useRoute();
const nomerSurah = route.query.nomerSurah;

const fetchSurah = await $fetch('https://equran.id/api/v2/surat/' + nomerSurah);
const ayats = fetchSurah.data;

const fetchTafsir = await $fetch('https://equran.id/api/v2/tafsir/' + nomerSurah);
var tafsir = fetchTafsir.data;

var listAyat = [];
var listTafsir=[];
var listAudio = [];
const file = ref('http://www.hochmuth.com/mp3/Boccherini_Concerto_478-1.mp3')

for (let i = 0; i < ayats.ayat.length; i++) {
    listAyat.push(ayats.ayat[i]);
    listAudio.push(ayats.ayat[i].audio['02']);
    for (var j = 0; j < tafsir.tafsir.length; j++) {
      listTafsir.push(tafsir.tafsir[j].teks);
    }
}

const dialog = reactive({
  dialog: false,
});
var teksTafsir='';
var title='';
const tafsir_ayat=async (ayat:any)=>{
  dialog.dialog = true;
   title = 'Tafsir Ayat ' +(ayat+1);
  teksTafsir = listTafsir[ayat]
}
</script>

<style></style>

<template>
    <v-container>
        <div class="items-center justify-center align-middle ">
            <div class="flex items-center justify-center max-w-full pt-4 mx-auto ">
                <v-img class="h-auto text-white bg-transparent filter invert" aspect-ratio="16/9"
                    src="/public/img/pngwing.com (2).png" cover>
                </v-img>
            </div>
        </div>
    </v-container>
    <v-container>
        <div v-for="(ayat, i) in listAyat">
            <figure class="items-center p-8 mt-4 rounded-md md:flex bg-slate-100 md:p-0 dark:bg-slate-800">
                <div class="w-20 ml-5">
                    <v-img class="w-24 h-24 mx-auto rounded-full md:w-48 md:h-auto md:rounded-none"
                        src="/public/img/nomor.png" alt="" width="100" height="100">
                        <div class="justify-center d-flex align-center text-h5 text-blue" style="height: 100%;">
                            {{ i + 1 }}
                        </div>
                    </v-img>
                </div>
                <div class="w-full pt-6 space-y-4 text-right md:p-8 md:text-right">
                    <blockquote>
                        <p class="font-serif text-lg text-h3">
                            {{ ayat.teksArab }}
                        </p>
                    </blockquote>
                    <figcaption class="font-medium text-left">
                        <div class="text-sky-500 dark:text-sky-400">
                            {{ ayat.teksLatin }}
                        </div>
                        <div class="text-slate-700 dark:text-slate-500">
                            {{ ayat.teksIndonesia }}
                            {{ ayat.audio[1] }}
                        </div>
<!--                        <audio controls>-->
<!--                            <source :src="ayat.audio['02']" type="audio/mpeg">-->
<!--                        </audio>-->
                      <v-btn x-small dark variant="outlined" @click="tafsir_ayat(i)" class="pa-1 mt-4">Tafsir</v-btn>
                    </figcaption>
                </div>
            </figure>
        </div>

    </v-container>

  <v-dialog v-model="dialog.dialog" max-width="800" persistent>
    <v-card>
      <v-card :title="title" class="pa-4">
        <template v-slot:text>
          <p class="text-lg">{{teksTafsir}}</p>
        </template>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn @click="dialog.dialog = false">Tidak</v-btn>
          <v-btn >Ya</v-btn>
        </v-card-actions>
      </v-card>


    </v-card>
  </v-dialog>
</template>