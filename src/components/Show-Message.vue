<template>
  <div class="m-6 text-white text-xs w-[100vh] md:h-full overflow-auto">
    <h3>Message:</h3>
    <h2>{{ msg }}</h2>
  </div>
</template>
<script setup>
defineProps({
  msg: {
    type: String,
  },
});
</script>
