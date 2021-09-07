<template>
  <div class="wrapper-content wrapper-content--fixed">
    <section>
      <div class="container">
        <div class="content">
          <search
            :value="search"
            placeholder="Type username..."
            @search="search = $event"
          />
          <button @click="getRepos" class="btn btnPrimary">Search</button>
          <div class="repos" v-if="repos">
            <div class="repos__item" v-for="repo in repos" :key="repo.id">
              <div class="repos__info">
                <a class="link" :href="repo.html_url" target="_blank">{{
                  repo.name
                }}</a>
                <span>{{ repo.stargazers_count }}⭐</span>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
import axios from "axios";
import search from "@/components/Search.vue";

export default {
  components: { search },
  data() {
    return {
      search: "",
      repos: null,
    };
  },
  methods: {
    getRepos() {
      axios
        .get(`https://api.github.com/users/${this.search}/repos`)
        .then((res) => {
          console.log(res.data);
          this.repos = res.data;
        })
        .catch((err) => console.log(err));
    },
  },
};
</script>

<style lang="scss" scoped>
.content {
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-wrap: wrap;
  gap: 32px;
}

.repos {
  display: flex;
  justify-content: space-between;
  flex-wrap: wrap;
  gap: 24px;
  width: 100%;

  &__item {
    width: calc((100% - 24px * 2) / 3);
    padding: 24px;
    border: 1px solid #dbdbdb;
  }

  &__info {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
}
</style>