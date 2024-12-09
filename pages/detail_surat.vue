<script lang="ts" setup>
const route = useRoute();
const nomerSurah = route.query.nomerSurah;

const response = await $fetch('https://equran.id/api/v2/surat/' + nomerSurah);
const ayats = response.data;
console.log(ayats)
// let listAyat=ayats.ayat.find((item)=>item.teksArab)
// let listAyat = ayats.map((item) => {
//     return {
//         nomerAyat: item.nomerAyat,
//         teksArab: item.teksArab
//     };
// });
var listAyat = [];
var listAudio = [];
const file = ref('http://www.hochmuth.com/mp3/Boccherini_Concerto_478-1.mp3')

for (let i = 0; i < ayats.ayat.length; i++) {
    listAyat.push(ayats.ayat[i]);
    listAudio.push(ayats.ayat[i].audio['02']);

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
                        <audio controls>
                            <source :src="ayat.audio['02']" type="audio/mpeg">
                        </audio>
                        <!-- <button @click="playAudio">
                            play
                        </button> -->
                    </figcaption>
                </div>
            </figure>
        </div>

    </v-container>
    <!-- <v-container class="justify-center align-middle justify-items-center md:justify-center md:align-middle">
        <div class="items-center w-62 md:items-center">
            <v-img class="flex h-auto text-white bg-transparent filter invert w-72" aspect-ratio="16/9"
                src="/public/img/pngwing.com (2).png">
            </v-img>
        </div>
        <div class="flex items-center justify-center bg-red">
            <v-row dense class="items-center content-center pt-8 md:align-middle md:justify-center">
                <v-col v-for="(ayat, i) in listAyat" :key="i" cols="12"
                    class="flex justify-center align-middle md:align-middle md:justify-center">
                    <v-card class="hover:text-blue-500 w-96 " variant="outlined">
                        <v-card-item>
                            <template v-slot:subtitle>
                                <div class="py-4">
                                    <v-row no-gutters align="center">
                                        <v-col>{{ ayat.teksIndonesia }}
                                        </v-col>
                                    </v-row>
                                </div>
                            </template>
<template v-slot:prepend>
                                <v-img class="text-white bg-transparent filter invert" :width="50" aspect-ratio="1/1"
                                    src="/public/img/nomor.png">
                                    <div class="justify-center d-flex align-center text-h6 text-blue"
                                        style="height: 100%;">
                                        {{ i + 1 }}
                                    </div>
                                </v-img>
                            </template>
<template v-slot:append>
                                <v-col class="font-serif text-right text-h5">{{ ayat.teksArab }}</v-col>
                            </template>
</v-card-item>
<v-card-subtitle class="space-y-4 md:text-left md:text-lg lg:text-xl">
    {{ ayat.teksIndonesia }}
</v-card-subtitle>
</v-card>
</v-col>
</v-row>
</div>
</v-container> -->
</template>