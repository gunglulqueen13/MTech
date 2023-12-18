<template>
    <div class="modal">
        <span class="title">СОЗДАНИЕ</span>
        <span class="head-title">Данные</span>
        <div class="form">
            <div class="list">
                <template v-for="(child, key) in renderFields()" :key="key">
                    <component :is="child" @setValue="setValue"></component>
                </template>
            </div>
            <div class="btns">
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
import ChoiseUser from './Fields/ChoiseUser.vue'
import LinkInput from './Fields/LinkInput.vue'
import { ref } from 'vue'


const fields = ref([
    {
        id: 1,
        type: 'ChoiseUser',
        name: 'manager',
        default: 'Нет пользователя',
        value: '',
        user_type: 'Менеджер',
        options: ['Менеджер 1', 'Менеджер 2', 'Менеджер 3']
    },
    {
        id: 2,
        type: 'TextInput',
        name: 'product_name',
        title: 'Название продукта',
        value: '',
    },
    {
        id: 3,
        type: 'LinkInput',
        title: 'Ссылка в Jira',
        name: 'jira_link',
        note: 'Ссылка в jira, включая https://',
        value: '',
    },
    {
        id: 4,
        type: 'SelectInput',
        name: 'domen',
        title: 'Домен',
        value: '',
        options: ['Бэк - офис', 'Техплатформа', 'Офис больших данных', 'Цифровой опыт поставщика']
    },
])

function renderFields() {
    let componentsArr = []
    fields.value.forEach(elem => {
        if (elem.type == "TextInput") {
            componentsArr.push(<TextInput title={elem.title} id={elem.id} />)
        }
        if (elem.type == "SelectInput") {
            componentsArr.push(<SelectInput title={elem.title} id={elem.id} options={elem.options} />)
        }
        if (elem.type == "ChoiseUser") {
            componentsArr.push(<ChoiseUser default={elem.default} id={elem.id} user_type={elem.user_type} options={elem.options} />)
        }
        if (elem.type == "LinkInput") {
            componentsArr.push(<LinkInput title={elem.title} id={elem.id} note={elem.note} />)
        }
    });

    return componentsArr
}

function setValue(id, value) {
    const fieldIndex = fields.value.findIndex(field => field.id === id);
    if (fieldIndex !== -1) {
        fields.value[fieldIndex].value = value;
    }
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
    width: fit-content;
    font-size: 17px;
    font-weight: 400;
    padding: 0 10px 15px 10px;
    border-bottom: 2px solid #b19cd9;
}

.head-title {
    margin-top: 35px;
    font-size: 18px;
    font-weight: 500;
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