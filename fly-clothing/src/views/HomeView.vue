<template>
 <main style="background-color:rgba(113,110,107,255);">
   <div class="wrapper hero d-flex align-items-center ">
     <div class="container ">
       <div class="col-12 col-md-6  ">
         <h1 class="text-light fs-1 " >Your go to Sneaker shop!</h1>
         <p class="text-light ">We have the absolute best collection of sneakers on the market with the best prices !</p>
         <div class="btn btn-outline-danger ">Shop Now !</div>
       </div>
     </div>
   </div>
   <div class="cards  container g-5" >
     <h1 class="text-center text-light m-5">Trending sneakers</h1>
     <div class="d-flex">
              <div class="row w-100">
                <div
                  class="col-12 col-sm-6 col-md-4 col-lg-4"
                  v-for="(card, i) in productsList.slice(0,3)"
                  key="i"
                >
                  <div class="card justify-content-between">
                    <img :src="card.imgsrc" class="card-img-top" style="margin:auto;" alt="..." />
                    <div class="card-body">
                      <h5 class="card-title text-dark">{{ card.brand }} {{ card.model }}</h5>
                      <h6 class="card-titl text-muted fw-light">
                        Color: {{ card.color }}
                      </h6>
                      <h6 class="card-titl text-muted">Price: ${{ card.price }}</h6>
                      <button class="btn btn-success" @click="add(card.id)" >Add to cart</button>
                    </div>
                  </div>
                </div>
                </div>
                </div>
   </div>
 </main>
</template>

<script>


export default {
props: ["productsList","add"],
}
</script>
<style lang="scss" scoped>
*{
  box-sizing: border-box !important;
}
  .hero{
    background-image: url("../assets/img/banner.webp");
    background-size: cover;
    width: 100%;
    height: 660px;
    
  }
  main{
    padding-bottom: 140px !important;
  }
  .card {
  height: 100%;
  border-bottom:1px solid rgb(255, 255, 255) !important; 
  
}
.card-body {
  flex: 0 !important;
  border: none !important;
 border-top: 1px solid rgb(255, 0, 0) !important;
}
</style>