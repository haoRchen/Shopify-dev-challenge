<template>
  <div class="content">
    <div class="content__title">
      <h1 class="title__text">My Github Favorites</h1>
    </div>
    <div class="content__data ">
      <!-- Column for displaying the table for fetched results -->
      <div class="content__results">
        <app-search-bar/>
        <app-table/>
      </div>
      <!-- Column for displaying the table for favorited repository -->
      <div class="content__favorites">
        <app-table/>
      </div>
    </div>
  </div>
</template>

<script>
import AppTable from "./AppTable";
import AppSearchBar from "./AppSearchBar";

export default {
  name: "MainPage",
  components: {
    AppTable,
    AppSearchBar
  }
};
</script>

<style lang="scss" scoped>
@import "../scss/colour.scss";
@import "../scss/mixin.scss";
.content {
  display: flex;
  flex-direction: column;
  height: 100%;
  min-height: 100vh;
  overflow: auto;
  &__title {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 100%;
    height: 8rem;
    background-color: $primary;
    color: $white;
  }
  &__data {
    display: flex;
    flex-direction: column;
    flex: 1;
    height: 100%;
    @include tablet {
      flex-direction: row;
    }
  }
  &__results,
  &__favorites {
    flex: 1;
    display: flex;
    flex-direction: column;
    justify-content: flex-start;
    align-items: center;
    padding-top: 1rem;
    padding-bottom: 2rem;
  }
  &__results {
    background-color: $white;
  }
  &__favorites {
    background-color: $secondary;
  }
}
</style>
