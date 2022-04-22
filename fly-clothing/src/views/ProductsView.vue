<template>
  <div class="products container">
    <div class="row">
      <div class="col-3" v-for="(card,i) in productsList" key="i">
        <div class="card">
          <img :src="images[i]" class="card-img-top" alt="..." />
          <div class="card-body">
            <h5 class="card-title">Air Jordan 1</h5>
            <a href="#" class="btn btn-primary">Add to cart</a>
          </div>
        </div>
      </div>
      
    </div>
  </div>
</template>


<style lang="scss">
.products {
  background-color: rgb(231, 231, 231) !important;
}
</style>

<script>
import img from '../assets/img/jordangray.jpg'
export default {
  data(){
    return{
      images:[]
    }
  },
  props:['productsList'],
  async mounted(){
          this.productsList.forEach((element,i) => {
            this.images[i] = element.imgsrc
          });
          console.log(img)
  }
}
</script>