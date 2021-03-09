<template>
  <div class="card flex justify-center items-center">
    <h1>{{ name }}</h1>
  </div>
</template>

<script>
export default {
  props: {
    name: {
      type: String,
      default: '',
    },
  },
}
</script>

<style lang="scss" scoped>
.card {
  @apply flex flex-grow-0 flex-shrink-0 rounded-3xl bg-white shadow-lg;

  height: 463px;
  width: 364px;
  margin-bottom: 20px;
}
</style>
