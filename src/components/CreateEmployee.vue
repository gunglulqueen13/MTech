<template>
    <div class="modal" :key="componentKey">
        <span class="title text-center">Создать сотрудника</span>
        <div class="form">
            <div class="list">
                <template v-for="(child, key) in renderFields()" :key="key">
                    <component :is="child" @setValue="setValue"></component>
                </template>
            </div>
            <div class="btns">
                <button class="cancel" @click="resetComponent">
                    <span>ОТМЕНА</span>
                </button>
                <button class="creation" @click="result">
                    <span>СОЗДАТЬ</span>
                </button>
            </div>

        </div>
    </div>
</template>
<script setup>
import TextInput from './Fields/TextInput.vue'
import SelectInput from './Fields/SelectInput.vue'
import NumberInput from './Fields/NumberInput.vue'
import ChoiseUser from './Fields/ChoiseUser.vue'
import { ref } from 'vue'

let componentKey = ref(0)

function resetComponent() {
    componentKey.value += 1
}

function setValue(id, value) {
    const fieldIndex = fields.value.findIndex(field => field.id === id);
    if (fieldIndex !== -1) {
        fields.value[fieldIndex].value = value;
    }
}

const fields = ref([
    {
        id: 1,
        type: 'ChoiseUser',
        name: 'employee',
        default: 'Нет пользователя',
        value: '',
        user_type: 'Сотрудник',
        options: ['Сотрудник 1', 'Сотрудник 2', 'Сотрудник 3']
    },
    {
        id: 2,
        type: 'ChoiseUser',
        name: 'supervisor',
        default: 'Нет пользователя',
        value: '',
        user_type: 'Руководитель',
        options: ['Руководитель 1', 'Руководитель 2', 'Руководитель 3']
    },
    {
        id: 3,
        type: 'SelectInput',
        name: 'bet_type',
        title: 'Тип ставки',
        value: '',
        options: ['opex', 'capex']
    },
    {
        id: 4,
        type: 'SelectInput',
        name: 'business_unit',
        title: 'Бизнес единица',
        value: '',
        options: ['MVP', 'MTech']
    },
    {
        id: 5,
        type: 'NumberInput',
        name: 'capitalization_percentage',
        title: 'Процент капитализации',
        value: 0,
    },
    {
        id: 6,
        type: 'TextInput',
        name: 'job_title',
        title: 'Должность',
        value: '',
    }


])

function renderFields() {
    let componentsArr = []
    fields.value.forEach(elem => {
        if (elem.type == "TextInput") {
            componentsArr.push(<TextInput title={elem.title} id={elem.id} />)
        }
        if (elem.type == "NumberInput") {
            componentsArr.push(<NumberInput title={elem.title} id={elem.id} />)
        }
        if (elem.type == "SelectInput") {
            componentsArr.push(<SelectInput title={elem.title} id={elem.id} options={elem.options} />)
        }
        if (elem.type == "ChoiseUser") {
            componentsArr.push(<ChoiseUser default={elem.default} id={elem.id} user_type={elem.user_type} options={elem.options} />)
        }
    });

    return componentsArr
}

function result() {
    const result = fields.value.map((item) => {
        return {
            name: item.name,
            value: item.value
        }
    })
    console.log(result)
}


</script>
<style scoped>
.title {
    font-size: 25px;
    font-weight: 400;
}

.list {
    margin-top: 20px;
    display: flex;
    flex-direction: column;
    gap: 20px;
    width: 800px
}

.btns {
    margin-top: 40px;
    display: flex;
    justify-content: end;
}
</style>