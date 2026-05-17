<script setup>
import { Pencil, Plus, Search, Trash2 } from '@lucide/vue';
import AdminShell from './AdminShell.vue';

defineProps({
    products: {
        type: Array,
        required: true,
    },
});
</script>

<template>
    <AdminShell title="Products" subtitle="Create, review, and organize products available in the storefront.">
        <section class="admin-panel">
            <div class="admin-section-head">
                <label class="admin-search">
                    <Search :size="17" />
                    <input type="search" placeholder="Search products">
                </label>
                <button class="primary-button" type="button"><Plus :size="17" /> Add product</button>
            </div>

            <div class="admin-table admin-table--products">
                <div class="admin-table__row admin-table__head">
                    <span>Product</span>
                    <span>Category</span>
                    <span>Tag</span>
                    <span>Price</span>
                    <span>Actions</span>
                </div>
                <div v-for="product in products" :key="product.id" class="admin-table__row">
                    <span>
                        <strong>{{ product.name }}</strong>
                        <small>{{ product.lead }}</small>
                    </span>
                    <span>{{ product.category }}</span>
                    <span><mark>{{ product.tag }}</mark></span>
                    <span>${{ product.price }}</span>
                    <span class="admin-actions">
                        <button type="button" aria-label="Edit product"><Pencil :size="15" /></button>
                        <button type="button" aria-label="Delete product"><Trash2 :size="15" /></button>
                    </span>
                </div>
            </div>
        </section>
    </AdminShell>
</template>
