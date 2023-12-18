<template>
    <div class="field choise__container" v-on-click-outside="() => {
        showList = false
    }" :class="showList ? 'choise_container-focus' : ''">
        <div class="row" @click="switchShowList()">
            <div class="choise__user">
                <img src="icons/person.svg" />
                <div class="choise__information">
                    <span>{{ user_type }}</span>
                    <span>{{ selectValue ? selectValue : default_value }}</span>
                </div>
            </div>
            <img src="icons/plus.svg" />
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

let props = defineProps(['default', 'user_type', 'options', 'id'])
const emits = defineEmits(['setValue'])

const default_value = toRefs(props).default
const user_type = toRefs(props).user_type
const options = toRefs(props).options
const id = toRefs(props).id

const showList = ref(false)
const selectValue = ref()

function switchShowList() {
    showList.value = showList.value == true ? false : true
}

function setSelectValue(value) {
    selectValue.value = value
    showList.value = false

    setValueData(value)
}

function setValueData(value) {
    emits('setValue', id.value, value);
}

</script>


<style scoped>
.choise__container {
    cursor: pointer;
    position: relative;
    display: flex;
    width: 100%;
    border: 1px solid #B8B8B8;
    border-radius: 0;
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 10px 25px 10px 20px;
}

.choise_container-focus {
    border: 2px solid #b19cd9;
    border-radius: 5px 5px 0 0;
}

.choise__user {
    display: flex;
    align-items: center;
    justify-content: space-between;
}

.choise__information {
    display: flex;
    margin-left: 32px;
    flex-direction: column;
    gap: 2px;
}

.choise__information span:first-child {
    font-size: 14px;
    font-weight: 400;
    color: grey;
}

.choise__information span:last-child {
    font-size: 17px;
    font-weight: 400;
}

.row {
    display: flex;
    width: 100%;
    display: flex;
    align-items: center;
    justify-content: space-between;
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