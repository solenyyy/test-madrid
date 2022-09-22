<template>
  <div>view Form</div>
  <span>{{ formData.name }}</span>
</template>
<script>
export default {
  props: {
    formData: {
      name: String,
    },
  },
};
</script>
