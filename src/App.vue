<template>
  <CreateEmployee v-if="modalType == 'Сотрудник'" />
  <CreateProduct v-if="modalType == 'Продукт'" />
</template>

<script setup>

import { ref } from 'vue';
import CreateEmployee from './components/CreateEmployee.vue'
import CreateProduct from './components/CreateProduct.vue'

const modalType = ref("Сотрудник");

// Чтобы выбрать модальное окно нужно в рефе указать его название (Продукт или Сотрудник)
// При нажатии на кнопку "Создать" в консоль будет выведен объект с ключами и значениями, который можно будет потом отправить на сервер
// Кнопка "Отмена" ререндерит компонент

</script>