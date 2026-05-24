<template>
  <div class="fixed-top w-100 h-100 overflow-hidden pointer-events-none z-0">
    <!-- The Central Rainbow Gleam -->
    <div class="position-absolute top-0 start-50 translate-middle-x opacity-60" style="width: 800px; height: 400px; margin-top: -100px;">
      <div class="w-100 h-100 rainbow-gleam"></div>
    </div>

    <!-- Side Accents -->
    <div class="position-absolute top-25 start-0 translate-middle-x bg-primary bg-opacity-10 rounded-circle" style="width: 500px; height: 500px; filter: blur(100px);"></div>
    <div class="position-absolute bottom-0 end-0 bg-purple bg-opacity-10 rounded-circle" style="width: 600px; height: 600px; filter: blur(130px); margin-bottom: -100px; margin-right: -50px;"></div>
  </div>
</template>

<script>
export default {
  name: 'Background'
}
</script>

<style scoped>
.z-0 { z-index: 0; }
.pointer-events-none { pointer-events: none; }
</style>
