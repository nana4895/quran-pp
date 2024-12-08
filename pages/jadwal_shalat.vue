<script lang="ts" setup>
import { ref, watch } from 'vue';
const model = ref('');

    watch(model, (newValue) => {
      console.log(newValue);
    });
</script>

<template>
  <!-- <div>
    <v-icon icon="fas fa-user" />
    <v-icon icon="mdi:home" />
  </div>
  <v-col cols="auto">
    <v-btn density="compact" icon="mdi-plus"></v-btn>
  </v-col> -->

  <v-switch
    v-model="model"
    :label="`Switch: ${model.toString()}`"
    hide-details
    
  ></v-switch>

</template>