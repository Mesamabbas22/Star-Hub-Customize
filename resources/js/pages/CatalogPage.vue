<script setup>
import { Heart, Plus, Search } from '@lucide/vue';

defineProps({
    page: {
        type: Object,
        required: true,
    },
    categories: {
        type: Array,
        required: true,
    },
    products: {
        type: Array,
        required: true,
    },
    logoUrl: {
        type: String,
        required: true,
    },
    searchQuery: {
        type: String,
        required: true,
    },
    activeCategory: {
        type: String,
        required: true,
    },
});

defineEmits(['update:searchQuery', 'update:activeCategory', 'add-to-cart']);
</script>

<template>
    <section class="page-shell">
        <div class="page-head">
            <div>
                <p class="eyebrow">Catalog</p>
                <h1>{{ page.title }}</h1>
                <p>Browse clean custom products and add them to your cart.</p>
            </div>
            <label class="search-box">
                <Search :size="18" />
                <input
                    :value="searchQuery"
                    type="search"
                    placeholder="Search products"
                    @input="$emit('update:searchQuery', $event.target.value)"
                >
            </label>
        </div>

        <div class="mb-6 flex gap-2 overflow-x-auto pb-2">
            <button
                v-for="category in categories"
                :key="category"
                class="category-pill"
                :class="{ active: activeCategory === category }"
                type="button"
                @click="$emit('update:activeCategory', category)"
            >
                {{ category }}
            </button>
        </div>

        <div class="product-grid-list">
            <article v-for="product in products" :key="product.id" class="product-card">
                <div class="product-visual" :class="product.tone">
                    <span>{{ product.tag }}</span>
                    <img :src="logoUrl" alt="">
                </div>
                <div class="p-4">
                    <div class="mb-4 flex items-start justify-between gap-3">
                        <div>
                            <h3 class="font-semibold">{{ product.name }}</h3>
                            <p class="mt-1 text-sm text-[var(--muted)]">{{ product.lead }}</p>
                        </div>
                        <a class="tiny-icon" href="#/wishlist" aria-label="Save product">
                            <Heart :size="16" />
                        </a>
                    </div>
                    <div class="flex items-center justify-between">
                        <strong class="text-lg">${{ product.price }}</strong>
                        <button class="add-button" type="button" @click="$emit('add-to-cart', product)">
                            <Plus :size="17" />
                            Add
                        </button>
                    </div>
                </div>
            </article>
        </div>
    </section>
</template>
