<template>
  <footer class="footer">
    <p>&copy;{{ new Date().getFullYear() }}</p>
  </footer>
</template>

<script setup></script>

<style lang="scss">
.footer {
  position: sticky;
  bottom: 0;
  padding: 10px;
  background: #000;
  color: #fff;
  z-index: 100;
}
</style>
