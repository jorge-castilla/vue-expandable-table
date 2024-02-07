<template>
  <main class="w-screen h-screen flex justify-center items-center">
    <expandable-table :data="data" :columns="columns"></expandable-table>
  </main>
</template>

<script setup>
import ExpandableTable from '@/components/ExpandableTable.vue'
import { ref } from 'vue'
const data = ref([
  { name: 'Luke', Homeworld: 'Tatooine', age: 19, birthDate: '1996-01-01' },
  { name: 'Leia', Homeworld: 'Alderaan', age: 19, birthDate: '1994-01-02', father: 'Anakin' }
])

const columns = ref([
  { label: 'Name', field: 'name' },
  { label: 'Age', field: 'age' },
  { label: 'Homeworld', field: 'Homeworld' }
])
</script>
