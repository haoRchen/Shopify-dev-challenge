<template>
  <div class="content">
    <div class="content__title">
      <h1 class="title__text">My Github Favorites</h1>
    </div>
    <div class="content__data ">
      <!-- Column for displaying the table for fetched results -->
      <div class="content__results">
        <app-search-bar @searching="findRepositories" @emptyInputField="clearRepositories"/>
        <app-table :repo="repositories" @rowClicked="updateRow"/>
      </div>
      <!-- Column for displaying the table for favorited repository -->
      <div class="content__favorites">
        <app-table :isFavorite="true" :repo="favoriteRepositories" @rowClicked="updateRow"/>
      </div>
    </div>
  </div>
</template>

<script>
import AppTable from "./AppTable";
import AppSearchBar from "./AppSearchBar";

export default {
  name: "MainPage",
  data() {
    return {
      api: "https://api.github.com/search/repositories?q=",
      repositories: [],
      favoriteRepositories: []
    };
  },
  components: {
    AppTable,
    AppSearchBar
  },
  methods: {
    // grab the first 10 Github repository matching the search value
    findRepositories(searchValue) {
      this.clearRepositories();
      this.$http.get(this.api + searchValue).then(response => {
        const repo = response.data.items.slice(0, 10);
        this.parseData(repo);
      });
    },
    // strip the desired properties of a Github repository
    parseData(repo) {
      for (const item of repo) {
        this.$http.get(item.tags_url).then(response => {
          this.repositories.push({
            id: item.id,
            name: item.full_name,
            repoUrl: item.html_url,
            language: item.language,
            releaseTag: response.data.length == 0 ? "-" : response.data[0].name,
            favorited: false
          });
        });
      }
    },
    // Add/remove from row if favorited
    updateRow(id, isFavorite) {
      if (isFavorite) {
        let repo = this.repositories.find(x => x.id === id);
        if (repo.favorited) {
          repo.favorited = false;
          this.favoriteRepositories.splice(
            this.favoriteRepositories.indexOf(repo),
            1
          );
        }
      } else {
        let repo = this.repositories.find(x => x.id === id);
        if (!repo.favorited) {
          repo.favorited = true;
          this.favoriteRepositories.push(repo);
        }
      }
    },
    clearRepositories() {
      this.repositories = [];
      this.favoriteRepositories = [];
    }
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
