<template>
  <form action="javascript:void(0);">
    <div class="margin">
      <div class="form-field">
        <label for="name">Tu nombre:</label>
        <input
          type="text"
          v-model="formData.name"
          placeholder="Nombre"
          required
        />
      </div>
      <div class="form-field">
        <label for="lastname">Tu apellido:</label>
        <input
          type="text"
          v-model="formData.lastName"
          placeholder="Apellido"
          required
        />
      </div>
      <div class="check-field">
        <label v-if="!validODSSelection"
          >Tienes que elegir entre 1 y 3 ODS:</label
        >
        <div class="wrapper">
          <div v-for="ods in allODSs" :key="ods.id">
            <input
              required
              type="checkbox"
              :id="ods.id"
              @change="check($event)"
            />
            <label for="ods.id"
              ><img :src="require(`../assets/ODS/${ods.image}`)"
            /></label>
          </div>
        </div>
      </div>
      <div class="select">
        <label class="fav-label">Elige tu fav:</label>
        <select name="char" v-model="formData.favouriteCharacter">
          <option v-for="char in this.characters" :key="char">
            {{ char.Name }}
          </option>
        </select>
      </div>
      <button class="btn" @click="sendForm()">Enviar</button>
    </div>
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
    };
  },
  computed: {
    validODSSelection: function () {
      return this.formData.ods.length > 0 && this.formData.ods.length < 4;
    },
    allODSs: function () {
      return ODSs;
    },
  },
  created() {
    fetch("https://futuramaapi.herokuapp.com/api/v2/characters")
      .then((response) => response.json())
      .then((data) => (this.characters = data));
  },
  methods: {
    sendForm() {
      if (this.validODSSelection) this.$emit("update", this.formData);
    },
    check: function (event) {
      if (event.target.checked) {
        this.formData.ods.push(event.target.id);
      } else {
        const indexOfOds = this.formData.ods.indexOf(event.target.id);
        if (indexOfOds > -1) this.formData.ods.splice(indexOfOds, 1);
      }
    },
  },
};
</script>
<style scoped>
ul {
  list-style: none;
}

img {
  width: 100px;
}

.wrapper {
  display: flex;
  flex-direction: row;
  justify-content: space-evenly;
}

form {
  max-width: 700px;
  padding: 3rem;
  font-family: Arial, Helvetica, sans-serif;
  color: #222;
  font-size: 1.1rem;
  border-radius: 20px;
  border: 2px solid transparent;
  margin: 0 auto;
  box-shadow: 1px 1px 6px 1px rgba(128, 128, 128, 0.674);
}

.form-field,
.select {
  margin: 0 0 1rem 0;
}
label,
input,
select {
  width: 70%;
  padding: 0.5rem;
  box-sizing: border-box;
  justify-content: space-between;
}
label {
  text-align: right;
  width: 30%;
  font-weight: 600;
}

input,
select {
  border: 2px solid #aaa;
  border-radius: 10px;
}

.btn {
  border: 2px solid #aaa;
  background-color: transparent;
  border-radius: 2px;
  padding: 0.5rem 2rem;
  font-size: 1.1rem;
  border-radius: 10px;
  cursor: pointer;
  margin: 0 auto;
  font-family: Arial, Helvetica, sans-serif;
}
.btn:hover {
  border: 2px solid #000;
}
.wrapper {
  margin: 2% 0 5% 0;
}
@media (max-width: 600px) {
  img {
    width: 60px;
  }
}
</style>
