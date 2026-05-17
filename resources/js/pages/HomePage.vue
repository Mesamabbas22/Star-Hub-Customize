<script setup>
import { ArrowRight, Check, PackageCheck, Plus, Truck } from '@lucide/vue';

defineProps({
    logoUrl: {
        type: String,
        required: true,
    },
    products: {
        type: Array,
        required: true,
    },
});

defineEmits(['add-to-cart']);
</script>

<template>
    <section class="grid gap-8">
        <div class="hero-section">
            <div>
                <p class="eyebrow">Custom branded essentials</p>
                <h1>Simple products for your brand.</h1>
                <p>Clean apparel, drinkware, desk kits, and gift boxes customized with the Star Hub Customize style.</p>
                <div class="mt-8 flex flex-col gap-3 sm:flex-row">
                    <a class="primary-button" href="#/shop">
                        Shop products
                        <ArrowRight :size="18" />
                    </a>
                    <a class="secondary-button" href="#/collections">View collections</a>
                </div>
            </div>

            <div class="hero-product compact">
                <div class="hero-product__image">
                    <img :src="logoUrl" alt="Star Hub Customize featured product">
                </div>
                <div class="flex items-end justify-between gap-4">
                    <div>
                        <h2>Launch Brand Kit</h2>
                        <p>Hoodie, mug, notebook, stickers</p>
                    </div>
                    <button class="add-button" type="button" @click="$emit('add-to-cart', products[4])">
                        <Plus :size="17" />
                        Add
                    </button>
                </div>
            </div>
        </div>

        <div class="grid gap-4 md:grid-cols-3">
            <div class="info-card">
                <PackageCheck :size="22" />
                <h3>Proof before print</h3>
                <p>Approve artwork before production.</p>
            </div>
            <div class="info-card">
                <Truck :size="22" />
                <h3>Ready to ship</h3>
                <p>Clean packaging for teams and clients.</p>
            </div>
            <div class="info-card">
                <Check :size="22" />
                <h3>Brand matched</h3>
                <p>Simple layouts built around your logo.</p>
            </div>
        </div>
    </section>
</template>
