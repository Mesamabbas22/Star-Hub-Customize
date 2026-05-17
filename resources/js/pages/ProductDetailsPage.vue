<script setup>
import { ShoppingBag } from '@lucide/vue';

defineProps({
    product: {
        type: Object,
        required: true,
    },
    logoUrl: {
        type: String,
        required: true,
    },
});

defineEmits(['add-to-cart']);
</script>

<template>
    <section class="page-shell">
        <div class="product-detail">
            <div class="product-detail__image">
                <img :src="logoUrl" alt="Signature Logo Hoodie">
            </div>
            <div>
                <p class="eyebrow">Product Details</p>
                <h1>{{ product.name }}</h1>
                <p>{{ product.lead }} with clean logo placement, soft fabric, and bulk order options.</p>
                <strong class="mt-5 block text-3xl">${{ product.price }}</strong>
                <div class="mt-6 flex flex-col gap-3 sm:flex-row">
                    <button class="primary-button" type="button" @click="$emit('add-to-cart', product)">
                        Add to cart
                        <ShoppingBag :size="18" />
                    </button>
                    <a class="secondary-button" href="#/reviews">Read reviews</a>
                </div>
            </div>
        </div>
    </section>
</template>
