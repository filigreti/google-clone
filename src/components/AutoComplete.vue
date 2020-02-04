<template>
  <main ref="auto">
    <div v-for="item in searched.slice(0,10)" :key="item.id">
      <img class="icon" src="@/assets/search.svg" alt />
      <div @click="navigate(item)" class="auto-space">{{ item.name}}</div>
    </div>
  </main>
</template>

<script>
export default {
  props: ["searched", "search"],
  watch: {
    searched: {
      immediate: true,
      handler(x) {
        if (x.length == 0) {
          this.$emit("checkValue", false);
        }
      }
    }
  },
  methods: {
    navigate(x) {
      this.$router.push({
        name: "view",
        params: {
          data: x,
          searched: x.name,
          clicked: true
        }
      });
    }
  },
  mounted() {
    this.$refs.auto.focus();
  }
};
</script>

<style>
.auto-space {
  padding-left: 50px;
  margin-top: 9px;
  font-size: 14px;
}
</style>