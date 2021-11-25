<template>
  <div class="dashboard-container">
    <div class="dashboard-text">name: {{ name }}</div>
    <valid-code :value.sync="validCode" />
  </div>
</template>

<script>
import { mapGetters } from "vuex";
import validCode from "@/components/Code/validCode.vue";

export default {
  name: "Dashboard",
  components: { validCode },
  data() {
    return {
      validCode: false
    }
  },
  computed: {
    ...mapGetters(["name"]),
  },
};
</script>

<style lang="scss" scoped>
.dashboard {
  &-container {
    margin: 30px;
  }
  &-text {
    font-size: 30px;
    line-height: 46px;
  }
}
</style>
