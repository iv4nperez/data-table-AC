<template>
   <div class="c-flex c-w-full c-overflow-auto  c-justify-center">
      <StatusDataTable
        :title="label"
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
</template>


<script>

import axios from 'axios'
import HeaderTable  from '../DataTableDynamic/HeaderTable'
import StatusDataTable  from '../DataTableDynamic/StatusDataTable'


export default({
  components:{
    HeaderTable,
    StatusDataTable
  },
  props:{
    label:{
        type: String,
        default: ''
    },
    type:{
        type: Number,
        default: 1 // factores autorizados, 2 factores por autorizar 
    }
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

      if(this.type === 1){
        this.fatorAutorizado = data.data.factorAutorizado
      }else{    
        this.fatorAutorizado = data.data.factoresPorAutorizar
      }

    }
  },
  created(){
    this.getData()
  }
});

</script>
