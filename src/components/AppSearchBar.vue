<template>
  <div class="search">
    <input type="input" class="search__input">
    <button class="search__button">Search</button>
  </div>
</template>

<script>
export default {
  name: "SearchBar"
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
    @include hover-supported() {
      transition: background-color 0.3s ease-out;
      &:hover {
        background-color: $primary-darker;
      }
    }
  }
}
</style>
