<template>
    <my-order-form
        v-model:show="isShowOrderForm"
        :cartData = "cart"
        @submitOrder="handler"
    />
    <section class="cart">
        <header class="cart__header">
            <div class="cart__header--flex container">
                <h1>КОРЗИНА</h1>
            </div>
        </header>
        <div class="cart__main container">
            <div class="cart__main--flex">
                <div class="cart__items cart__items--flex">
                        <cart-item
                            v-for="cartItem in cart"
                            :cartItem="cartItem"
                            :key="cartItem.id_product"
                            @delete="handler"
                            @decrement="handler"
                            @increment="handler"
                        />
                        <div class="cart__main-common">
                            <div class="total-price">
                                Полная стоимость: {{cartTotalCost}} Р.
                            </div>
                        </div>
                        <div class="cart__items-btns">
                            <button @click="showOrderForm">Оформить заказ</button>
                            <button @click="$router.push('/')">Продолжить покупки</button>
                            <button @click.stop="handler({action: 'clear', url: `${this.urlCart}`})">Отчистить корзину</button>
                        </div>
                </div>
            </div>
        </div>
    </section>
</template>

<script>
import CartItem from '../components/CartItem.vue'
import MyOrderForm from '../components/MyOrderForm.vue'
import { mapActions, mapGetters } from 'vuex'

export default {
    components: { CartItem, MyOrderForm },
    data() {
        return {
            isShowOrderForm: false,
        }
    },
    methods: {
        ...mapActions({
            BUILD_ACT_DESC: 'userActions/BUILD_ACT_DESC',
        }),
        handler($data) {
            this.BUILD_ACT_DESC($data);
        },
        showOrderForm() {
            this.isShowOrderForm = !this.isShowOrderForm;
        }
    },
    computed: {
        ...mapGetters({
            cart: 'cart/cart',
            cartTotalCost: 'cart/cartTotalCost',
            cartTotalCnt: 'cart/cartTotalCnt'
        })
    },
}
</script>

