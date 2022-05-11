
<template>
<KeepAlive>
  <div class="container d-flex justify-content-center">
    <p>{{ $store.state.count}}</p>
    <form
      action=""
      @submit="validateBeforeSubmit"
      class="d-flex flex-column w-50"
    >
      <label for="fn">Full name</label>
      <input
        type="text"
        name=""
        id="fn"
        class="form-control p-1 mb-2"
        v-model="typedUsername"
      />
      <label for="email">E-mail</label>
      <input
        type="email"
        name=""
        id="email"
        class="form-control p-1 mb-2"
        v-model="typedEmail"
      />
      <label for="pw">Password</label>
      <input
        type="password"
        name=""
        id="pw"
        class="form-control p-1 mb-2"
        v-model="typedPassword"
      />
      <label for="cp">Confirm password</label>
      <input type="password" name="" id="cp" class="form-control p-1 mb-2" />
      <label for="cc">CC</label>
      <input type="text" name="" id="cc" class="form-control p-1 mb-2" />
      <input
        type="submit"
        value="Sign up"
        class="btn btn-outline-success w-25"
      />
      {{ this.error }}
    </form>
    
  </div>
  </KeepAlive>
</template>


<script>
export default {
  data() {
    return {
      typedUsername: "",
      typedPassword: "",
      typedEmail: "",
      invalid: "",
      error: "",
      valid: true,
      users: [
        {
          name: "hello",
          email: "world@gmail.com",
        },
        {
          name: "second",
          email: "second@gmail.com",
        },
      ],
    };
  },
  watch:{
    typedUsername(newval,oldval){
      this.valid = true;
    },
    typedEmail(newval,oldval){
      this.valid = true;
    },
  },
  methods: {
    validate() {
     this.users.forEach(element=>{
       if(element.name === this.typedUsername){
         this.valid = false
          this.error="Name is taken"
         
       }else if(element.email === this.typedEmail){
          this.valid = false
         this.error="Email is taken"
       }
     })
    },

    validateBeforeSubmit(e) {
      this.validate()
      if (!this.valid) {
        e.preventDefault();
        console.log("prevented");
      } else {
      }
    },
  },
};
</script>