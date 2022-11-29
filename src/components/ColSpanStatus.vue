<template>
    <div>
      <div class="px-6 bg-white py-2 flex flex-col items-center relative border border-white">
        <h2 class="text-white">test</h2>
      </div>
      <div class="flex">
        <div class="w-full bg-orange-500 px-4 font-bold flex justify-center relative">
          ESTATUS
          <button style="border: 1px solid; right: -8px; top: 4px;z-index: 10;" class="absolute bg-white w-4 h-4 flex justify-center items-center -ml-2" @click="show = !show">
              {{ show ? '-' : '+' }}
            </button>
        </div>
        <div class="w-full bg-orange-500 px-4 font-bold flex justify-center">
          SEGMENTOS
        </div>
      </div>
        <div class="flex">
          <div 
            :class="[
              { 'flex justify-end': !show },
              { 'flex justify-center items-center': show }
            ]"
            class="border w-full px-4  relative">
            
            <span class="font-bold block">EN CONCILIACIÓN</span>
          </div>
          <div v-if="show">
            <div v-for="(item) in segmentos" class="border w-full px-4 flex justify-end relative">
              <span class="font-bold block">{{ item }}</span>
            </div>
          </div>
        </div>
        <div v-if="show"
          style="background-color: gray;color: white"
          class="border w-full px-2 flex justify-end"
        >
          <span>TOTALES</span>
        </div>
        <div class="flex">
          <div
            :class="[
              { 'flex justify-end': !show },
              { 'flex justify-center items-center': show }
            ]"
            class="border w-full px-4  relative">
            <span class="font-bold block">POR CONCILIAR</span>
          </div>
          <div v-if="show">
            <div v-for="(item) in segmentos" class="border w-full px-4 flex justify-end relative">
              <span class="font-bold block">{{ item }}</span>
            </div>
          </div>
        </div>
        <div
        style="background-color: gray;color: white"
        class="border w-full px-2 flex justify-end">
          <span>TOTALES</span>
        </div>
      </div>
</template>


<script>
export default({
  props: {
    value: {
      type: Boolean,
      default: false
    }
  },
  data(){
    return {
      segmentos: ['OBRA','BARCO', 'PERNOCTA']
    }
  },
  computed:{
    show: {
        get(){
            return this.value;
        },
        set(value){
            this.$emit('input', value)
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