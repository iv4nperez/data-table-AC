<template>
    <div class="bg-blue-500 h-fit w-auto ">
    <div class="px-6 bg-[#1e295d] py-2 flex flex-col items-center relative border">
      <h2 class="text-white">{{ contrato }}</h2>
      <button style="border: 1px solid;" class="absolute bg-white left-0 top-0 w-4 h-4 flex justify-center items-center -ml-2" @click="showItem = !showItem">
        {{ showItem ? '-' : '+' }}
      </button>
    </div>
    <div class="flex">
        <div v-if="showItem" class="flex transition ease-in-out delay-150" >
          <ColSpan class="transition ease-in-out delay-150" title="MXN" :item="itemsPrepareMxn"  />
          <ColSpan class="transition ease-in-out delay-150" title="USD" :item="itemsPrepareUsd" />
        </div>
        <ColSpan class="transition ease-in-out delay-150" title="HOM .MXN" :item="itemsPrepareTotal" />
     </div>
    </div>
</template>

<script>
import ColSpan from './ColSpan.vue'
export default({
  components:{
    ColSpan
  },
  props: {
    contrato:{
        type: String,
        default: ''
    },
    items: {
      type: Array,
      default: () => []
    }
  },
  data(){
    return {
      showItem: false
    }
  },
  computed:{
    itemsPrepareMxn(){
      let mxnConciliacion = this.items.filter((x) => x.estatus.toLowerCase().trim() === 'conciliacion')
      let mxnPorConciliacion = this.items.filter((x) => x.estatus.toLowerCase().trim() === 'conciliar')
      let totales = this.items.filter((x) => x.estatus.toLowerCase().trim() === 'n/a')

      return {
        contrato: this.contrato,
        conciliacion: mxnConciliacion[0]?.montoMxn ?? 0,
        porConciliar: mxnPorConciliacion[0]?.montoMxn ?? 0,
        total: totales[0]?.montoMxn ?? 0
      }
    },
    itemsPrepareUsd(){
      let mxnConciliacion = this.items.filter((x) => x.estatus.toLowerCase().trim() === 'conciliacion')
      let mxnPorConciliacion = this.items.filter((x) => x.estatus.toLowerCase().trim() === 'conciliar')
      let totales = this.items.filter((x) => x.estatus.toLowerCase().trim() === 'n/a')

      return {
        contrato: this.contrato,
        conciliacion: mxnConciliacion[0]?.montoUsd ?? 0,
        porConciliar: mxnPorConciliacion[0]?.montoUsd ?? 0,
        total: totales[0]?.montoUsd ?? 0
      }
    },
    itemsPrepareTotal(){
      let mxnConciliacion = this.items.filter((x) => x.estatus.toLowerCase().trim() === 'conciliacion')
      let mxnPorConciliacion = this.items.filter((x) => x.estatus.toLowerCase().trim() === 'conciliar')
      let totales = this.items.filter((x) => x.estatus.toLowerCase().trim() === 'n/a')

      return {
        contrato: this.contrato,
        conciliacion: mxnConciliacion[0]?.homo ?? 0,
        porConciliar: mxnPorConciliacion[0]?.homo ?? 0,
        total: totales[0]?.homo ?? 0
      }
    }

  }
})
</script>

<style>
.animation{
  transition: all 0.100 ease;
}


</style>