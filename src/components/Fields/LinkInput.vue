<template>
    <div class="field__link">
        <div class="field field__border-purple">
            <input :placeholder="title" class="field__input" @input="setValueData($event.target.value)" />

        </div>
        <span class="field__link__notes">{{ note }}</span>
    </div>
</template>

<script setup>
import { defineProps, toRefs, defineEmits } from 'vue';
const emits = defineEmits(['setValue'])

function setValueData(value) {
    emits('setValue', id.value, value);
}


let props = defineProps(['title', 'note', 'id'])

const title = toRefs(props).title
const note = toRefs(props).note
const id = toRefs(props).id


</script>
<style scoped>
.field__link {
    display: flex;
    flex-direction: column;
    gap: 5px;

}

.field__link__notes {
    margin-left: 20px;
    font-size: 16px;
    font-weight: 300;
    color: grey;

}
</style>