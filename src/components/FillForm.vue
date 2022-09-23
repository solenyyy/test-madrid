<template>
  <div v-if="errors.length">
    <strong>Corrige los siguientes errores: </strong>
    <ul>
      <li v-for="error in errors" :key="error">{{ error }}</li>
    </ul>
  </div>
  <form action="javascript:void(0);">
    <input type="text" v-model="formData.name" placeholder="Nombre" required />
    <br />
    <input
      type="text"
      v-model="formData.lastName"
      placeholder="Apellido"
      required
    />
    <div class="wrapper">
      <span v-if="!validODSSelection">Solo elige entre 1 y 3 ODS:</span>
      <div v-for="ods in getAllODSs()" :key="ods.id">
        <input type="checkbox" :id="ods.id" @change="check($event)" />
        <label for="ods.id"
          ><img :src="require(`../assets/ODS/${ods.image}`)"
        /></label>
      </div>
    </div>
    <div class="select">
      <label class="fav-label">Si quieres, elige tu fav:</label> <br />
      <select name="char" v-model="formData.favouriteCharacter">
        <option v-for="char in this.characters" :key="char">
          {{ char.Name }}
        </option>
      </select>
    </div>
    <button @click="sendForm()">Enviar</button>
  </form>
</template>
<script>
import { ODSs } from "../ods.js";

export default {
  name: "FillForm",
  emits: {
    update: null,
  },
  data() {
    return {
      formData: {
        name: "",
        lastName: "",
        favouriteCharacter: "",
        ods: [],
      },
      characters: [],
      eachChar: [],
      errors: [],
    };
  },
  computed: {
    validODSSelection: function () {
      return this.formData.ods.length > 0 && this.formData.ods.length < 4;
    },
  },
  created() {
    fetch("https://futuramaapi.herokuapp.com/api/v2/characters")
      .then((response) => response.json())
      .then((data) => (this.characters = data));
  },
  methods: {
    sendForm() {
      console.log(this.formData);
      if (this.validODSSelection) this.$emit("update", this.formData);
    },
    check: function (event) {
      if (event.target.checked) {
        this.formData.ods.push(event.target.id);
      } else {
        const indexOfOds = this.formData.ods.indexOf(event.target.id);
        if (indexOfOds > -1) this.formData.ods.splice(indexOfOds, 1);
      }
      console.log(this.formData.ods);
    },
    getAllODSs() {
      return ODSs;
    },
  },
};
</script>
<style scoped>
form {
  width: 70%;
  margin: 0 auto;
  border: 1px solid black;
  border-radius: 20px;
}

ul {
  list-style: none;
}

img {
  width: 100px;
}

.wrapper {
  display: flex;
  flex-direction: row;
  justify-content: center;
}

input {
  margin: 20px;
}

button {
  margin: 20px;
}
</style>
