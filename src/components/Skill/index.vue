<template>
  <div>
    <div
      class="relative h-24 w-24 flex justify-center items-center"
      @click="data.showModal = !data.showModal">
      <svg
        class="absolute"
        viewBox="0 0 36 36">
        <path
          fill="transparent"
          stroke="#E5E5E5"
          stroke-width="3"
          d="M18 2.0845 a 15.9155 15.9155 0 0 1 0 31.831 a 15.9155 15.9155 0 0 1 0 -31.831" />
        <path
          fill="transparent"
          stroke="#FFC800"
          :stroke-dasharray="formattedProgress"
          :stroke-width="doneItemCount ? 3 : 0"
          stroke-linecap="round"
          d="M18 2.0845 a 15.9155 15.9155 0 0 1 0 31.831 a 15.9155 15.9155 0 0 1 0 -31.831" />
      </svg>
      <img
        class="absolute h-16 w-16 p-2.5 bg-blue-400 rounded-full select-none pointer-events-none"
        :src="image"
        alt="">
      <div
        v-if="data.showModal && items.length"
        class="absolute w-max p-4 top-24 bg-blue-400 rounded-2xl z-50">
        <ul>
          <li
            v-for="item in items"
            :key="item"
            class="flex text-white font-semibold items-center">
            <div class="h-5 w-5 mr-1.5">
              <check-badge-icon
                v-if="item.status"
                class="h-4.5 w-4.5" />
            </div>
            {{ item.content }}
          </li>
        </ul>
      </div>
    </div>
    <div class="font-bold capitalize text-center">
      {{ name }}
    </div>
  </div>
</template>

<script>
export default {
  name: 'Skill'
};
</script>

<script setup>
import { computed, defineProps, reactive } from 'vue';
import { CheckBadgeIcon } from "@heroicons/vue/24/solid";

const props = defineProps({
  name: {
    type: String,
    required: true
  },
  image: {
    type: String,
    required: true
  },
  items: {
    type: Array,
    default: () => []
  }
});

const data = reactive({
  showModal: false,
});

const doneItemCount = computed(() => props.items.reduce((result, item) => result + Number(item.status), 0));

const formattedProgress = computed(() => `${doneItemCount.value / props.items.length * 100 || 0}, 100`);
</script>
