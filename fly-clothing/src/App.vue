<template>
  <transition name="fade">
    <sidebar
      v-if="showSidebar"
      :cart="cart"
      :cartIsEmpty="cartIsEmpty"
      :total="total"
      :removeFromCart="removeFromCart"
    />
  </transition>
  <div style="background-color:rgb(255, 222, 222);">
  <div class="container-md" style="background-color:rgb(255, 222, 222);position: relative">
    <nav
      class="
        navbar navbar-light navbar-expand-md
        d-flex
        justify-content-between
        w-100
        mainnav
      "
      style="background-color:rgb(255, 222, 222);"
    >
      <router-link
        to="/#"
        class="navbar-brand text-dark fw-bolder d-flex align-items-center"
      >
        <img
          src="./assets/logo.png"
          width="60"
          class="d-inline-block align-top me-3"
          alt=""
        />
        SneakerLab
      </router-link>

      <button
        class="navbar-toggler"
        type="button"
        data-bs-toggle="collapse"
        data-bs-target="#navbarNavDropdown"
        aria-controls="navbarNavDropdown"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>
      <div
        class="collapse navbar-collapse g-5 justify-content-end"
        id="navbarNavDropdown"
      >
        <ul class="navbar-nav">
          <li class="nav-item">
            <button
              class="text-success cart-btn"
              style="font-size: 1.6rem; border: none; background-color:rgb(255, 222, 222);"
              @click="toggleSidebar"
            >
              <i class="bi bi-cart2"></i>
            </button>
          </li>
          <li class="nav-item">
            <router-link to="/" class="nav-link active" aria-current="page"
              >Home</router-link
            >
          </li>
          <li class="nav-item">
            <router-link to="/products" class="nav-link"
              >Our Products</router-link
            >
          </li>
        </ul>
      </div>
    </nav>
  </div>
  </div>
  <router-view :productsList="products" :add="addToCart" />
  <footer class="p-5">
    <div class="container">
      <div>
        <h5>Navigate</h5>
        <ul>
          <li><a href="">Home</a></li>
          <li><a href="">Products</a></li>
          <li><a href="">Contacts</a></li>
        </ul>
      </div>
       <div>
        <h5>Get help</h5>
        <ul>
          <li><a href="">Terms and conditions</a></li>
          <li><a href="">Privacy policy</a></li>
        </ul>
      </div>
      <div class="d-flex icons">
        <a href=""><i class="bi bi-instagram"></i></a>
        <a href=""><i class="bi bi-facebook"></i></a>
        <a href=""><i class="bi bi-youtube"></i></a>
        <a href=""><i class="bi bi-twitter"></i></a>

      </div>
    </div>
  </footer>
</template>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Poppins:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;0,800;0,900;1,100;1,200;1,300;1,400;1,500;1,600;1,700;1,800;1,900&display=swap");
// body{
//   background-color: rgb(217, 237, 245);

// }
footer {
  background: rgb(255, 222, 222);
border-top: 1px solid white;  .icons{
    flex-wrap: wrap;
    max-width: 100px;
    height: fit-content;
    i{
      color:red;
      font-size: 2rem;
      margin:0 8px;
    }
   
  }
  &>div{
    display: flex;
    justify-content: space-around;
  }
  h5{
    // text-decoration: underline;
    color:red;
    padding-left: 5px;
    border-left:1px solid red;
    margin-bottom:25px;
  }
  ul{
    list-style-type: none;
    padding: 0;
    li a {
      color: black;
      text-decoration: none;
      margin-bottom: 8px;
      display: block;
    }
  }
}
* {
  font-family: "Poppins", sans-serif;
}
.cart-btn:hover {
  background-color: #198754 !important;
  color: white !important;
}
.cart-btn {
  border-radius: 3px;
  transition: 0.2s ease;
  &:hover {
    background-color: #198754 !important;
    color: white !important;
  }
}
.fade-enter-from,
.fade-leave-to {
  transform: translateX(-400px);
}
.fade-enter-to,
.fade-leave-from {
  transform: translateX(0px);
}
.fade-enter-active,
.fade-leave-active {
  transition: transform 0.3s ease;
}
.mainnav {
  height: 50px !important;
}

.card {
  .card-body {
    background-color: rgb(236, 236, 236);
  }
}
</style>
<script>
import sidebar from "./components/sidebar.vue";
import res from "./assets/products.json";
export default {
  components: {
    sidebar,
  },
  data() {
    return {
      products: res,
      showSidebar: false,
      cart: [],
      cartIsEmpty: true,
      total: 0,
    };
  },
  methods: {
    findById(array, id) {
      return array.find((item) => item.id == id);
    },
    findByOrder(array, id) {
      return array.find((item) => item.order == id);
    },
    toggleSidebar() {
      this.showSidebar = !this.showSidebar;
    },
    addToCart(id) {
      let obj = this.findById(this.products, id);
      this.cart.push(obj);
      this.cartIsEmpty = false;
      this.total += obj.price;
      this.cart.forEach((e, i) => {
        e.order = i;
      });
    },
    removeFromCart(id) {
      let removeID = this.findByOrder(this.cart, id);
      this.total -= removeID.price;
      this.cart.splice(id, 1);
      this.cart.forEach((e, i) => {
        e.order = i;
      });
      if (this.cart.length == 0) {
        this.cartIsEmpty = true;
      }
    },
  },
};
</script>
