<template>
  <div class="vh-100 d-flex justify-content-center align-items-center" style="background: rgb(57 181 255)">
    <div class="container">
      <div class="row d-flex justify-content-center">
        <div class="col-12 col-md-8 col-lg-6">
          <div class="card bg-white">
            <div class="card-body p-5">
              <form class="mb-3 mt-md-4" @submit.prevent="signupUser">
                <h2 class="fw-bold mb-2 text-uppercase" style="margin-left: 116px">
                  Присоединяйтесь!
                </h2>
                <!-- <p class="mb-5">Please enter your login and password!</p> -->
                <div class="mb-3">
                  <label for="exampleInputEmail1" class="form-label">Имя</label>
                  <input type="name" class="form-control" aria-describedby="emailHelp" placeholder="Ваше имя"
                    v-model="user.name" />
                </div>
                <div class="mb-3">
                  <label for="email" class="form-label">Email адрес</label>
                  <input type="email" class="form-control" id="email" placeholder="name@example.com"
                    v-model="user.email" />
                </div>
                <div class="mb-3">
                  <label for="password" class="form-label">Пароль</label>
                  <input type="password" class="form-control" id="password" placeholder="*******"
                    v-model="user.password" />
                </div>
                <div class="mb-3">
                  <label for="adress" class="form-label">Адрес доставки</label>
                  <input type="address" class="form-control" aria-describedby="emailHelp"
                    placeholder="например: Беларусь, Минск, 765" v-model="user.address" />
                </div>
                <div class="form-outline">
                  <label class="form-label" for="typePhone">Номер телефона</label>
                  <input type="tel" id="typePhone" class="form-control" placeholder="Например: +7 (999) 111-22-33"
                    v-model="user.number" />
                </div>

                <div class="d-grid">
                  <br />
                  <button class="btn btn-outline-dark" type="submit">
                    Логин
                  </button>
                </div>
              </form>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import "../Firebase";
import { getAuth, createUserWithEmailAndPassword } from "firebase/auth";
import { getFirestore, collection, addDoc } from "firebase/firestore";
const auth = getAuth();
const db = getFirestore();
const dbRef = collection(db, "users");
import router from "../router";
export default {
  name: "SignUpView",
  data() {
    return {
      user: {
        name: "",
        email: "",
        address: "",
        password: "",
        number: "",
        uid: "",
      },
    };
  },
  methods: {
    signupUser() {
      createUserWithEmailAndPassword(auth, this.user.email, this.user.password)
        .then((dataUser) => {
          addDoc(dbRef, {
            name: this.user.name,
            email: this.user.email,
            address: this.user.address,
            number: this.user.number,
            uid: dataUser.user.uid,
          });
          localStorage.setItem("uidUser", dataUser.user.uid);
          if (this.$store.state.count > 0) {
            router.push("/cart");
          } else {
            router.push("/products");
          }
        })
        .catch((error) => {
          console.log(error);
        });
    },
  },
};
</script>

<style>
.mt-md-4 {
  margin-top: -0.5rem !important;
}
</style>