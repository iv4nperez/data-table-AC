<template>
  <div class="c-flex c-flex-col  c-justify-center c-items-center c-px-8">
  

    <Table
      :label="`<p>FACTORES<br/>AUTORIZADOS</p>`"
      :type="1"
    />

    <Table
      :label="`<p>FACTORES<br/>POR AUTORIZAR</p>`"
      :type="2"
    />

  </div>


</template>

<script>

import Table from './components/DataTableDynamic/Table.vue'


export default({
  components:{
    Table,
  },
  data(){
    return {
     
    }
  },
  methods:{


  },
  created(){

   
  }
 
 
})
</script>

<style>

* {
  font-family: sans-serif;
}
</style>