<template>
  <div class="home" id="viewLogin">
     <b-container class="py-5">
       <b-row class="d-flex justify-content-center">
         <b-col sm="12" lg="4">
           <div class="card shadow-sm border-0  p-4">
            <b-form @submit.prevent="singIn" >
              <b-form-group
                id="input-group-1"
                label="Email address:"
                label-for="input-1"
                description="We'll never share your email with anyone else."
              >
              <b-form-input
                id="input-1"
                v-model="email"
                type="email"
                placeholder="Enter email"
                required
              ></b-form-input>
            </b-form-group>

            <b-form-group id="input-group-2" label="Your Password:"  class="mb-5" label-for="input-2">
              <b-form-input
                id="input-2"
                type="password"
                v-model="password"
                placeholder="Enter name"
                required
              ></b-form-input>
            </b-form-group>

                <b-button type="submit" variant="primary">Submit</b-button>

              </b-form>
              <b-card class="mt-3" header="Form Data Result">
                <pre class="m-0">{{ form }}</pre>
                <pre class="m-1" v-show="error">{{error}}</pre>
              </b-card>
          </div>
         </b-col>
       </b-row>
     </b-container>
  </div>
</template>

<script>


export default {
  name: 'Home',
  components: {
  
  },
  data() {
    return {
      email: "",
      password: "",
      error: false,
      message: ""
    }
  },

  methods: {
    singIn() {
        let json = {
          'usuario': this.email,
          'password': this.password,
        }
        
        this.axios.post(`https://api.solodata.es/auth`, json)
        .then(data => {
          console.log(data)
          if(data.data.status == "ok") {
              localStorage.token = data.data.result.token;
               this.$router.push('dashboard');
          }
        }).catch(error => {
             this.error=true;
             console.log(error);
            this.message = error.message
        })
        
    },
  
  },
  created() {
  
  },
}
</script>

<style lang="scss" >
  
</style>
