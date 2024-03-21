<template>
  <div class="footer">
    <div class="container">
      <footer class="py-5" style="padding-bottom: 1rem !important">
        <div class="row">
          <div class="col-md-5 links footer_block">
            <img src="../assets/logo.webp" height="50 px" width="160px" />
            <br />

            <p>
              No. 1 в мире Гейминга в России, Геймерские ПК  и профессиональные,
              рабочие станции, аксессуары  и компоненты, низкие цены.
               Тел:

              <br />+7 (812) 123 45 67 <br /> +7 (812) 765 43 21
            </p>
          </div>

          <div class="col">
            <h5>Разделы</h5>
            <ul class="nav flex-column">
              <li class="nav-item mb-2">
                <a href="#" class="nav-link p-0 text-muted">Главная</a>
              </li>
              <li class="nav-item mb-2">
                <a href="Features" class="nav-link p-0 text-muted">Услуги</a>
              </li>
              <li class="nav-item mb-2">
                <a href="Blog" class="nav-link p-0 text-muted">Блог</a>
              </li>
              <li class="nav-item mb-2">
                <a href="FAQs" class="nav-link p-0 text-muted">FAQs</a>
              </li>
              <li class="nav-item mb-2">
                <a href="bout" class="nav-link p-0 text-muted">О нас</a>
              </li>
            </ul>
          </div>

          <div class="col">
            <form>
              <h5>Подпишитесь на рассылку</h5>
              <p>Ежемесячные актуальные новости из диджитал мира от нас.</p>
              <div class="d-flex flex-column flex-sm-row w-100 gap-2">
                <label for="newsletter1" class="visually-hidden"
                  >Email адрес</label
                >
                <input
                  id="newsletter1"
                  type="text"
                  class="form-control"
                  placeholder="Email адрес"
                />
                <button
                  class="btn btn-primary"
                  type="button"
                  style="height: 38px; background-color: #39b5ff"
                >
                  Подпишись
                </button>
              </div>
            </form>
          </div>
        </div>

        <div
          class="
            d-flex
            flex-column flex-sm-row
            justify-content-between
            py-4
            my-4
            border-top
          "
        >
          <p style="padding-left: 35%">
            &copy; 2024 Gamdig, Inc. Все права защищены.
          </p>
        </div>
      </footer>
    </div>
  </div>
</template>
<script>
export default {
  name: "FooterView",
};
</script>
<style>
.footer {
  background: #f4f5f6;
}
.py-5 {
  padding-top: 4rem !important;
  padding-bottom: 0rem !important;
}
</style>