<template>
  <FillForm v-if="!formAnswered" @update="this.onFormSubmited"></FillForm>
  <ViewForm :formData="formData" v-else></ViewForm>
</template>

<script>
import FillForm from "../components/FillForm.vue";
import ViewForm from "../components/ViewForm.vue";

export default {
  name: "Form",
  components: {
    FillForm,
    ViewForm,
  },
  data() {
    return {
      formAnswered: false,
      formData: {
        name: "",
        lastName: "",
        ods: [],
        favouriteCharacter: "",
      },
    };
  },
  methods: {
    onFormSubmited(payload) {
      this.formData = payload;
      this.formAnswered = true;
    },
  },
};
</script>
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
