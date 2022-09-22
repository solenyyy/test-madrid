<template>
  <input type="text" v-model="formData.name" />
  <button @click="sendForm()">ENVIAR</button>
</template>
<script>
export default {
  name: "FillForm",
  data() {
    return {
      formData: {},
    };
  },

  methods: {
    sendForm() {
      this.$emit("update", this.formData);
    },
  },
};
</script>
