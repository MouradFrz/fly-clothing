<template>
  <!-- <nav>
    <router-link to="/" class="btn btn-primary">Home</router-link> |
    <router-link to="/about">abt</router-link>
  </nav> -->
  <div class="container">
    <nav class="navbar navbar-light  navbar-expand-md d-flex justify-content-between w-100">
      <router-link to="/#" class="navbar-brand text-success d-flex align-items-center">
        <img
          src="./assets/logo.png"
          width="30"
          class="d-inline-block align-top me-3"
          alt=""
        />
        Fly-Clothing
      </router-link>

      <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNavDropdown" aria-controls="navbarNavDropdown" aria-expanded="false" aria-label="Toggle navigation">
      <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse g-5 justify-content-end" id="navbarNavDropdown">
      <ul class="navbar-nav">
        
        <li class="nav-item">
          <router-link to="/" class="nav-link active" aria-current="page" >Home</router-link>
        </li>
        <li class="nav-item">
          <router-link to="/products" class="nav-link" >Our Products</router-link>
        </li>
        <li class="nav-item">
          <router-link to="/login" class="nav-link btn btn-outline-success" >Login</router-link>
        </li>
        <li class="nav-item">
          <router-link to="/signup" class="nav-link btn-success ms-2 rounded" >Sign Up</router-link>
        </li>
      </ul>
    </div>
    </nav>
  </div>
  <router-view />
</template>

<style lang="scss">
nav{
  background-color:rgb(231, 231, 231) !important;
}
</style>
