<template>
  <div id="app">
    <div class="input--group">
      <input
        :value="str"
        @input="onInput"
        @blur="onBlur"
        type="text"
        :maxlength="maxChars"
      />
      <p v-show="err" class="input--group--alert">Invalid Time</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      maxChars: 5,
      str: "",
      err: false,
      regex: new RegExp(/^[0-1]{1}[0-9]{1}|[0-2]{1}[0-4]{1}:[0-5]{1}[0-9]{1}$/),
    };
  },
  methods: {
    onInput(e) {
      this.str = e.target.value;
      if (this.str.length === 2 && e.inputType !== "deleteContentBackward") {
        this.str += ":";
      }
    },
    onBlur(e) {
      if (this.str.length < this.maxChars) {
        this.str = this.str.padEnd(this.maxChars, "0");
      }
    },
  },
  watch: {
    str(v) {
      this.err = !this.regex.test(v.toString());
    },
  },
};
</script>

<style>
body {
  display: grid;
  place-items: center;
  height: 100vh;
}

input {
  border: none;
  outline: none;
  border-radius: 20px;
  padding: 20px;
  height: 50px;
  width: 100px;
  text-align: center;
  font-size: 30px;
  box-shadow: 0px 0px 2px 1px lightgray;
}
.input--group {
  position: relative;
}
.input--group--alert {
  position: absolute;
  bottom: -50px;
  left: 0;
  border-left: 5px solid darkred;
  background: gray;
  color: white;
  font-size: 16px;
  transition: bottom 1s;
}
</style>
