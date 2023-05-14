<template>
  <tr>
    <th scope="row">{{ data[0] }}</th>
    <td v-for="i in data.length - 1">{{ data[i] }}</td>
  </tr>
</template>

<script setup>
/* ---------------- props ------------------- */
const props = defineProps(["data"]);
/* ---------------- data -------------------- */
/* ---------------- refs -------------------- */
/* ---------------- computed ---------------- */
/* ---------------- functions --------------- */
/* ---------------- watchers ---------------- */
/* ------------- lifecycle hooks ------------ */
</script>

<style>
</style>