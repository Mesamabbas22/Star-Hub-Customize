<script setup>
import { Briefcase, PackageCheck } from '@lucide/vue';
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
            <article class="info-card"><Briefcase :size="22" /><h3>{{ page.title }}</h3><p>This SPA page is ready for your real business content, images, and backend data.</p></article>
            <article class="info-card"><PackageCheck :size="22" /><h3>Brand quality</h3><p>Simple layout, readable sections, and clean calls to action.</p></article>
        </div>
    </section>
</template>
