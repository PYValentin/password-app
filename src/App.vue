<template>
  <div id="app">
    <div class="wrapper">
      <h1>
        Bravo!<br />
        Les lutins ont livrés leurs cadeaux!
      </h1>
      <h3>
        📦📦 Ils vous ont laissé une mysterieuse boite avec un cadenas... 📦📦
        <br />À vous de trouver le code!
      </h3>
      <div class="input__wrapper">
        <input
          class="input"
          ref="input1"
          type="number"
          maxlength="1"
          @input="goToNext()"
          v-model="input1"
        />
        <input
          class="input"
          ref="input2"
          type="number"
          maxlength="1"
          @input="goToNext()"
          v-model="input2"
        />
        <input
          class="input"
          ref="input3"
          type="number"
          maxlength="1"
          @input="goToNext()"
          v-model="input3"
        />
        <input
          class="input"
          ref="input4"
          type="number"
          maxlength="1"
          v-model="input4"
        />
      </div>
      <div class="validate__wrapper">
        <button class="button" @click="validatePassword">Valider</button>
      </div>
    </div>
    <div class="code__valid" v-if="codeValid">
      <h1>🥳🥳 TROP FACILE 🥳🥳</h1>
      <h3>Bonne dégustation!</h3>
    </div>
    <div class="code__invalid" v-if="codeInvalid">
      <h1>🤦‍♀️🤦‍♀️🤦‍♀️🤦‍♀️</h1>
      <button class="button" @click="retry">Retour</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "PasswordApp",

  data() {
    return {
      input1: null,
      input2: null,
      input3: null,
      input4: null,
      code: 3116,
      codeValid: false,
      codeInvalid: false,
    };
  },

  computed: {
    enteredCode() {
      return Number(this.input1 + this.input2 + this.input3 + this.input4);
    },

    codeComplete() {
      return (
        this.input1 !== null &&
        this.input2 !== null &&
        this.input3 !== null &&
        this.input !== null
      );
    },
  },

  methods: {
    validatePassword() {
      if (this.codeComplete) {
        this.enteredCode === this.code
          ? (this.codeValid = true)
          : (this.codeInvalid = true);
      }
    },

    retry() {
      this.codeInvalid = false;
      this.input1 = null;
      this.input2 = null;
      this.input3 = null;
      this.input4 = null;
    },

    goToNext() {
      if (event.target.value !== "") {
        event.target.nextElementSibling.focus();
      }
    },
  },
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #fff;
}

body {
  background-color: #5b8c5a;
}

.button {
  background-color: #fff;
  border-radius: 5px;
  border: none;
  height: 40px;
  width: 100px;
  text-align: center;
  text-transform: uppercase;
  font-weight: bold;
}

.wrapper {
  margin: 30px 10px;
  h1 {
    margin-top: 0;
  }
  .input__wrapper {
    margin: 30px 0;
  }
  .input {
    width: 50px;
    height: 50px;
    margin: 0 10px;
    border-radius: 5px;
    border: none;
    font-size: 40px;
    text-align: center;

    &:focus {
      outline: none;
    }
  }

  .validate__wrapper {
    margin-top: 20px;
  }
}

.code__valid,
.code__invalid {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  z-index: 9999;
  background-color: #5b8c5a;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;

  h1 {
    margin-bottom: 0;
  }

  h3 {
    margin-top: 0;
  }

  .button {
    margin-top: 30px;
  }
}
</style>
