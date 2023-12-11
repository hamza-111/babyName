<script setup lang="ts">
import {Gender, Popularity, Length, names} from "@/data"

  interface Options {
    gender: Gender;
    popularity: Popularity;
    length: Length;
  }

  const options = reactive<Options>({
    gender: Gender.GIRL,
    popularity: Popularity.UNIQUE,
    length: Length.LONG,
  });

  const selectedName = ref<string[]>([]);

  const removeName = (name: string) => {
    selectedName.value = selectedName.value.filter(n => n !== name);
  };
  
  const findName = () => {
    selectedName.value = names.filter((name) => {
      return name.gender === options.gender &&
        name.popularity === options.popularity &&
        (options.length === Length.ALL || name.length === options.length)
    }).map((name) => name.name);
  };

  const optionsArray = [
    {
      title : "1) Choose a gender",
      category : "gender",
      buttons : [Gender.BOY, Gender.GIRL, Gender.UNISEX]
    },
    {
      title : "2) Choose the name's popularity",
      category : "popularity",
      buttons : [Popularity.UNIQUE, Popularity.TRENDY]
    },
    {
      title : "3) Choose a length of name",
      category : "length",
      buttons : [Length.SHORT, Length.LONG, Length.ALL]
    }
  ]
</script>

<template>
  <div class="p-8">
    <h1 class="text-4xl font-bold mb-4 text-center">Baby Name Generator</h1>
    <p class="text-gray-600 mb-8 text-center">Choose your options and click the right button</p>
    <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
      <Options v-for="option in optionsArray" :key="option.title" :option="option" :options="options"></Options>
    </div>
    <div class="text-center mt-8">
      <button @click="findName" class="bg-blue-500 text-white px-4 py-2 rounded">Find Name</button>
    </div>
        <!-- Response -->
    <div class="mt-8">
      <h2 class="text-2xl font-semibold mb-4 text-center">Generated Names</h2>
      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4  mx-auto">
        <!-- Boucle à travers les noms générés et les afficher ici -->
        <NameCard :selectedName="selectedName" @remove="removeName"></NameCard>
      </div>
    </div>
  </div>
</template>
