<template>
<transition name="fade"> 
<sidebar v-if="showSidebar" :cart="cart" :cartIsEmpty="cartIsEmpty" :total="total" :removeFromCart="removeFromCart" />
</transition>
  <div class="container-md" style="position:relative;">
    
    <nav class="navbar navbar-light  navbar-expand-md d-flex justify-content-between w-100 mainnav">
      <router-link to="/#" class="navbar-brand text-dark fw-bolder d-flex align-items-center">
        <img
          src="./assets/logo.png"
          width="30"
          class="d-inline-block align-top me-3"
          alt=""
        />
        SneakerLab
      </router-link>

      <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNavDropdown" aria-controls="navbarNavDropdown" aria-expanded="false" aria-label="Toggle navigation">
      <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse g-5 justify-content-end" id="navbarNavDropdown">
      <ul class="navbar-nav">
        <li class="nav-item">
          <button class="text-success cart-btn" style="font-size:1.6rem;border:none;background-color: white;" @click="toggleSidebar"><i class="bi bi-cart2"></i></button>
        </li>
        <li class="nav-item">
          <router-link to="/" class="nav-link active" aria-current="page" >Home</router-link>
        </li>
        <li class="nav-item">
          <router-link to="/products" class="nav-link" >Our Products</router-link>
        </li>
        <li class="nav-item">
          <router-link to="/login" class="nav-link btn btn-outline-danger" >Login</router-link>
        </li>
        <li class="nav-item">
          <router-link to="/signup" class="nav-link btn btn-danger ms-2 text-light " >Sign Up</router-link>
        </li>
        
      </ul>
    </div>
    </nav>
  </div>
  <router-view :productsList="products"  :add="addToCart"/>
</template>

<style lang="scss">
body{
  background-color: rgb(217, 237, 245);
}
.cart-btn:hover{
  background-color: #198754 !important;
  color:white !important; 
}
.cart-btn{
  border-radius: 3px;
  transition: 0.2s ease;
  &:hover{
  background-color: #198754 !important;
  color:white !important; 
}
}
.fade-enter-from,.fade-leave-to{
  transform:translateX(-400px);
}
.fade-enter-to,.fade-leave-from{
  transform:translateX(0px);
}
.fade-enter-active,.fade-leave-active{
  transition : transform 0.3s ease;
}
.mainnav{
   height: 70px !important;
}

.card{
  .card-body{
    background-color: rgb(236, 236, 236);
  }
}
</style>
<script>
import sidebar from './components/sidebar.vue';
import res from './assets/products.json';
export default {
  components:{
    sidebar,
  },
  data(){
    return{
      products:res,
          showSidebar:false,
          cart:[],
          cartIsEmpty:true,
          total:0
    }
  },
  methods:{
    findById(array,id){
      return array.find(item=>item.id == id)
    },
     findByOrder(array,id){
      return array.find(item=>item.order == id)
    },
    toggleSidebar(){
      this.showSidebar = !this.showSidebar;
    },
    addToCart(id){
      let obj = this.findById(this.products,id)
      this.cart.push(obj)
      this.cartIsEmpty=false;
      this.total+=obj.price
      this.cart.forEach((e,i)=>{
        e.order=i;
      });
    },
    removeFromCart(id){
      let removeID = this.findByOrder(this.cart,id)
      this.total-=removeID.price;
      this.cart.splice(id,1);
      this.cart.forEach((e,i)=>{
        e.order=i;
      });
      if(this.cart.length==0){
        this.cartIsEmpty=true;
      }
    }
  }
}
</script>
