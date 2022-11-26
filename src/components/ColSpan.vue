<template>
    <div class="block w-full">
        <div class="bg-gray-200 px-2 flex justify-center font-bold">
          {{ title }}
        </div>
      <div class="bg-white  w-full">
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
        }
    },
  data(){
    return {
      showItem: false
    }
  }
})
</script>