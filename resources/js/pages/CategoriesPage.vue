<script setup>
import PageTitle from '../components/PageTitle.vue';

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
});
</script>

<template>
    <section class="page-shell">
        <PageTitle :page="page" />
        <div class="simple-grid">
            <a v-for="category in categories.filter((item) => item !== 'All')" :key="category" class="info-card" href="#/shop">
                <h3>{{ category }}</h3>
                <p>{{ products.filter((product) => product.category === category).length }} products available.</p>
            </a>
        </div>
    </section>
</template>
