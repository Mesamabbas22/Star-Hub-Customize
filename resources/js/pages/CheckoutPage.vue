<script setup>
import { ArrowRight, Minus, Plus } from '@lucide/vue';
import PageTitle from '../components/PageTitle.vue';

defineProps({
    page: {
        type: Object,
        required: true,
    },
    cart: {
        type: Array,
        required: true,
    },
    cartTotal: {
        type: Number,
        required: true,
    },
});

defineEmits(['update-quantity']);
</script>

<template>
    <section class="page-shell">
        <PageTitle :page="page" />
        <div class="checkout-layout">
            <div class="panel">
                <div v-for="item in cart" :key="item.id" class="cart-line">
                    <div>
                        <h3>{{ item.name }}</h3>
                        <p>${{ item.price }} each</p>
                    </div>
                    <div class="quantity-control">
                        <button type="button" @click="$emit('update-quantity', item.id, -1)"><Minus :size="14" /></button>
                        <span>{{ item.quantity }}</span>
                        <button type="button" @click="$emit('update-quantity', item.id, 1)"><Plus :size="14" /></button>
                    </div>
                </div>
            </div>
            <div class="panel">
                <h3>Order summary</h3>
                <div class="summary-row"><span>Subtotal</span><span>${{ cartTotal }}</span></div>
                <div class="summary-row"><span>Shipping</span><span>$12</span></div>
                <div class="summary-row total"><span>Total</span><span>${{ cartTotal + 12 }}</span></div>
                <a class="checkout-button mt-5 w-full" :href="page.type === 'cart' ? '#/checkout' : '#/order-confirmation'">
                    Continue
                    <ArrowRight :size="18" />
                </a>
            </div>
        </div>
    </section>
</template>
