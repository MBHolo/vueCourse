<script setup>

    import { Form, Field, ErrorMessage } from 'vee-validate';
    import * as yup from 'yup';
    import { ref } from 'vue';

    const itemChooseUpdate = defineProps(["itemChooseUpdate"]);

    const titleItem = defineModel('itemTitle');
    const itemPrice = defineModel('itemPrice');
    const itemId    = defineModel('itemId');

    const scheme = yup.object({
        titleItemForm:  yup.string().required("Обязательное поле"),
        priceItemForm:  yup.number().typeError('Должно быть числом'),
        idItemForm:     yup.number(),
    });

    const emit = defineEmits(['updateItemInfo'])
    function updateItem(updateItemInfo){
        emit('updateItemInfo', updateItemInfo);
    }

</script>

<template>
    <Form @submit="updateItem" :validation-schema="scheme">
        <div class="form__update">
            <Field
                name="idItemForm"
                type="hidden"
                v-model="itemId"
            >
            </Field>
            <label>Название элемента</label>
            <Field
                name="titleItemForm"
                type="text"
                v-model="titleItem"
            >
            </Field>
            <label>Цена элемента</label>
            <Field
                name="priceItemForm"
                type="text"
                v-model="itemPrice"
            >
            </Field>
            <button type="submit">Сохранить</button>
        </div>
    </Form>

</template>

<style scoped>
    .form__update{
        display: flex;
        flex-direction: column;
        gap: 10px;
    }
</style>