<template>
    <div class=" c-bg-white  c-full c-border c-border-white c-text-black">
      <div class="c-px-10 c-py-2 c-bg-[#1e295d] c-text-white c-relative">
        <p class="c-text-sm c-font-semibold c-text-center">{{ title }}</p>

        <button @click="(showElements = !showElements)" style="border:1px solid" class="c-bg-white c-px-2 c-text-black c-absolute -c-left-3 c-top-2 c-z-50" >
            {{ showElements ? `-` : `+` }}
        </button>
      </div>
      <table>
        <thead class="c-bg-[#c0bfbf]">
            <tr>
                <th v-if="showElements" colspan="1" class="c-border c-border-black c-text-center c-px-4 c-font-bold c-text-black c-text-sm">MXN</th>
                <th v-if="showElements" colspan="1" class="c-border c-border-black c-text-center c-px-4 c-font-bold c-text-black c-text-sm">USD</th>
                <th colspan="1"     
                :class="[
                    {'c-px-4': showElements},
                    {'c-px-10': !showElements},
                ]"
                class="c-border c-border-black c-text-center c-font-bold c-text-black c-text-sm">
                    <p class="c-w-28">HOM. MXN</p>
                </th>
            </tr>
        </thead>
        <tbody class="c-bg-white">
            <template v-if="!showSegmentos" v-for="(estatus, i) in subItems">
                <tr>
                    <td v-if="showElements" class="c-border c-border-black c-text-black c-px-4 c-text-sm"> {{ estatus.montoMxn }}</td>
                    <td v-if="showElements" class="c-border c-border-black c-text-black c-px-4 c-text-sm">{{ estatus.montoUsd }}</td>
                    <td class="c-border c-border-black c-text-black c-px-4 c-text-sm">{{ estatus.homo }}</td>
                </tr>
                <!-- index !== 0 -->
                <!-- pendiente ajutar conciliacion -->
                <!-- <div :style="`height: ${ maxSizeHeight > 0 ? maxSizeHeight + 'px' : 'auto' }; visibility: ${ index === 0 ? 'visible': 'hidden' }`" id="expandConciliacion" class="c-bg-slate-300" v-if="expandPorConciliar && i === 0 ">
                    <tr  v-for="(conc, j) in dataPorConciliarOt" :key="conc.obraId" class="c-bg-white">

                        <td>
                            <div class="c-w-full">
                                <div class="c-px-10 c-py-1   c-bg-[#1e295d] c-text-white c-relative">
                                    <p class="c-text-xs c-uppercase c-font-bold">{{ conc.contratoId }}</p>
                                </div>
                                <table>
                                    <thead>
                                        <th class="c-border c-bg-[#ee7c31] c-border-black c-text-center c-px-4 c-font-bold c-text-black c-text-xs c-w-full">
                                            OBRA
                                        </th>
                                        <th class="c-border c-border-black c-text-center c-px-4 c-font-bold c-text-black c-text-xs c-w-full c-bg-[#c0bfbf]">
                                            HOM.&nbsp;MXN
                                        </th>
                                        <th v-if="showElements" colspan="1" class="c-border c-border-black c-text-center c-px-4 c-font-bold c-text-black c-text-sm c-bg-[#c0bfbf]">MXN</th>
                                        <th v-if="showElements" colspan="1" class="c-border c-border-black c-text-center c-px-4 c-font-bold c-text-black c-text-sm c-bg-[#c0bfbf]">USD</th>
                                    </thead>
                                    <tbody>
                                        <tr v-for="(ot, o) in conc.obras" :key="o">
                                            <td class="c-border c-border-black c-text-black c-px-4 c-text-sm">
                                                {{ ot.obra }}
                                            </td>
                                            <td class="c-border c-border-black c-text-black c-px-4 c-text-sm">
                                                {{ ot.homo }}
                                            </td>
                                            <td v-if="showElements" class="c-border c-border-black c-text-black c-px-4 c-text-sm"> {{ ot.montoMxn }}</td>
                                            <td v-if="showElements" class="c-border c-border-black c-text-black c-px-4 c-text-sm">{{ ot.montoUsd }}</td>
                                        </tr>
                                    </tbody>
                                </table>
                            </div>
                        </td>
                    </tr>
                </div> -->

                <div :style="`height: ${ maxSizeHeight > 0 ? maxSizeHeight + 'px' : 'auto' }; visibility: ${ index === 0 ? 'visible': 'hidden' }`" id="expandPorConciliar" class="c-bg-slate-300" v-if="expandPorConciliar && i === 1 ">
                    <tr  v-for="(conc, j) in dataPorConciliarOt" :key="conc.obraId" class="c-bg-white">

                        <td>
                            <div class="c-w-full">
                                <div class="c-px-10 c-py-1   c-bg-[#1e295d] c-text-white c-relative">
                                    <p class="c-text-xs c-uppercase c-font-bold">{{ conc.contratoId }}</p>
                                </div>
                                <table>
                                    <thead>
                                        <th class="c-border c-bg-[#ee7c31] c-border-black c-text-center c-px-4 c-font-bold c-text-black c-text-xs c-w-full">
                                            OBRA
                                        </th>
                                        <th class="c-border c-border-black c-text-center c-px-4 c-font-bold c-text-black c-text-xs c-w-full c-bg-[#c0bfbf]">
                                            HOM.&nbsp;MXN
                                        </th>
                                        <th v-if="showElements" colspan="1" class="c-border c-border-black c-text-center c-px-4 c-font-bold c-text-black c-text-sm c-bg-[#c0bfbf]">MXN</th>
                                        <th v-if="showElements" colspan="1" class="c-border c-border-black c-text-center c-px-4 c-font-bold c-text-black c-text-sm c-bg-[#c0bfbf]">USD</th>
                                    </thead>
                                    <tbody>
                                        <tr v-for="(ot, o) in conc.obras" :key="o">
                                            <td class="c-border c-border-black c-text-black c-px-4 c-text-sm">
                                                {{ ot.obra }}
                                            </td>
                                            <td class="c-border c-border-black c-text-black c-px-4 c-text-sm">
                                                {{ ot.homo }}
                                            </td>
                                            <td v-if="showElements" class="c-border c-border-black c-text-black c-px-4 c-text-sm"> {{ ot.montoMxn }}</td>
                                            <td v-if="showElements" class="c-border c-border-black c-text-black c-px-4 c-text-sm">{{ ot.montoUsd }}</td>
                                        </tr>
                                    </tbody>
                                </table>
                            </div>
                        </td>
                    </tr>
                </div>


                <tr v-if="(i + 1 === subItems.length)">
                    <td v-if="showElements" class="c-border c-border-black c-text-black c-px-4 c-text-sm"> {{ montoMxn }}</td>
                    <td v-if="showElements" class="c-border c-border-black c-text-black c-px-4 c-text-sm">{{ montoUsd }}</td>
                    <td class="c-border c-border-black c-text-black c-px-4 c-text-sm">{{ homo }}</td>
                </tr>
            </template>


            <template v-if="showSegmentos"  v-for="(item,i) in subItems">
                <template v-for="(seg,s) in item.segmentos" >
                    <tr>
                        <td v-if="showElements" class="c-border c-border-black c-text-black c-px-4 c-text-sm">
                            {{ seg.montoMxn }}
                        </td>
                        <td v-if="showElements" class="c-border c-border-black c-text-black c-px-4 c-text-sm">
                            {{ seg.montoUsd }}
                        </td>
                        <td class="c-border c-border-black c-text-black c-px-4 c-text-sm">
                            {{ seg.homo }}
                        </td>
                    </tr>
                    <tr v-if="(s + 1 === item.segmentos.length)" class="c-bg-gray-300">
                        <td v-if="showElements" class="c-border c-border-black c-text-black c-px-4 c-text-sm">
                            {{ item.montoMxn }}
                        </td>
                        <td v-if="showElements" class="c-border c-border-black c-text-black c-px-4 c-text-sm">
                            {{ item.montoUsd }}
                        </td>
                        <td class="c-border c-border-black c-text-black c-px-4 c-text-sm">
                            {{ item.homo }}
                        </td>
                    </tr>
                </template>
            </template>
        </tbody>
    </table>

    </div>
</template>
<script>
import axios from 'axios'

export default({
    props:{
        title:{
            type: String,
            default: ''
        },
        subItems: {
            type: Array,
            default: () => []
        },
        homo:{
            type: [Number],
            default: 0
        },
        montoMxn:{
            type: [Number],
            default: 0
        },
        montoUsd:{
            type: [Number],
            default: 0
        },
        segmentos:{
            type: Array,
            default: () => []
        },
        showSegmentos:{
            type: Boolean,
            default: false
        },
        expandConciliacion:{
            type: Boolean,
            default: false
        },
        expandPorConciliar:{
            type: Boolean,
            default: false
        },
        index:{
            type: Number,
            default: 0
        },
        maxSizeHeight:{
            type: Number,
            default: 0
        }
    },
    data(){
        return {
            showElements: false,
            dataConciliacionOt:[],
            dataPorConciliarOt:[]
        }
    },
    watch:{
        async expandConciliacion(){
            if(this.expandConciliacion){
                await this.getOts('Conciliacion')
            }
        },
        async expandPorConciliar(){
            if(this.expandPorConciliar){
               await this.getOts('Conciliar')
               await this.matchHeight()
            }
        }
    },
    methods:{
        async getOts(type){
            const {  data } = await axios.get(`https://localhost:5001/api/PronosticosAC/escenarioOt?monedaId=1&tc=20.01&status=${type}`)

            if(type === 'Conciliacion'){
                this.dataConciliacionOt = data.data
            }

            if(type === 'Conciliar'){
                this.dataPorConciliarOt = data.data

                console.log(this.dataPorConciliarOt )
            }

        },
        matchHeight() {
            // let height = this.$refs.box.clientHeight;
            // console.log(height)
            let box = document.querySelector('#expandPorConciliar')
            console.log(box.offsetHeight)

            this.$emit('sizeHeight', box.offsetHeight)
        }
    },
    async created(){
        await this.getOts()
    }
})
</script>