<template>
  <div>
    <form>
      <div id="converter"> <label for="converter-px"><input id="converter-px" type="number" v-model="inputPx"
            @input="updater('inputPx')">px </label>
        <span> = </span>
        <label for="converter-rem"><input id="converter-rem" type="number" v-model="inputRem"
            @input="updater('inputRem')">rem</label>
      </div>
      <label for="root-element-size">Root element size <input id="root-element-size" type="number"
          v-model="rootElementSize" @input="updater('rootElementSize')">px</label>
    </form>
    <table id="common-table">
    </table>
  </div>
</template>

<script>

export default {
  data() {
    return {
      rootElementSize: 16,
      inputPx: 16,
      inputRem: 1
    }
  },
  mounted() {
    this.renderTable();
  },
  methods: {
    updater(changedVar) {
      if (changedVar === "inputPx") {
        this.inputRem = (this.inputPx / this.rootElementSize);
      } else if (changedVar === "inputRem") {
        this.inputPx = this.inputRem * this.rootElementSize;
      } else if (changedVar === "rootElementSize") {
        this.inputRem = (this.inputPx / this.rootElementSize);
      }
      this.renderTable();
    },
    renderTable() {
      let table = document.querySelector("#common-table");
      let tablebody = document.createElement("tbody");

      table.innerHTML = "";

      for (let i = 8; i < 33; i++) {
        let rem = (i / this.rootElementSize);
        let row =
          `<tr>
            <td>${i}px</td><td>=</td>
            <td>${rem}rem</td>
        </tr>`;
        tablebody.insertAdjacentHTML("beforeend", row);
      }

      table.append(tablebody);
    }
  },

}
</script>

<style lang="scss">
$dark: #1f1f1f;
$light: #f7f9f9;

body {
  background-color: $dark;
  color: $light;
  font-size: larger;
}

form {
  margin: 5rem auto;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 2rem;

  input {
    font-size: larger;
    background-color: $dark;
    color: $light;
    text-align: center;
    border: none;
    border-bottom: dotted 1px $light;
  }
}

table {
  margin: 4rem auto;
}
</style>