<template>
    <div>
        <footer class="py-5 mt-0 bg-darkmorphic text-center">
            <p class="mb-0 text-white small">
            &copy; {{ new Date().getFullYear() }} Aryant Nigam. All rights reserved.
            </p>
        </footer>
    </div>
</template>
<script>
export default {
  name: 'Footer'
}
</script>
<style scoped>  
.bg-darkmorphic{
    background: rgba(10, 10, 10, 0.65) !important;
    backdrop-filter: blur(24px);
    -webkit-backdrop-filter: blur(24px);
}
</style>