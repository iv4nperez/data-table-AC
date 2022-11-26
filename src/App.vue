<template>
  <div class="flex h-screen w-full justify-center items-center">
    <div class="flex">
      <ColSpanStatus />
      <div class="flex">
        <TableCol 
          v-if="fatorAutorizado != null"
          v-for="(item, i) in fatorAutorizado?.contratos" 
          :contrato="item.contratoId"
          :items="item.estatus"
        />
      </div>
    </div>
  </div>


</template>

<script>
import TableCol from './components/TableCol.vue'
import ColSpanStatus from './components/ColSpanStatus.vue'
import axios from 'axios'


export default({
  components:{
    TableCol,
    ColSpanStatus
  },
  data(){
    return {
      fatorAutorizado: null,
      factoresPorAutorizar: null
    }
  },
  methods:{

    async getData(){
      let { data } = await axios.get('https://localhost:5001/api/PronosticosAC/escenario?monedaId=1&tc=20')
      console.log(data)
      this.fatorAutorizado = data.data.factorAutorizado
      // this.factoresPorAutorizar = data.data.factoresPorAutorizar
      console.log(data.data.factorAutorizado)
      // console.log(data.data.factoresPorAutorizar)
    }

  },
  async created(){
    await this.getData()
  }
})
</script>

<style>

* {
  font-family: sans-serif;
}
</style>