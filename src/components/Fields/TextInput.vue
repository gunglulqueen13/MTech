<template>
    <div class="field field__border-purple">
        <input :placeholder="title" class="field__input" @input="setValueData($event.target.value)" />
    </div>
</template>

<script setup>

import { defineProps, toRefs, defineEmits } from 'vue';
const emits = defineEmits(['setValue'])

function setValueData(value) {
    emits('setValue', id.value, value);
}


let props = defineProps(['title', 'id'])

const title = toRefs(props).title
const id = toRefs(props).id


</script>