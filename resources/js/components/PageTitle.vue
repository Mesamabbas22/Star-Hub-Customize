<script setup>
defineProps({
    page: {
        type: Object,
        required: true,
    },
});
</script>

<template>
    <div class="page-head single">
        <div>
            <p class="eyebrow">Star Hub Customize</p>
            <h1>{{ page.title }}</h1>
            <p>This page is separated inside the Vue SPA and ready for real content.</p>
        </div>
    </div>
</template>
