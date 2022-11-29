<template>
    <div>
        <div class="flex">
        <div style="background-color: #1e295d; display: flex; justify-content: center; align-items: center; padding: 20px;color:white;margin-top: 42px;">
            <h2 v-html="label"></h2>
        </div>
        <ColSpanStatus v-model="open" />
        <div class="flex">
            <TableCol
            :showSegmentos="open"
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
import TableCol from '../components/TableCol.vue'
import ColSpanStatus from '../components/ColSpanStatus.vue'
import axios from 'axios'

export default({
  components:{
    TableCol,
    ColSpanStatus
  },
  props:{
    label: {
      type: String,
      default: ''
    }
  },
  data(){
    return {
      fatorAutorizado: null,
      factoresPorAutorizar: null,
      open: false
    }
  },
  methods:{
    async getData(){
      let { data } = await axios.get('https://localhost:5001/api/PronosticosAC/escenario?monedaId=1&tc=20')
      this.fatorAutorizado = data.data.factorAutorizado
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