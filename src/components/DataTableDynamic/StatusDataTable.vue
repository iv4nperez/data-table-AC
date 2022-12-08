<template>

    <div  class="c-flex" >
        <div class=" c-bg-[#1e295d] c-full c-border c-border-white c-text-black c-flex c-justify-center c-items-center c-px-4 c-mt-9">
           <div class="c-text-sm c-text-white c-font-bold c-text-center" v-html="title"></div>
        </div>
    <div class=" c-bg-white  c-full c-border c-border-white c-text-black">
        <div class="c-px-10 c-py-2 c-bg-white c-text-white c-relative">
            <p class="c-text-sm c-font-semibold c-text-center c-select-none">''</p>

            <!-- <button @click="(showElements = !showElements)" style="border:1px solid" class="c-bg-white c-px-2 c-text-black c-absolute -c-left-3 c-top-2 c-z-50" >
                {{ showElements ? `-` : `+` }}
            </button> -->
        </div>
        <table>
            <thead class="c-bg-[#ee7c31]">
                <tr>
                    <th :colspan="3"  colspan="1" class="c-border c-border-black c-text-center c-px-4 c-font-bold c-text-black c-text-sm">ESTATUS</th>
                </tr>
            </thead>
            <tbody class="c-bg-white">
                <tr>
                    <td  class="c-border c-border-black c-text-black c-px-4 c-text-sm c-font-bold c-text-right"> EN CONCILIACION</td>
                </tr>
                <tr>
                    <td  class="c-border c-border-black c-text-black c-px-4 c-text-sm c-font-bold c-text-right">POR CONCILIAR</td>
                </tr>
                <tr>
                    <td class="c-border c-border-black c-text-black c-px-4 c-text-sm c-font-bold c-text-right">TOTALES:</td>
                </tr>
            </tbody>
        </table>
    </div>
    </div>
</template>
<script>
export default({
    props:{
        title:{
            type: String,
            default: ''
        }
    },
    data(){
        return {
            showElements: false
        }
    }
})
</script>