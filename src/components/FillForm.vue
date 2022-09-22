<template>
  <div v-if="errors.length">
    <strong>Corrige los siguientes errores: </strong>
    <ul>
      <li v-for="error in errors" :key="error">{{ error }}</li>
    </ul>
  </div>
  <form>
    <input type="text" v-model="formData.name" placeholder="Nombre" required />
    <br />
    <input type="text" v-model="formData.lastName" placeholder="Apellido" />
    <div class="wrapper">
      <div>
        <input type="checkbox" id="myCheckbox1" />
        <label for="myCheckbox1"
          ><img src="../assets/ODS/S-WEB-Goal-01.png"
        /></label>
      </div>
      <div>
        <input type="checkbox" id="myCheckbox2" />
        <label for="myCheckbox2"
          ><img src="../assets/ODS/S-WEB-Goal-02.png"
        /></label>
      </div>
      <div>
        <input type="checkbox" id="myCheckbox3" />
        <label for="myCheckbox3"
          ><img src="../assets/ODS/S-WEB-Goal-03.png"
        /></label>
      </div>
      <div>
        <input type="checkbox" id="myCheckbox4" />
        <label for="myCheckbox4"
          ><img src="../assets/ODS/S-WEB-Goal-04.png"
        /></label>
      </div>
      <div>
        <input type="checkbox" id="myCheckbox5" />
        <label for="myCheckbox5"
          ><img src="../assets/ODS/S-WEB-Goal-05.png"
        /></label>
      </div>
    </div>
    <div class="select">
      <label class="fav-label">Si quieres, elige tu fav:</label> <br />
      <select name="char" v-model="formData.fav">
        <option v-for="char in this.characters" :key="char">
          {{ char.Name }}
        </option>
      </select>
    </div>
    <button @click="sendForm()">ENVIAR</button>
  </form>
</template>
<script>
export default {
  name: "FillForm",
  emits: {
    update: null,
  },
  data() {
    return {
      formData: {},
      characters: [],
      eachChar: [],
      errors: [],
    };
  },
  created() {
    fetch("https://futuramaapi.herokuapp.com/api/v2/characters")
      .then((response) => response.json())
      .then((data) => (this.characters = data));

    /*     for (let i = 0; i < this.characters.length; i++) {
      console.log(this.characters[i]);
    } */
  },
  methods: {
    checkInputs() {
      this.errors = [];
      if (!this.formData.name) {
        this.errors.push("Escribe tu nombre.");
      }
      if (!this.formData.lastName) {
        this.errors.push("Escribe tu apellido.");
      }
    },
    sendForm() {
      this.$emit("update", this.formData);
      this.checkInputs();
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
