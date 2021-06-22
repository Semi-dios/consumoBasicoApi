<template>
  <div>
    <Header></Header>
     <b-container class="p-3">
      <b-row class="d-flex justify-content-center">
        <b-col sm="12" lg="10">
          <b-row>
            <b-col>
              <router-link class="btn btn-primary" to="/Nuevo">Nuevo</router-link>
            </b-col>
          </b-row>
        <b-table
          :items="list"
          :fields="fields"
           responsive="sm"
          ref="selectableTable"
          selectable
          @row-selected="onRowSelected"
        >
          <!-- Example scoped slot for select state illustrative purposes -->
          <template #cell(selected)="{ rowSelected }">
            <template v-if="rowSelected">
              <span aria-hidden="true">&check;</span>
              <span class="sr-only">Selected</span>
            </template>
            <template v-else>
              <span aria-hidden="true">&nbsp;</span>
              <span class="sr-only">Not selected</span>
            </template>
          </template>

          <template #cell(actions)="row">
            <b-button size="sm" @click="redEdit(78)" class="mr-1">
              Edit Information
            </b-button>
            <b-button size="sm" @click="row.toggleDetails">
              {{ row.detailsShowing ? 'Hide' : 'Show' }} Details
            </b-button>
          </template>

          <template #row-details="row">
            <b-card>
              <ul>
                <li v-for="(value, key) in row.item" :key="key">{{ key }}: {{ value }}</li>
              </ul>
            </b-card>
          </template>
        </b-table>

      
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
  name:'Dashboard',
  components: {
    Header,
    Footer
  },
    data() {
      return {
        
        fields: ['PacienteId', 'Nombre', 'DNI', 'Telefono', 'Correo','actions'],
        list: null,
        page: '1',
        selected: [],
       
        

      }
    },
    methods: {
      onRowSelected(items) {
        this.selected = items
      },
      selectAllRows() {
        this.$refs.selectableTable.selectAllRows()
      },
      clearSelected() {
        this.$refs.selectableTable.clearSelected()
      },
      selectThirdRow() {
        // Rows are indexed from 0, so the third row is index 2
        this.$refs.selectableTable.selectRow(2)
      },
      unselectThirdRow() {
        // Rows are indexed from 0, so the third row is index 2
        this.$refs.selectableTable.unselectRow(2)
      },
   
      getInfo(){
        this.axios.get('https://api.solodata.es/pacientes?page='+ this.page)
        .then(data => {
          console.log(data);
          this.list = data.data;
        });
      },
      redEdit(id){
        console.log(id)
      this.$router.push('/Edit/'+ id );
      }
     
     
    },
     mounted() {
      this.getInfo();
    },
}
</script>

<style>

</style>


