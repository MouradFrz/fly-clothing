<template>
  <div class="products container-md">
    <div class="row g-4">
      <div class="col-12 col-sm-6 col-md-4 col-lg-3" v-for="(card,i) in productsList" key="i">
        <div class="card justify-content-between">
          <img :src="images[i]" class="card-img-top" alt="..." />
          <div class="card-body">
            <h5 class="card-title">Air Jordan 1</h5>
            <h5 class="card-title">Color:{{card.color}}</h5>
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
.card{
  height: 100%;
}
.card-body{
  flex:0 !important;
}
</style>

<script>
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
  }
}
</script>