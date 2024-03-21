<template>
  <div class="container">
    <br />
    <h1 style="text-align: center">Мои заказы</h1>
    <br />
    <table class="table table-bordered" v-if="orders.length > 0">
      <thead style="background: #39b5ff; color: white">
        <tr>
          <!-- <th scope="col"></th> -->
          <th scope="col">Имя</th>
          <th scope="col">Дата</th>
          <th scope="col">Адресс</th>
          <th scope="col">Номер тел.</th>
          <th scope="col">Товары</th>
          <th scope="col">Действия</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="item in orders" :key="item.name">
          <!-- <th scope="row"></th> -->
          <td class="align-middle">{{ item.name }}</td>
          <td class="align-middle">{{ item.date }}</td>
          <td class="align-middle">{{ item.address }}</td>
          <td class="align-middle">{{ item.number }}</td>
          <td>
            <table class="table mb-0 table-bordered">
              <thead>
                <tr class="table-secondary">
                  <th scope="col">Наименование</th>
                  <th scope="col">Количество</th>
                  <th scope="col">Цена</th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="cartitem in item.cart" :key="cartitem.name">
                  <td>{{ cartitem.name }}</td>
                  <td>{{ cartitem.quantity }}</td>
                  <td>{{ cartitem.totalPrice }} DT</td>
                </tr>
                <tr>
                  <td colspan="2" class="table-active">
                    Всего (Включая доставку)
                  </td>
                  <td>{{ item.total }} DT</td>
                </tr>
              </tbody>
            </table>
          </td>
          <td>
            <div class="d-grid gap-2">
              <button
                type="button"
                @click="
                  GetOrderData(
                    item.name,
                    item.date,
                    item.address,
                    item.number,
                    item.cart,
                    item.key,
                    item.total
                  )
                "
                class="btn btn-success"
                data-bs-toggle="modal"
                data-bs-target="#validation"
              >
                Проверить
              </button>
              <button
                type="button"
                class="btn"
                style="background: red; color: white"
                data-bs-toggle="modal"
                data-bs-target="#delete"
                v-on:click="getDataKey(item.key, item.name)"
              >
                Удалить
              </button>
            </div>
          </td>
        </tr>
      </tbody>
    </table>
    <div
      v-else
      class="row d-flex justify-content-center align-items-center h-100"
    >
      <br />
      <div>
        <center>страница заказа пуста</center>
        <br />
        <br />
        <router-link to="/products">
          <img src="../assets/icons8_back_64px.png" style="height: 37px" />
        </router-link>
        <a style="width: auto"> Продолжить покупки </a>
      </div>
    </div>
    <!-- Modal 3 (delete) -->
    <div
      class="modal fade"
      id="delete"
      data-bs-backdrop="static"
      data-bs-keyboard="false"
      tabindex="-1"
      aria-labelledby="staticBackdropLabel"
      aria-hidden="true"
    >
      <div class="modal-dialog">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title" id="staticBackdropLabel">Удалить заказ</h5>
            <button
              type="button"
              class="btn-close"
              data-bs-dismiss="modal"
              aria-label="Close"
            ></button>
          </div>
          <div class="modal-body">
            .
            <!-- form start here -->
            <form>
              <h3>
                Вы действительно хотите удалить заказ {{ dataProduct.name }} ?
              </h3>
            </form>
            <!-- form end here -->
          </div>
          <div class="modal-footer">
            <button
              type="button"
              id="close"
              class="btn btn-secondary"
              data-bs-dismiss="modal"
            >
              Закрыть
            </button>
            <button
              type="button"
              class="btn"
              style="background: red; color: white"
              v-on:click="RemoveFromCheckout(dataProduct.key)"
            >
              Удалить
            </button>
          </div>
        </div>
      </div>
    </div>
    <!-- fin model -->
    <!-- Modal  (validation) -->
    <div
      class="modal fade"
      id="validation"
      data-bs-backdrop="static"
      data-bs-keyboard="false"
      tabindex="-1"
      aria-labelledby="staticBackdropLabel"
      aria-hidden="true"
    >
      <div class="modal-dialog modal-xl">
        <div class="modal-content" style="border: black">
          <div class="modal-header" style="background: #242121; color: white">
            <h5
              class="modal-title"
              id="staticBackdropLabel"
              style="display: flex; margin: auto"
            >
              Напечатать счёт
            </h5>
          </div>
          <div class="modal-body">
            <!-- form start here -->
            <div class="container" id="printJS-form">
              <div class="col-md-12">
                <div class="invoice">
                  <!-- begin invoice-company -->

                  <div class="row align-items-start">
                    <div class="col">GameDig, Inc</div>
                  </div>
                  <!-- end invoice-company -->
                  <!-- begin invoice-header -->
                  <div class="invoice-header">
                    <div class="invoice-from">
                      <small>из</small>
                      <address class="m-t-5 m-b-5">
                        <strong class="text-inverse">GamDig, Inc.</strong><br />
                        Адресс: Россия, Санкт-Петербург<br />
                        Тел: +7 (812) 123-45-67
                      </address>
                    </div>
                    <div class="invoice-to">
                      <small>to</small>
                      <address class="m-t-5 m-b-5">
                        <strong class="text-inverse">{{
                          productdata.name
                        }}</strong
                        ><br />
                        Адресс: {{ productdata.address }}<br />
                        Тел: +7 (812) {{ productdata.number }}
                      </address>
                    </div>
                    <div class="invoice-date">
                      <small>Счёт / период</small>
                      <div class="date text-inverse m-t-5">
                        {{ productdata.date }}
                      </div>
                      <br />
                      <div class="invoice-detail">Услуги</div>
                    </div>
                  </div>
                  <!-- end invoice-header -->
                  <!-- begin invoice-content -->
                  <div class="invoice-content">
                    <!-- begin table-responsive -->
                    <div class="table-responsive">
                      <table class="table table-invoice">
                        <thead>
                          <tr>
                            <th>Товары</th>
                            <th class="text-center" width="10%">Рейтинг</th>
                            <th class="text-center" width="10%">Количество</th>
                            <th class="text-right" width="20%">Всего</th>
                          </tr>
                        </thead>
                        <tbody>
                          <tr v-for="item in productdata.cart" :key="item.name">
                            <td>
                              <span class="text-inverse">{{ item.name }}</span
                              ><br />
                              <small>{{ item.brand }}</small>
                            </td>
                            <td class="text-center">{{ item.price }} DT</td>
                            <td class="text-center">{{ item.quantity }}</td>
                            <td class="text-right">{{ item.totalPrice }} DT</td>
                          </tr>
                        </tbody>
                      </table>
                    </div>
                    <!-- end table-responsive -->
                    <!-- begin invoice-price -->
                    <div class="invoice-price">
                      <div class="invoice-price-left">
                        <div class="invoice-price-row">
                          <div class="sub-price">
                            <small>Промежуточный итог</small>
                            <span class="text-inverse"
                              >{{ productdata.total - 7 }} DT</span
                            >
                          </div>
                          <div class="sub-price">
                            <i class="fa fa-plus text-muted"></i>
                          </div>
                          <div class="sub-price">
                            <small>Доставка</small>
                            <span class="text-inverse">7 DT</span>
                          </div>
                        </div>
                      </div>
                      <div class="invoice-price-right">
                        <small>Всего</small>
                        <span class="f-w-600">{{ productdata.total }} DT</span>
                      </div>
                    </div>
                    <!-- end invoice-price -->
                  </div>
                  <!-- end invoice-content -->
                  <!-- begin invoice-note -->
                  <div class="invoice-note">
                    * Оформить все чеки, подлежащие оплате GamDig<br />
                    * Оплата производится в течение 30 дней<br />
                    * Если у вас есть какие-либо вопросы относительно этого счета, свяжитесь с
                    support@gamdig.com
                  </div>
                  <!-- end invoice-note -->
                  <!-- begin invoice-footer -->
                  <div class="invoice-footer">
                    <p class="text-center m-b-5 f-w-600">
                      Благодарим, что Вы выбрали нас
                    </p>
                    <p class="text-center">
                      <span class="m-r-10"
                        ><i class="fa fa-fw fa-lg fa-globe"></i>
                        www.gamdig.com</span
                      >
                      <span class="m-r-10"
                        ><i class="fa fa-fw fa-lg fa-phone-volume"></i>
                        T:+7(812) 123-45-67</span
                      >
                      <span class="m-r-10"
                        ><i class="fa fa-fw fa-lg fa-envelope"></i>
                        gamdig@gmail.com</span
                      >
                    </p>
                  </div>
                  <!-- end invoice-footer -->
                </div>
              </div>
            </div>
            <!-- form end here -->
          </div>
          <div class="modal-footer">
            <button
              type="button"
              id="close"
              class="btn btn-secondary"
              data-bs-dismiss="modal"
            >
              Закрыть
            </button>
            <button
              type="button"
              class="btn"
              style="background: red; color: white"
              @click="printinvoice"
            >
              Экспортировать в PDF
            </button>
          </div>
        </div>
      </div>
    </div>
    <!-- fin model -->
  </div>
</template>
<script>
import "../Firebase";

import {
  collection,
  query,
  getFirestore,
  onSnapshot,
  doc,
  deleteDoc,
} from "firebase/firestore";
import printJS from "print-js";
const db = getFirestore();
const q = query(collection(db, "Checkout"));

export default {
  name: "OrdersView",
  data() {
    return {
      orders: [],
      dataProduct: {
        name: "",
        price: 0,
        image: "",
        brand: "",
        description: "",
        key: "",
      },
      productdata: {
        address: "",
        date: "",
        name: "",
        number: "",
        total: "",
        cart: [],
        key: "",
      },
    };
  },
  created() {
    onSnapshot(q, (querySnapshot) => {
      this.orders = [];
      querySnapshot.forEach((doc) => {
        this.orders.push({
          key: doc.id,
          name: doc.data().name,
          address: doc.data().address,
          number: doc.data().number,
          date: doc.data().date,
          total: doc.data().total,
          cart: doc.data().cart,
        });
      });
    });
  },
  methods: {
    getDataKey(key, name) {
      this.dataProduct.key = key;
      this.dataProduct.name = name;
    },

    RemoveFromCheckout(key) {
      deleteDoc(doc(db, "Checkout", key)).then(() => {
        document.getElementById("close").click();
      });
    },
    GetOrderData(name, date, address, number, cart, key, total) {
      this.productdata.name = name;
      this.productdata.date = date;
      this.productdata.address = address;
      this.productdata.number = number;
      this.productdata.cart = cart;
      this.productdata.key = key;
      this.productdata.total = total;
      console.log(this.productdata);
    },
    printinvoice() {
      printJS({
        printable: "printJS-form",
        type: "html",
        targetStyles: ["*"],
        scanStyles: true,
      });
    },
  },
};
</script>
<style>
body {
  background: rgb(255, 255, 255);
}

.invoice {
  background: #fff;
  padding: 20px;
}

.invoice-company {
  font-size: 20px;
}

.invoice-header {
  margin: 0 -20px;
  background: #f0f3f4;
  padding: 20px;
}

.invoice-date,
.invoice-from,
.invoice-to {
  display: table-cell;
  width: 1%;
}

.invoice-from,
.invoice-to {
  padding-right: 20px;
}

.invoice-date .date,
.invoice-from strong,
.invoice-to strong {
  font-size: 16px;
  font-weight: 600;
}

.invoice-date {
  text-align: right;
  padding-left: 20px;
}

.invoice-price {
  background: #f0f3f4;
  display: table;
  width: 100%;
}

.invoice-price .invoice-price-left,
.invoice-price .invoice-price-right {
  display: table-cell;
  padding: 20px;
  font-size: 20px;
  font-weight: 600;
  width: 75%;
  position: relative;
  vertical-align: middle;
}

.invoice-price .invoice-price-left .sub-price {
  display: table-cell;
  vertical-align: middle;
  padding: 0 20px;
}

.invoice-price small {
  font-size: 12px;
  font-weight: 400;
  display: block;
}

.invoice-price .invoice-price-row {
  display: table;
  float: left;
}

.invoice-price .invoice-price-right {
  width: 25%;
  background: #2d353c;
  color: #fff;
  font-size: 28px;
  text-align: right;
  vertical-align: bottom;
  font-weight: 300;
}

.invoice-price .invoice-price-right small {
  display: block;
  opacity: 0.6;
  position: absolute;
  top: 10px;
  left: 10px;
  font-size: 12px;
}

.invoice-footer {
  border-top: 1px solid #ddd;
  padding-top: 10px;
  font-size: 10px;
}

.invoice-note {
  color: #999;
  margin-top: 80px;
  font-size: 85%;
}

.invoice > div:not(.invoice-footer) {
  margin-bottom: 20px;
}

.btn.btn-white,
.btn.btn-white.disabled,
.btn.btn-white.disabled:focus,
.btn.btn-white.disabled:hover,
.btn.btn-white[disabled],
.btn.btn-white[disabled]:focus,
.btn.btn-white[disabled]:hover {
  color: #2d353c;
  background: #fff;
  border-color: #d9dfe3;
}
</style>