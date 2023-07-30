<script setup>
import { ref, watch, computed, onBeforeMount, onMounted } from 'vue';
import axios from 'axios'

defineProps({
  msg: String,
  total: Number,
});

const user = ref({
  first: 'Eric',
  last: 'Carvalho',
});

const changeName = () => {
  user.value.first = 'Val';
};

watch(
  user,
  () => {
    console.log('Watch here!');
  },
  {
    deep: true,
  }
);

const fullName = computed(() => user.value.first + ' ' + user.value.last )

const result = ref([])

onBeforeMount(() => {
  axios.get('https://jsonplaceholder.typicode.com/todos/1')
      .then(response => {
        result.value.push(response.data)
      })

})

</script>

<template>
  <h1 @click="changeName()">{{ msg }}</h1>
  <pre>{{ user.first }}</pre>
  <pre>{{ fullName }}</pre>
  <pre>{{ total }}</pre>
  <pre v-if="result">{{ result }}</pre>
</template>

<style scoped>
.read-the-docs {
  color: #888;
}
</style>
