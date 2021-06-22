<template>
    
   <div class="home" id="viewEdit">
     <Header></Header>
     <b-container class="py-5">

       <b-row class="d-flex justify-content-center">
         <b-col sm="12" lg="4">
           <div class="card shadow-sm border-0  p-4">
           <h2>Detalle de Paciente </h2> 
               <b-form @submit.prevent="editInfo(form)" > 
              <b-form-group
                id="input-group-1"
                label="PacienteId:"
                label-for="input-1"
                description="We'll never share your id with anyone else."
              >
              <b-form-input
                id="input-1"
                v-model="form.pacienteId"
                type="text"
                disabled
         
              ></b-form-input>
            </b-form-group>
            <b-form-group
                id="input-group-1"
                label="Nombre:"
                label-for="input-1"
                
                description="We'll never share your name with anyone else."
              >
              <b-form-input
                id="input-1"
                v-model="form.nombre"
                type="text"
                
                required
              ></b-form-input>
            </b-form-group>
            <b-form-group
                id="input-group-1"
                label="DNI:"
                label-for="input-1"
                description="We'll never share your DNI with anyone else."
              >
              <b-form-input
                id="input-1"
                v-model="form.dni"
                type="text"
                required
                
              ></b-form-input>
            </b-form-group>
            <b-form-group
                id="input-group-1"
                label="Telefono:"
                label-for="input-1"
                description="We'll never share your Telefono with anyone else."
              >
              <b-form-input
                id="input-1"
                v-model="form.telefono"
                type="text"
                required
                
              ></b-form-input>
            </b-form-group>
            <b-form-group
                id="input-group-1"
                label="Correo:"
                label-for="input-1"
                description="We'll never share your Correo with anyone else."
              >
              <b-form-input
                id="input-1"
                v-model="form.correo"
                type="email"
                required
                
              ></b-form-input>
            </b-form-group>
            <b-form-group
                id="input-group-1"
                label="Genero:"
                label-for="input-1"
                description="We'll never share your Genero with anyone else."
              >
              <b-form-input
                id="input-1"
                v-model="form.genero"
                type="text"
                required
                
              ></b-form-input>
            </b-form-group>
            <b-form-group
                id="input-group-1"
                label="Direccion:"
                label-for="input-1"
                description="We'll never share your Direccion with anyone else."
              >
              <b-form-input
                id="input-1"
                v-model="form.direccion"
                type="text"
                required
                
              ></b-form-input>
            </b-form-group>
            <b-form-group
                id="input-group-1"
                label="Fecha de Nacimiento:"
                label-for="input-1"
                description="We'll never share your Fecha de Nacimiento with anyone else."
              >
              <b-form-input
                id="input-1"
                v-model="form.fechaNacimiento"
                type="text"
                required
                
              ></b-form-input>
            </b-form-group>
            
                 <b-button type="submit" variant="primary">Submit</b-button>

                 <router-link  class="btn btn-success" to="/Dashboard">Cancelar</router-link>

              </b-form>
          </div>
           <b-button type="button" variant="danger" @click="deleteE()">Delete</b-button>
         </b-col>
       </b-row>
     </b-container>
     <Footer></Footer>
  </div>
             
 
</template>

<script>
import Header from "@/components/Header.vue"
import Footer from "@/components/Footer.vue"
export default {
name:'Edit',
component: {
  Header,
  Footer
},
data() {
  return {
    pacienteId: null,
     form:{
          "pacienteId":"",
          "nombre" : "",
          "direccion": "", 
          "dni" : "",
          "correo":"",
          "codigoPostal" :"",
          "genero" : "",
          "telefono" : "",
          "fechaNacimiento" : "",
          "token" : "" 
        }
  }
},
methods: {
   editInfo(){
          
         
           
         this.axios.put('https://api.solodata.es/pacientes?id='+this.form.pacienteId, this.form)
        .then(response => {
              console.log(response)
             this.$router.push('/Dashboard');
        })
        .catch(error => {
          console.log(error)
        })
      },
      getInfo()  {
        this.axios.get('https://api.solodata.es/pacientes?id='+ this.$route.params.id) 
          .then(response => {
              console.log(response);
               this.form.pacienteId = this.$route.params.id;
               this.form.nombre = response.data[0].Nombre;
              this.form.direccion = response.data[0].Direccion;
              this.form.dni = response.data[0].DNI;
              this.form.correo = response.data[0].Correo;
              this.form.codigoPostal = response.data[0].CodigoPostal;
              this.form.genero = response.data[0].Genero;
              this.form.telefono = response.data[0].Telefono;
              this.form.fechaNacimiento = response.data[0].FechaNacimiento;
              this.form.token = localStorage.getItem("token");
        console.log(this.form);
              console.log(this.form);

          })
          .catch(error => {
            console.log(error);
          })
        
      },
      deleteE(){
          var form =  {

            "pacienteId": this.form.pacienteId,
            "token": this.form.token
          };
        
          this.axios.delete('https://api.solodata.es/pacientes' ,{ headers : form})
          .then(response=>{
            console.log(response)
              this.$router.push('/Dashboard');
          })
          .catch(error=>error)
          
      }
},
mounted() {
  this.getInfo();
},

}
</script>

<style>

</style>