<script setup>
import { computed } from "vue";
import { useStore } from "vuex";
const store = useStore();


const layout = computed(() => store.state.layout);
defineProps({
  card: {
    type: Object,
    required: true,
    title: String,
    description: String,
    links: {
      type: Array,
      default: () => [],
      label: String,
      route: String,
      color: String,
    },
  },
});
</script>

<template>
  <div v-show="layout !== 'landing'" class="card card-plain shadow-none" id="sidenavCard">
    <div v-if="card">
      <h2>{{ card.title }}</h2>
      <p>{{ card.description }}</p>
      <ul>
        <li v-for="link in card.links" :key="link.label">
          <a :href="link.route" :style="{ color: link.color }">{{ link.label }}</a>
        </li>
      </ul>
    </div>
  </div>
</template>
