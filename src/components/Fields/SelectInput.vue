<template>
    <div v-on-click-outside="() => {
        showList = false
    }" class="field field__border-purple choise_container" :class="showList ? 'choise_container-focus' : ''">
        <div class="row" @click="switchShowList()">
            <span class="choise_title">{{ selectValue ? selectValue : title }}</span>
            <img src="icons/arrow_down.svg" />
        </div>
        <ul class="choise_list" v-if="showList">
            <li v-for="(option, key) in options" :key="key" class="field field__border-purple choise_field"
                @click="setSelectValue(option)">{{ option }}
            </li>
        </ul>
    </div>
</template>
<script setup>
import { vOnClickOutside } from '@vueuse/components'
import { defineProps, toRefs, ref, defineEmits } from 'vue';

const emits = defineEmits(['setValue'])

function setValueData(value) {
    emits('setValue', id.value, value);
}

const showList = ref(false)
const selectValue = ref()

function setSelectValue(value) {
    selectValue.value = value
    showList.value = false
    setValueData(value)
}
function switchShowList() {
    showList.value = showList.value == true ? false : true
}



let props = defineProps(['title', 'options', 'id'])

const title = toRefs(props).title
const options = toRefs(props).options
const id = toRefs(props).id
</script>
<style scoped>
.select_field {
    color: #121212;
    width: 100%;
    font-size: 18px;
    border: none;
    outline: none;
}

.choise_container {
    width: 100%;
    cursor: pointer;
    flex-direction: column;
    align-items: start;
    position: relative;
    padding: 15px 8px 15px 15px;

}

.choise_container-focus {
    border: 2px solid #b19cd9;
    border-radius: 5px 5px 0 0;
}

.row {
    width: 100%;
    display: flex;
    justify-content: space-between;
}

.choise_title {
    color: grey;
    font-size: 18px;
}

.choise_list {
    position: absolute;
    top: 52px;
    left: -2px;
    width: calc(100% + 4px);
    padding-left: 0;
    display: flex;
    flex-direction: column;
    align-items: center;
    z-index: 2;
}


.choise_field {
    border-radius: 0;
    border-top: none;
    border-bottom: none;
    border-left: 2px solid #b19cd9;
    border-right: 2px solid #b19cd9;
}



.choise_field:last-child {
    border-radius: 0 0 5px 5px;
    border-bottom: 2px solid #b19cd9;
}

.choise_field:hover {
    background-color: #f7f6f6;
}
</style>