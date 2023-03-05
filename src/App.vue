<template>
  <div class="h-screen feather flex justify-center gap-10 p-5">
    <div
      v-for="column in data.children"
      :key="column"
      class="flex flex-col gap-6">
      <div
        v-for="row in column.children"
        :key="row"
        class="flex justify-center gap-6">
        <skill
          v-for="item in row"
          :key="item"
          :name="item.name"
          :image="item.image"
          :items="item.items" />
      </div>
    </div>
  </div>
</template>

<script setup>
import Skill from './components/Skill/index.vue';
import data from '../data.json';
</script>
