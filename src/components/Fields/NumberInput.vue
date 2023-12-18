<template>
    <div class="field field__border-purple optional__container">
        <div сlass="optional__input">
            <span class="optional__notes">{{ title }}</span>
            <input placeholder="0" class="field__input" v-model="inputValue" @input="validateInput" />
        </div>
        <img src="icons/cancel.svg" @click="deleteValue" />
    </div>
</template>

<script setup>
import { defineProps, toRefs, ref, defineEmits } from 'vue';
const emits = defineEmits(['setValue'])
let props = defineProps(['title', 'id'])

const title = toRefs(props).title
const id = toRefs(props).id

const inputValue = ref("")

function setValueData(value) {
    emits('setValue', id.value, value);
}

function deleteValue() {
    console.log("test")
    inputValue.value = ""
}

function validateInput(event) {
    let val = event.target.value
    if (isNaN(val)) {
        event.target.value = ''
    } else if (val < 0 || val > 100) {
        event.target.value = ''
    }
    else {
        setValueData(event.target.value)
    }
}

</script>

<style scoped>
.optional__container {
    display: flex;
    width: 100%;
    cursor: pointer;
    align-items: center;
    justify-content: space-between;
    padding: 6px 8px 6px 15px;
}

.optional__input {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
}

.optional__notes {
    font-size: 17px;
    font-weight: 400;
    color: grey;

}

.optional_input input {
    color: #121212 !important;
    font-weight: 300px;
}
</style>