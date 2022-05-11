<template>
  <div class="sidebar">
      <p v-if="cartIsEmpty" style="padding:40px">Your cart is empty</p>
      <span v-if="!cartIsEmpty" class="cart-element">
          <h6 style="margin-right:auto;white-space:nowrap;">Model</h6>
            <h6>Color</h6>
            <h6>Price</h6>
            <span style="width:50px;"></span>
          </span>   
      <div v-for="(element,i) in cart" key="i"  >
          <span v-if="element" class="cart-element">
          <p style="margin-right:auto;white-space:nowrap;">{{ element.model }}</p>
            <p>{{ element.color }}</p>
            <p>${{element.price }}</p>
          <button class="btn btn-danger fw-bolder px-3 py-0" @click="removeFromCart(element.order)"><i class="bi bi-trash-fill"></i></button>
          </span>   
      </div>
      <p class="checkout text-success">Total : ${{ total }}</p>
      <button class="btn btn-success checkout">Checkout</button>
  </div>
</template>

<script>
export default {
props:['cart','cartIsEmpty','total','removeFromCart'],


}

</script>

<style lang="scss">
.checkout{
    align-self: flex-end;
    margin-top: 18px;
}
    .sidebar{
        height:100vh;
        position: fixed;
        width: 400px;
        border-right: 1px solid red;
        background-color: white;
        z-index: 300;
        display: flex;
        flex-direction: column;
        overflow-y: scroll;
        }
    .cart-element{
        display: flex;
        // gap: 40px;
        width: 100%;
        // justify-content: flex-end;
        // align-items: center;
        padding: 15px;
        margin: 10px;
        border-bottom: 2px solid rgb(219, 219, 219);
        transition: all 0.3 ease;
        p,h6{  min-width: 25%;
            max-width: 25%;
            text-align: left;
            margin: 0;
        }
    }
</style>