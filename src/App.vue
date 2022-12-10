<template>
  <div class="c-flex  c-justify-center c-items-center c-px-8">
  

   <div class="c-flex c-w-full c-overflow-auto  c-justify-center">
      <StatusDataTable 
        :title="`<p>FACTORES<br/>AUTORIZADOS</p>`" 
        v-model="showSegmentos" 
        @OTConcoliacion="OTConcoliacion"
        @OTPorConcoliacion="OTPorConcoliacion"
        :maxSizeHeight="sizeAllItems"
      />

    <HeaderTable 
      v-for="(item, i) in fatorAutorizado?.contratos" 
      :title="item.contratoId"
      :subItems="item.estatus"
      :homo="item.homo"
      :montoMxn="item.montoMxn"
      :montoUsd="item.montoUsd"
      :showSegmentos="showSegmentos"
      :expandConciliacion="showOTConcoliacion"
      :expandPorConciliar="showOTPorConcoliacion"
      :index="i"
      @sizeHeight="getSize"
      :maxSizeHeight="sizeAllItems"
    ></HeaderTable>
   
   </div>


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
      fatorAutorizado: null,
      showSegmentos: false,
      showOTConcoliacion: false,
      showOTPorConcoliacion: false,
      sizeAllItems: 0
    }
  },
  methods:{

    OTConcoliacion(n){
        this.showOTConcoliacion = n
    },
    OTPorConcoliacion(n){
        this.showOTPorConcoliacion = n
    },
    getSize(h){
      this.sizeAllItems = h
    },  
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