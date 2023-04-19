
<template>
  <main>
    <form @submit.prevent="submitForm">
      <div>
        <label for="height">Рост</label>
        <input type="number" id="height" v-model="height" required>
      </div>
      <div>
        <label for="weight">Вес</label>
        <input type="number" id="weight" v-model="weight" required>
      </div>
      <label for="schema">Выберите схему</label>
      <select id="schema" v-model="selectedOption" >
        <option value="FOLFOX">FOLFOX</option>
        <option value="FOLFIRI">FOLFIRI</option>
        <option value="FOLFOX_B_MAB">FOLFOX + b-mab</option>
      </select>
      <button type="submit">Submit</button>
    </form>
    <p>S = {{summarize}} M<sup>2</sup></p>
    <template v-for="(elem, index) in selectedObject" :key="index">
      <p>{{elem.name}} {{elem.value * summarize}}</p>

    </template>
  </main>
</template>

<script>
export default {
  data() {
    return {
      height: '',
      weight: '',
      password: '',
      confirmPassword: '',
      selectedOption: '',
      schema: {
        FOLFOX: [
          {name: 'oxaliplitinum', value: 85},
          {name: 'CalciumFolinate', value: 400},
          {name: 'FtorUracileFirst', value: 400},
          {name: 'FtorUracileSecond', value: 2400},
        ],
        FOLFIRI: [
          {name: 'Irinotekani', value: 180},
          {name: 'CalciumFolinate', value: 400},
          {name: 'FtorUracileFirst', value: 400},
          {name: 'FtorUracileSecond', value: 2400},
        ],
        FOLFOX_B_MAB: [
          {name: 'oxaliplitinum', value: 85},
          {name: 'CalciumFolinate', value: 400},
          {name: 'FtorUracileFirst', value: 400},
          {name: 'FtorUracileSecond', value: 2400},
          {name: 'Avegra', value: 400},
        ],
      },
    }
  },
  methods: {
    submitForm() {
      // this.sum = Number(this.email) + Number(this.name)
    }
  },
  computed: {
    selectedObject() {
      console.log(this.schema[this.selectedOption]);
      return this.schema[this.selectedOption];
    },
      summarize(){
        let sum = (Math.sqrt((Number(this.height) * Number(this.weight)) / 3600)).toFixed(2)
        return isNaN(sum) ? 0 : sum
      }
  }
}
</script>

<style lang="scss" scoped>
main{
  width: 100%;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}
</style>
