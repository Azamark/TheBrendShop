<template>
    <section class="product-page product-page--box">
        <header class="product-page__header">
            <div class="product-page__header--flex container">
            <h1>Карточка товара</h1>
            </div>
        </header>
        <section class="product-page__body product-page__body--flex">
            <img class="product-page__img" :src="require(`../assets/${product.img}`)" alt="product">
            <div class="product-page__desc container">
                <div class="product-page__desc--flex">
                    <h2>{{product.product_name}}</h2>
                    <div class="line__red"></div>
                    <p> Категория: {{product.category}}</p>
                    <p>
                        Lorem ipsum dolor sit amet consectetur adipisicing elit. Natus beatae harum ad fugiat laudantium quam est ducimus et cumque, adipisci, eveniet fugit officia. Inventore?
                    </p>
                    <strong>{{product.price}} Р.</strong>
                    <div class="line__grey"></div>
                    <div class="add__btn--red">
                        <my-button-add
                        @addItem="handler"
                        />
                    </div>
                </div>
            </div>
        </section>
    </section>
</template>

<script>
import MyButtonAdd from '../components/UI/MyButtonAdd.vue'
import { mapGetters, mapActions } from 'vuex'

export default {
    components: {
        MyButtonAdd
    },
    methods: {
        ...mapActions({
            BUILD_ACT_DESC: 'userActions/BUILD_ACT_DESC',
        }),
        handler(){
            this.BUILD_ACT_DESC({
                action: 'add',
                data: this.product,
            });
        }
    },
    computed: {
        ...mapGetters({
            product: 'catalog/product',
        })
    }
}
</script>
