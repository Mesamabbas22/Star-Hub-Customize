<script setup>
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
            <div class="info-card"><h3>Launch Kits</h3><p>Starter bundles for new brands.</p></div>
            <div class="info-card"><h3>Office Essentials</h3><p>Desk goods and team supplies.</p></div>
            <div class="info-card"><h3>Gift Boxes</h3><p>Premium packs for clients.</p></div>
        </div>
    </section>
</template>
