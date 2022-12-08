<template>
  <div class="c-flex c-h-screen c-w-screen c-justify-center c-items-center c-px-8">
  

    <StatusDataTable :title="`<p>FACTORES<br/>AUTORIZADOS</p>`"/>

    <HeaderTable 
      v-for="(item, i) in fatorAutorizado.contratos" 
      :title="item.contratoId"
      :subItems="item.estatus"
      :homo="item.homo"
      :montoMxn="item.montoMxn"
      :montoUsd="item.montoUsd"
    ></HeaderTable>


  </div>


</template>

<script>
import Table from './components/Table.vue'
import axios from 'axios'
import HeaderTable from './components/DataTableDynamic/HeaderTable.vue'
import StatusDataTable from './components/DataTableDynamic/StatusDataTable.vue'

export default({
  components:{
    Table,
    HeaderTable,
    StatusDataTable
  },
  data(){
    return {
      fatorAutorizado: null
    }
  },  
  methods:{
    async getData(){
      let { data } = await axios.get('https://localhost:5001/api/PronosticosAC/escenario?monedaId=1&tc=20.01')
      this.fatorAutorizado = data.data.factorAutorizado

      console.log(this.fatorAutorizado)
    }


  },
  created(){

    this.getData()

  }
 
 
})
</script>

<style>

* {
  font-family: sans-serif;
}
</style>