<template>
    <div class="block w-full">
        <div class="bg-gray-200 px-2 flex justify-center font-bold">
          {{ title }}
        </div>
      <div v-if="!showSegmentos" class="bg-white w-full">
        <div class="border w-full px-2">
          <span>{{ item?.conciliacion }}</span>
        </div>
        <div class="border w-full px-2">
          <span>{{ item?.porConciliar }}</span>
        </div>
        <div class="border w-full px-2">
          <span>{{ item?.conciliacion + item?.porConciliar }}</span>
        </div>
      </div>
      <div  v-else class="bg-white w-full">
        <div class="border w-full px-2">
          <span>{{ itemSegmentos?.obraConciliacion }}</span>
        </div>
        <div class="border w-full px-2">
          <span>{{ itemSegmentos?.barcoConciliacion }}</span>
        </div>
        <div class="border w-full px-2">
          <span>{{ itemSegmentos?.pernoctaConciliacion }}</span>
        </div>
        <div style="background-color: gray; color:white" class="border w-full px-2">
          <span>{{ itemSegmentos?.totalEnConciliacion }}</span>
        </div>


        <div class="border w-full px-2">
          <span>{{ itemSegmentos?.obraPorConciliacion }}</span>
        </div>
        <div class="border w-full px-2">
          <span>{{ itemSegmentos?.barcoPorConciliacion }}</span>
        </div>
        <div class="border w-full px-2">
          <span>{{ itemSegmentos?.pernoctaPorConciliacion }}</span>
        </div>
        <div style="background-color: gray; color:white" class="border w-full px-2">
          <span>{{ itemSegmentos?.totalPorConciliacion }}</span>
        </div>

      </div>
    </div>
</template>

<script>
export default({
    props:{
        title: {
            type: String,
            default: ''
        },
        item: {
          type: Object,
          default:  () => {}
        },
        itemSegmentos:{
          type: Object,
          default:  () => {}
        },
        showSegmentos:{
          type: Boolean,
          default: false
        }
    },
  data(){
    return {
      showItem: false
    }
  }
})
</script>