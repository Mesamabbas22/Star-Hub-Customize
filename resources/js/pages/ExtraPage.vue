<script setup>
import { Bell, Home } from '@lucide/vue';
import PageTitle from '../components/PageTitle.vue';

defineProps({
    page: {
        type: Object,
        required: true,
    },
});
</script>

<template>
    <section class="page-shell">
        <PageTitle :page="page" />
        <div class="simple-grid">
            <div class="info-card"><Bell :size="22" /><h3>Overview</h3><p>{{ page.title }} content is separated as its own SPA view.</p></div>
            <div class="info-card"><Home :size="22" /><h3>Next step</h3><p>Connect this view to real Laravel API data when backend modules are ready.</p></div>
        </div>
    </section>
</template>
