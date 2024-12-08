<script lang="ts" setup>
const route = useRoute();
const nomerSurah = route.query.nomerSurah;

const response = await $fetch('https://equran.id/api/v2/surat/' + nomerSurah);
const ayats = response.data;
// console.log(ayats)
// let listAyat=ayats.ayat.find((item)=>item.teksArab)
// let listAyat = ayats.map((item) => {
//     return {
//         nomerAyat: item.nomerAyat,
//         teksArab: item.teksArab
//     };
// });
var listAyat = [];
const file = ref('http://www.hochmuth.com/mp3/Boccherini_Concerto_478-1.mp3')

for (let i = 0; i < ayats.ayat.length; i++) {
    listAyat.push(ayats.ayat[i]);

}
console.log(listAyat)
console.log(listAyat[2].audio['02'])
const audioFinish = () => {
    console.log('Audio finished playing')
}
</script>

<style></style>

<template>
    <v-container>
        <div class="align-middle justify-center items-center ">
            <div class="pt-4 max-w-full mx-auto flex items-center justify-center  ">
                <v-img class="h-auto bg-transparent text-white filter invert" aspect-ratio="16/9"
                    src="/public/img/pngwing.com (2).png" cover>
                </v-img>
            </div>
        </div>
    </v-container>
    <v-container>
        <div v-for="(ayat, i) in listAyat">

            <figure class="mt-4 items-center md:flex bg-slate-100 rounded-md p-8 md:p-0 dark:bg-slate-800">
                <div class="ml-5 w-20">
                    <v-img class=" w-24 h-24 md:w-48 md:h-auto md:rounded-none rounded-full mx-auto"
                        src="/public/img/nomor.png" alt="" width="100" height="100">
                        <div class="d-flex align-center justify-center text-h5 text-blue" style="height: 100%;">
                            {{ i + 1 }}
                        </div>
                    </v-img>
                </div>
                <div class="pt-6 md:p-8 w-full text-right md:text-right space-y-4">
                    <blockquote>
                        <p class="text-lg text-h3 font-serif">
                            {{ ayat.teksArab }}
                        </p>
                    </blockquote>
                    <figcaption class="text-left font-medium">
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
                    </figcaption>
                </div>
            </figure>
        </div>

    </v-container>
    <!-- <v-container class=" align-middle justify-center justify-items-center md:justify-center md:align-middle">
        <div class="w-62 items-center md:items-center">
            <v-img class="flex h-auto bg-transparent text-white filter invert w-72" aspect-ratio="16/9"
                src="/public/img/pngwing.com (2).png">
            </v-img>
        </div>
        <div class="bg-red flex items-center justify-center">
            <v-row dense class="pt-8 md:align-middle md:justify-center items-center content-center">
                <v-col v-for="(ayat, i) in listAyat" :key="i" cols="12"
                    class="flex md:align-middle md:justify-center align-middle justify-center">
                    <v-card class="hover:text-blue-500 w-96  " variant="outlined">
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
                                <v-img class="bg-transparent text-white filter invert" :width="50" aspect-ratio="1/1"
                                    src="/public/img/nomor.png">
                                    <div class="d-flex align-center justify-center text-h6 text-blue"
                                        style="height: 100%;">
                                        {{ i + 1 }}
                                    </div>
                                </v-img>
                            </template>
<template v-slot:append>
                                <v-col class="text-right font-serif text-h5">{{ ayat.teksArab }}</v-col>
                            </template>
</v-card-item>
<v-card-subtitle class="md:text-left md:text-lg lg:text-xl space-y-4">
    {{ ayat.teksIndonesia }}
</v-card-subtitle>
</v-card>
</v-col>
</v-row>
</div>
</v-container> -->
</template>