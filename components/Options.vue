<script setup lang="ts">
    import {Gender, Popularity, Length} from "@/data"

    interface OptionProps {
        option : {
            title : String;
            category : String ;
            buttons : Gender[] | Popularity[] | Length[]
        };
        options : {
            gender : Gender;
            popularity : Popularity;
            length : Length
        };
    }
    const props = defineProps<OptionProps>()
</script>
<template>
    <div class="bg-white p-4 rounded shadow-md">
      <h4 class="text-lg font-semibold mb-4 text-center">{{option.title }}</h4>
      <div class="flex space-x-4 justify-center">
        <button
          v-for="(value,index) in option.buttons"
          :key="index"
          @click="options[option.category] = value"
          :class="options[option.category as 'gender'|'popularity'|'length'] === value && 'bg-blue-950'"
          class="bg-blue-500 text-white px-4 py-2 rounded"
        >
          {{ value }}
        </button>
      </div>
    </div>
  </template>