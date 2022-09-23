<template>
  <div>view Form</div>
  <span>{{ formData.name }}</span>
  <span>{{ formData.lastName }}</span>
  <span>{{ formData.ods }}</span>
  <span>{{ formData.favouriteCharacter }}</span>
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
