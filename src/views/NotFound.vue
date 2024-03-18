
  <template>
  <div
    class="wrapper"
    style="color: var(--title-color); text-align: center; padding: 60px 0"
  >
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
    <h4>Извините, но такой странички у нас нет.</h4>
    <br />
    <button
      type="button"
      class="btn btn-primary"
      style="background: #39b5ff"
      @click="GoToHome"
    >
      Вернуться на главную
    </button>
  </div>
</template>


<script>
import router from "../router";
export default {
  name: "NotFound",
  methods: {
    GoToHome() {
      router.push("/");
    },
  },
};
</script>