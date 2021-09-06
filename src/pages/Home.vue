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
        </div>
      </div>
    </section>
  </div>
</template>

<script>
import search from "@/components/Search.vue";

export default {
  components: { search },
  data() {
    return {
      search: "",
    };
  },
  methods: {
    getRepos() {
      console.log(`get user ${this.search} repos`);
    },
  },
};
</script>

<style lang="scss" scoped>
.content {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 24px;
}
</style>