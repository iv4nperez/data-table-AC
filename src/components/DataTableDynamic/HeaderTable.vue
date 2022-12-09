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
                <!-- <tr v-if="'648235806' === estatus.contratoId">
                    <td>
                       otro
                       <br>
                       kjnsjn
                    </td>
                </tr>
                <tr v-else>
                    <td>
                       ''
                    </td>
                </tr> -->
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
            type: [String | Number],
            default: ''
        },
        montoMxn:{
            type: [String | Number],
            default: ''
        },
        montoUsd:{
            type: [String | Number],
            default: ''
        },
        segmentos:{
            type: Array,
            default: () => []
        },
        showSegmentos:{
            type: Boolean,
            default: false
        }
    },
    data(){
        return {
            showElements: false
        }
    }
})
</script>