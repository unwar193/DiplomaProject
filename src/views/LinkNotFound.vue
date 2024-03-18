<template>
  <div style="color: var(--title-color); text-align: center; padding: 60px 0">
    <h2
      style="
        font-size: 160px;
        color: var(--title-color);
        line-height: 1;
        margin: 0 0 25px;
      "
    >
      404
    </h2>
    <div></div>
    <h4>Извините, но такой искомой страницы на нашем сайте не существует.</h4>
    <br />
    <button
      type="button"
      class="btn btn-primary"
      style="background: #39b5ff"
      @click="GoToHome"
    >
      На главную
    </button>
  </div>
</template>
<script>
import router from "../router";
export default {
  name: "LinkNotFound",
  methods: {
    GoToHome() {
      router.push("/");
    },
  },
};
</script>
