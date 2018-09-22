<template>
  <table class="table">
    <tr>
      <th>Name</th>
      <th>Language</th>
      <th>Latest Tag</th>
      <th></th>
    </tr>
    <tr v-for="item in repo" :key="item.name">
      <td><a :href="item.url">{{item.name}}</a></td>
      <td>{{item.language}}</td>
      <td>{{item.releaseTag}}</td>
      <td><a href="">Add</a></td>
    </tr>
  </table>
</template>

<script>
export default {
  name: "AppTable",
  props: {
    repo: {
      type: Array,
      required: false,
      default: () => []
    }
  }
};
</script>

<style lang="scss" scoped>
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
</style>
