<template>
    <div 
    class="shopform shopform--flex"
    v-if="show"
    @click.stop="hide">
        <form @click.stop @submit.prevent="submitOrder">
            <div class="shopform__item"> 
                <h3>Имя и Фамилия</h3>
                <input
                    v-model.trim.lazy="userData.name" 
                    type="text" 
                    placeholder="Имя" 
                    required
                >
                <input
                    v-model.trim.lazy="userData.surname" 
                    type="text" 
                    placeholder="Фамилия" 
                    required
                >
            </div>
            <div class="shopform__item"> 
                <h3>Адрес</h3>
                <input 
                    v-model.trim.lazy="userData.city"
                    type="text" 
                    placeholder="Город" 
                    required
                >
                <input 
                    v-model.trim.lazy="userData.addr"
                    type="text" 
                    placeholder="Улица Дом" 
                    required
                >
            </div>
            <div class="shopform__item"> 
                <h3>Контакты</h3>
                <input 
                    v-model.trim.lazy="userData.phone"
                    type="tel" 
                    placeholder="Тел." 
                    required
                >
                <input
                    v-model.trim.lazy="userData.email" 
                    type="email" 
                    placeholder="Электронная почта" 
                    required
                >
            </div>
            <div class="buy-btn">
                <button type="submit">Отправить</button>
            </div>
        </form>  
    </div>
</template>

<script>
export default {
    props: {
        cartData: {
            type: Array,
            required: true,
        },
        show: {
            type: Boolean,
            default: false
        }
    },
    data() {
        return { 
            userData: {
                name: '',
                surname: '',
                city: '',
                addr: '',
                phone: '',
                email: ''
            }
        }
    },
    methods: {
        hide() {
            this.$emit('update:show', false);
        },
        submitOrder() {
            this.$emit('submitOrder',  {action:'submit', data: {id: Date.now(), ...this.userData, data: [...this.cartData]}});
            for(let key in this.userData) {
                this.userData[key] = '';
            }
        }
    }
}
</script>