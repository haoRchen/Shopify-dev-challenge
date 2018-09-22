<template>
  <table class="table">
    <tr>
      <th>Name</th>
      <th>Language</th>
      <th>Latest Tag</th>
      <th></th>
    </tr>
    <tr v-for="item in repo" :key="item.name">
      <td ><a class="repo" :href="item.url">{{item.name}}</a></td>
      <td>{{item.language}}</td>
      <td>{{item.releaseTag}}</td>
      <td><a href="#" @click="onButtonClick(item.id)">{{!isFavorite? (item.favorited? "" : "Add") : "Remove"}}</a></td>
    </tr>
  </table>
</template>

<script>
export default {
  name: "AppTable",
  props: {
    isFavorite: {
      type: Boolean,
      require: false,
      default: false
    },
    repo: {
      type: Array,
      required: false,
      default: () => []
    }
  },
  methods: {
    onButtonClick(id) {
      this.$emit("rowClicked", id, this.isFavorite);
    }
  }
};
</script>

<style lang="scss" scoped>
@import "../scss/colour.scss";
.table {
  overflow-x: auto;
  width: 90%;
  margin: 2rem 0;
  & th,
  & td {
    text-align: left;
    padding: 5px;
    width: 33.3%;
  }
}
.repo {
  color: $black;
}
</style>
