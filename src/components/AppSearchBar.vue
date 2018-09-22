<template>
  <div class="search">
    <input type="input" class="search__input" @keypress="onKeyPress"  @keyup="alertIfEmpty" v-model.trim="input">
    <button class="search__button" @click="onButtonClick">Search</button>
  </div>
</template>

<script>
export default {
  name: "SearchBar",
  data() {
    return {
      input: ""
    };
  },
  methods: {
    onButtonClick() {
      this.searchRepo();
    },
    // search when user hit enter
    onKeyPress(e) {
      if (e.which === 13) {
        this.searchRepo();
      }
    },
    // alert parent to search
    searchRepo() {
      this.$emit("searching", this.input);
    },
    // alert parent input field is empty
    alertIfEmpty() {
      if (!this.input.length > 0) {
        this.$emit("emptyInputField");
      }
    }
  }
};
</script>

<style lang="scss" scoped>
@import "../scss/colour.scss";
@import "../scss/mixin.scss";
.search {
  display: flex;
  width: 88%;
  margin-top: 2.5rem;
  margin-bottom: 1rem;
  height: 3rem;
  & * {
    border-radius: 5px;
    box-sizing: border-box;
    &:focus {
      outline: 0; // get rid of blue focus border
    }
  }
  &__input {
    flex: 2;
    height: 100%;
    padding: 0 10px;
    border: 1.3px solid $grey;
    font-size: 1rem;
    @include hover-supported() {
      transition: border-color 3s ease-out;
      &:hover {
        border-color: $primary-lighter;
      }
    }
  }
  &__button {
    width: 130px;
    height: 100%;
    background-color: $primary;
    color: $white;
    margin-left: 0.7rem;
    border: none;
    font-size: 1rem;
    font-weight: bold;
    @include hover-supported() {
      transition: background-color 0.3s ease-out;
      &:hover {
        background-color: $primary-darker;
      }
    }
  }
}
</style>
