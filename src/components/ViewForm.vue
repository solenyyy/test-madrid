<template>
  <div class="wrapper">
    <div class="title">Esta fue tu selección:</div>
    <ul>
      <li class="data">{{ formData.name }}</li>

      <li class="data">{{ formData.lastName }}</li>

      <li class="data">{{ formData.ods }}</li>

      <li class="data">{{ formData.favouriteCharacter }}</li>
    </ul>
    <div class="title align">¡Gracias!</div>
  </div>
</template>
<script>
export default {
  props: {
    formData: {
      name: String,
      lastName: String,
      ods: Array,
      favouriteCharacter: String,
    },
  },
};
</script>
<style scoped>
.wrapper {
  max-width: 280px;
  text-align: left;
  padding: 2.5rem;
  margin: 0 auto;
  font-family: monospace;
  color: #222;
  font-size: 1.3rem;
  border-radius: 20px;
  border: 2px solid transparent;
  box-shadow: 1px 1px 6px 1px rgba(128, 128, 128, 0.674);
}
.title {
  font-weight: 600;
  margin-bottom: 10px;
  font-size: 1.4rem;
}
.align {
  text-align: center;
}
</style>
