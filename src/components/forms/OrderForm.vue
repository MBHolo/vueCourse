<script setup>

    import { Form, Field, ErrorMessage } from 'vee-validate';
    import * as yup from 'yup';

    const countryCodes = ['de', 'fr', 'it', 'es', 'uk', 'cn', 'jp', 'in', 'kr', 'us', 'ca', 'ru', 'kz', 'by', 'ua'];

    const scheme = yup.object({
        name:       yup.string("*Неправильное значение").required('*Обязательное поле'),
        birthDate:  yup.date().max(new Date(), 'Дата рождения не может быть в будущем').required('Дата рождения обязательна'),
        email:      yup.string().email('*Введите корретный email').required("*Обязательное поле"),
        country:    yup.string().oneOf(countryCodes, 'Выберите страну из списка').required('Страна обязательна*'),
        adres:      yup.string().required("*Обязательное поле"),
        cartNumber: yup.string().required("*Обязательное поле"),
        policy:     yup.boolean().oneOf([true], 'Вы должны принять условия использования').required('*Необходимо ваше согласие'),
    });

    const emit = defineEmits(['order']);
    function onSubmitOrder(order){
        emit('order', order);
    }
</script>

<template>
    <Form @submit="onSubmitOrder" :validation-schema="scheme" class="order__form-block">
        <div class="order__form-item">
            <div class="order__form-item-input">
                <Field 
                    name="name"
                    type="text"
                    placeholder="ФИО*"
                />
            </div>
            <ErrorMessage name="name" v-slot="{ message }">
                {{ message }}
            </ErrorMessage>
        </div>
        <div class="order__form-item">
            <div class="order__form-item-input">
                <Field
                    name="birthDate"
                    v-slot="{ field }"
                >
                    <input 
                        v-bind="field"
                        type="date"
                        placeholder="дд.мм.гггг"
                    />
                </Field>
            </div>
            <ErrorMessage name="birthDate" v-slot="{ message }">
                {{ message }}
            </ErrorMessage>
        </div>
        <div class="order__form-item">
            <div class="order__form-item-input">
                <Field
                    name="email"
                    type="text"
                    placeholder="E-mail*" 
                />
            </div>
            <ErrorMessage name="email" v-slot="{ message }">
                {{ message }}
            </ErrorMessage>
        </div>
        <div class="order__form-item">
            <div class="order__form-item-input">         
                <Field
                    name="country"
                    as="select"
                    v-slot="field"
                >
                        <option value="" disabled>-- Выберите страну --</option>
                        <optgroup label="Европа">
                            <option value="de">Германия</option>
                            <option value="fr">Франция</option>
                            <option value="it">Италия</option>
                            <option value="es">Испания</option>
                            <option value="uk">Великобритания</option>
                        </optgroup>                      
                        <optgroup label="Азия">
                            <option value="cn">Китай</option>
                            <option value="jp">Япония</option>
                            <option value="in">Индия</option>
                            <option value="kr">Южная Корея</option>
                        </optgroup>
                        <optgroup label="Северная Америка">
                            <option value="us">США</option>
                            <option value="ca">Канада</option>
                        </optgroup>
                        <optgroup label="СНГ">
                            <option value="ru">Россия</option>
                            <option value="kz">Казахстан</option>
                            <option value="by">Беларусь</option>
                            <option value="ua">Украина</option>
                        </optgroup>
                </Field>
            </div>  
            <ErrorMessage name="country" v-slot="{ message }">
                {{ message }}
            </ErrorMessage>
        </div>
        <div class="order__form-item">
            <div class="order__form-item-input">
                <Field
                    name="adres"
                    type="text"
                    placeholder="Адрес*" 
                />
            </div>
            <ErrorMessage name="adres" v-slot="{ message }">
                {{ message }}
            </ErrorMessage>
        </div>
        <div class="order__form-item">
            <div class="order__form-item-input">         
                <Field
                    name="cartNumber"
                    type="text" 
                    v-slot="field"
                />
            </div>  
            <ErrorMessage name="cartNumber" v-slot="{ message }">
                {{ message }}
            </ErrorMessage>
        </div>
        <div class="order__form-item">
            <div class="order__form-item-input">         
                <Field
                    name="policy"
                    type="checkbox"
                    v-slot="{ field }"
                    :value="true"
                >
                    <input 
                        v-bind="field" 
                        type="checkbox"
                        :true-value="true" 
                        :false-value="false"
                    />
                </Field>
            </div>  
            <ErrorMessage name="policy" v-slot="{ message }">
                {{ message }}
            </ErrorMessage>
        </div>
        <div class="order__form-item">
            <button type="submit">Оформить заказ</button>
        </div>
    </Form>
</template>

<style scoped>
    .order__form-block{
        display: flex;
        flex-direction: column;
        gap: 20px;
    }
    .order__form-item{
        display: flex;
        gap: 20px;
    }
    .order__form-item-input input, select{
        font-size: 20px;
        width: 400px;
    }
</style>