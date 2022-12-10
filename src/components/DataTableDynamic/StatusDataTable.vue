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
        <div  class="c-flex c-gap-1">
            <table class="c-w-40 c-flex-shrink-0">
                <thead class="c-bg-[#ee7c31]">
                    <tr class="c-relative">
                        <th :colspan="3"  colspan="1" class="c-border c-border-black c-text-center c-px-4 c-font-bold c-text-black c-text-sm">ESTATUS</th>

                        <button @click="(showSegmentos = !showSegmentos)" style="border:1px solid" class="c-bg-white c-px-2 c-text-black c-absolute -c-left-3 -c-top-1 c-z-50" >
                            {{ showSegmentos ? `-` : `+` }}
                        </button>

                    </tr>
                </thead>
                <tbody class="c-bg-white">
                    <tr class="c-relative">
                        <td colspan="1"  class="c-border c-border-black c-text-black c-px-4 c-text-sm c-font-bold c-text-center">EN CONCILIACION</td>
                        <button @click="() => OTConcoliacion()" v-if="!showSegmentos" style="border:1px solid;height: 15px;bottom:-7px;right:-5px;;width:15px" class="c-bg-white  c-text-black c-absolute c-z-50 c-flex  c-justify-center c-items-center">
                            {{  showOTConcoliacion? '-' : '+' }}
                        </button>
                    </tr>
                    <tr :style="`height: ${ maxSizeHeight > 0 && showOTPorConcoliacion ? maxSizeHeight + 22 + 'px' : 'auto' } ;`" class="c-relative" v-if="!showSegmentos">
                        <td  class="c-border c-border-black c-text-black c-px-4 c-text-sm c-font-bold c-text-center">POR CONCILIAR</td>
                        <button @click="() => OTPorConcoliacion()" v-if="!showSegmentos" style="border:1px solid;height: 15px;bottom:-7px;right:-5px;width:15px" class="c-bg-white  c-text-black c-absolute c-z-50 c-flex c-justify-center c-items-center">
                            {{ showOTPorConcoliacion ? '-' : '+' }}
                        </button>
                    </tr>
                    <tr  v-if="!showSegmentos">
                        <td class="c-border c-border-black c-text-black c-px-4 c-text-sm c-font-bold c-text-center">TOTALES:</td>
                    </tr>
                </tbody>
            </table>
            <table class="c-w-full" v-if="showSegmentos">
                <thead class="c-bg-[#ee7c31]">
                    <tr>
                        <th :colspan="3"  colspan="1" class="c-border c-border-black c-text-center c-px-4 c-font-bold c-text-black c-text-sm">SEGMENTOS</th>
                    </tr>
                </thead>
                <tbody class="c-bg-white">
                    <tr>
                        <td  class="c-border c-border-black c-text-black c-px-4 c-text-sm c-font-bold c-text-right">BARCO</td>
                    </tr>
                    <tr>
                        <td  class="c-border c-border-black c-text-black c-px-4 c-text-sm c-font-bold c-text-right">OBRA</td>
                    </tr>
                    <tr>
                        <td class="c-border c-border-black c-text-black c-px-4 c-text-sm c-font-bold c-text-right">PERNOCTA</td>
                    </tr>
                    <tr class="c-bg-gray-300">
                        <td class="c-border c-border-black c-text-black c-px-4 c-text-sm c-font-bold c-text-right">TOTALES</td>
                    </tr>
                </tbody>
            </table>
        </div>

        <div v-if="showSegmentos" class="c-flex c-gap-1 c-w-full">
            <table class="c-w-40 c-flex-shrink-0">
                <tbody class="c-bg-white">
                    <tr >
                        <td colspan="1"  class="c-border c-border-black c-text-black c-px-4 c-text-sm c-font-bold c-text-center">POR CONCILIAR</td>
                    </tr>
                    
                </tbody>
            </table>
            <table class="c-w-full" v-if="showSegmentos">
                <tbody class="c-bg-white">
                    <tr>
                        <td  class="c-border c-border-black c-text-black c-px-4 c-text-sm c-font-bold c-text-right">BARCO</td>
                    </tr>
                    <tr>
                        <td  class="c-border c-border-black c-text-black c-px-4 c-text-sm c-font-bold c-text-right">OBRA</td>
                    </tr>
                    <tr>
                        <td class="c-border c-border-black c-text-black c-px-4 c-text-sm c-font-bold c-text-right">PERNOCTA</td>
                    </tr>
                    <tr class="c-bg-gray-300">
                        <td class="c-border c-border-black c-text-black c-px-4 c-text-sm c-font-bold c-text-right">TOTALES</td>
                    </tr>
                </tbody>
            </table>
        </div>
        
    </div>
    </div>
</template>
<script>
export default({
    props:{
        title:{
            type: String,
            default: ''
        },
        value:{
            type: Boolean,
            default: false
        },
        maxSizeHeight:{
            type: Number,
            default: 0
        }
    },
    data(){
        return {
            showElements: false,
            showOTConcoliacion: false,
            showOTPorConcoliacion: false
        }
    },
    methods:{
        OTConcoliacion(){
            this.showOTConcoliacion = !this.showOTConcoliacion
            this.$emit('OTConcoliacion', this.showOTConcoliacion)
        },
        OTPorConcoliacion(){
            this.showOTPorConcoliacion = !this.showOTPorConcoliacion
            this.$emit('OTPorConcoliacion', this.showOTPorConcoliacion)
        }
    },
    computed:{
        showSegmentos: {
            get(){
                return this.value;
            },
            set(value){
                this.$emit('input', value)
            }
        },
    
    }
})
</script>