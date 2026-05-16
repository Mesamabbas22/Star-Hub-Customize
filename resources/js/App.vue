<script setup>
import { computed, onMounted, onUnmounted, ref } from 'vue';
import {
    ArrowRight,
    Bell,
    Briefcase,
    Check,
    Heart,
    Home,
    Menu,
    Minus,
    PackageCheck,
    Plus,
    Search,
    ShoppingBag,
    Truck,
    UserRound,
    X,
} from '@lucide/vue';

const logoUrl = '/images/star-hub-logo.png';
const menuOpen = ref(false);
const searchQuery = ref('');
const activeCategory = ref('All');
const route = ref(normalizeHash());

const products = [
    { id: 1, name: 'Signature Logo Hoodie', category: 'Apparel', price: 48, tag: 'Best Seller', lead: 'Raised monochrome print', tone: 'dark' },
    { id: 2, name: 'Orbit Ceramic Mug', category: 'Drinkware', price: 18, tag: 'New', lead: 'Wraparound logo mark', tone: 'light' },
    { id: 3, name: 'Desk Identity Kit', category: 'Workspace', price: 64, tag: 'Bundle', lead: 'Notebook, stickers, pen', tone: 'soft' },
    { id: 4, name: 'Minimal Cotton Tee', category: 'Apparel', price: 26, tag: 'Custom', lead: 'Soft print front and back', tone: 'light' },
    { id: 5, name: 'Client Welcome Box', category: 'Gift Sets', price: 92, tag: 'Premium', lead: 'Ready to ship packaging', tone: 'dark' },
    { id: 6, name: 'Laser Bottle Pro', category: 'Drinkware', price: 34, tag: 'Offer', lead: 'Matte steel finish', tone: 'soft' },
];

const cart = ref([
    { ...products[0], quantity: 1 },
    { ...products[2], quantity: 1 },
]);

const pageGroups = [
    {
        title: 'Store',
        links: [
            { path: 'home', title: 'Home', type: 'home' },
            { path: 'shop', title: 'Shop', type: 'shop' },
            { path: 'products', title: 'Products', type: 'products' },
            { path: 'product-details', title: 'Product Details', type: 'product-details' },
            { path: 'categories', title: 'Categories', type: 'categories' },
            { path: 'collections', title: 'Collections', type: 'collections' },
            { path: 'deals-offers', title: 'Deals / Offers', type: 'deals' },
            { path: 'new-arrivals', title: 'New Arrivals', type: 'new-arrivals' },
            { path: 'best-sellers', title: 'Best Sellers', type: 'best-sellers' },
        ],
    },
    {
        title: 'User Account',
        links: [
            { path: 'login', title: 'Login', type: 'auth-login' },
            { path: 'register', title: 'Register', type: 'auth-register' },
            { path: 'forgot-password', title: 'Forgot Password', type: 'auth-forgot' },
            { path: 'my-account', title: 'My Account', type: 'account' },
            { path: 'profile', title: 'Profile', type: 'profile' },
            { path: 'order-history', title: 'Order History', type: 'orders' },
            { path: 'wishlist', title: 'Wishlist', type: 'wishlist' },
            { path: 'addresses', title: 'Addresses', type: 'addresses' },
        ],
    },
    {
        title: 'Cart & Checkout',
        links: [
            { path: 'cart', title: 'Cart', type: 'cart' },
            { path: 'checkout', title: 'Checkout', type: 'checkout' },
            { path: 'payment', title: 'Payment', type: 'payment' },
            { path: 'order-confirmation', title: 'Order Confirmation', type: 'confirmation' },
            { path: 'track-order', title: 'Track Order', type: 'track' },
        ],
    },
    {
        title: 'Info',
        links: [
            { path: 'about-us', title: 'About Us', type: 'info' },
            { path: 'contact-us', title: 'Contact Us', type: 'contact' },
            { path: 'faq', title: 'FAQ', type: 'faq' },
            { path: 'blog', title: 'Blog', type: 'blog' },
            { path: 'careers', title: 'Careers', type: 'careers' },
            { path: 'privacy-policy', title: 'Privacy Policy', type: 'policy' },
            { path: 'terms-conditions', title: 'Terms & Conditions', type: 'policy' },
            { path: 'refund-policy', title: 'Refund Policy', type: 'policy' },
            { path: 'shipping-policy', title: 'Shipping Policy', type: 'policy' },
        ],
    },
    {
        title: 'Extra',
        links: [
            { path: 'search-results', title: 'Search Results', type: 'search-results' },
            { path: 'compare-products', title: 'Compare Products', type: 'compare' },
            { path: 'reviews', title: 'Reviews', type: 'reviews' },
            { path: 'notifications', title: 'Notifications', type: 'notifications' },
            { path: 'support-center', title: 'Support Center', type: 'support' },
            { path: 'vendor-dashboard', title: 'Vendor Dashboard', type: 'vendor' },
            { path: 'affiliate-program', title: 'Affiliate Program', type: 'affiliate' },
        ],
    },
];

const PageTitle = {
    props: {
        page: {
            type: Object,
            required: true,
        },
    },
    template: `
        <div class="page-head single">
            <div>
                <p class="eyebrow">Star Hub Customize</p>
                <h1>{{ page.title }}</h1>
                <p>This page is separated inside the Vue SPA and ready for real content.</p>
            </div>
        </div>
    `,
};

const allPages = pageGroups.flatMap((group) => group.links);
const categories = ['All', ...new Set(products.map((product) => product.category))];
const featuredProduct = products[0];

const currentPage = computed(() => allPages.find((page) => page.path === route.value) ?? allPages[0]);
const cartTotal = computed(() => cart.value.reduce((sum, product) => sum + product.price * product.quantity, 0));
const cartCount = computed(() => cart.value.reduce((sum, product) => sum + product.quantity, 0));

const filteredProducts = computed(() => {
    return products.filter((product) => {
        const matchesCategory = activeCategory.value === 'All' || product.category === activeCategory.value;
        const matchesSearch = product.name.toLowerCase().includes(searchQuery.value.toLowerCase());

        return matchesCategory && matchesSearch;
    });
});

const pageProducts = computed(() => {
    if (currentPage.value.type === 'best-sellers') {
        return products.filter((product) => product.tag === 'Best Seller' || product.tag === 'Premium');
    }

    if (currentPage.value.type === 'new-arrivals') {
        return products.filter((product) => product.tag === 'New' || product.tag === 'Custom');
    }

    if (currentPage.value.type === 'deals') {
        return products.filter((product) => product.tag === 'Offer' || product.price < 30);
    }

    return filteredProducts.value;
});

function normalizeHash() {
    return window.location.hash.replace(/^#\/?/, '') || 'home';
}

function syncRoute() {
    route.value = normalizeHash();
    menuOpen.value = false;
    window.scrollTo({ top: 0, behavior: 'smooth' });
}

function addToCart(product) {
    const item = cart.value.find((cartItem) => cartItem.id === product.id);

    if (item) {
        item.quantity += 1;
        return;
    }

    cart.value.push({ ...product, quantity: 1 });
}

function updateQuantity(id, amount) {
    const item = cart.value.find((cartItem) => cartItem.id === id);

    if (!item) {
        return;
    }

    item.quantity += amount;

    if (item.quantity <= 0) {
        cart.value = cart.value.filter((cartItem) => cartItem.id !== id);
    }
}

onMounted(() => window.addEventListener('hashchange', syncRoute));
onUnmounted(() => window.removeEventListener('hashchange', syncRoute));
</script>

<template>
    <main class="min-h-screen bg-[#f7f7f5] text-[#171717]">
        <header class="sticky top-0 z-30 border-b border-black/10 bg-[#f7f7f5]/95 backdrop-blur">
            <div class="mx-auto flex max-w-7xl items-center justify-between px-5 py-4 lg:px-8">
                <a class="flex items-center gap-3" href="#/home" aria-label="Star Hub Customize home">
                    <img class="h-10 w-10 rounded-md object-cover" :src="logoUrl" alt="Star Hub Customize logo">
                    <span class="text-sm font-semibold uppercase tracking-[0.18em]">Star Hub Customize</span>
                </a>

                <nav class="hidden items-center gap-6 text-sm font-medium text-[#666] lg:flex">
                    <a href="#/home">Home</a>
                    <a href="#/shop">Shop</a>
                    <a href="#/products">Products</a>
                    <a href="#/deals-offers">Deals</a>
                    <a href="#/contact-us">Contact</a>
                </nav>

                <div class="flex items-center gap-2">
                    <a class="icon-button" href="#/search-results" aria-label="Search">
                        <Search :size="18" />
                    </a>
                    <a class="icon-button" href="#/my-account" aria-label="Account">
                        <UserRound :size="18" />
                    </a>
                    <a class="cart-button" href="#/cart" aria-label="Cart">
                        <ShoppingBag :size="18" />
                        <span>{{ cartCount }}</span>
                    </a>
                    <button class="icon-button lg:hidden" type="button" aria-label="Menu" @click="menuOpen = !menuOpen">
                        <Menu v-if="!menuOpen" :size="18" />
                        <X v-else :size="18" />
                    </button>
                </div>
            </div>

            <nav v-if="menuOpen" class="mx-5 grid max-h-[70vh] gap-5 overflow-auto border-t border-black/10 py-4 text-sm lg:hidden">
                <section v-for="group in pageGroups" :key="group.title">
                    <h3 class="mb-2 text-xs font-bold uppercase tracking-[0.18em] text-[#8a8a86]">{{ group.title }}</h3>
                    <div class="grid grid-cols-2 gap-2">
                        <a v-for="page in group.links" :key="page.path" class="mobile-link" :href="`#/${page.path}`">{{ page.title }}</a>
                    </div>
                </section>
            </nav>
        </header>

        <div class="mx-auto grid max-w-7xl gap-8 px-5 py-8 lg:grid-cols-[250px_1fr] lg:px-8">
            <aside class="side-nav hidden lg:block">
                <section v-for="group in pageGroups" :key="group.title" class="mb-6">
                    <h3>{{ group.title }}</h3>
                    <a
                        v-for="page in group.links"
                        :key="page.path"
                        :class="{ active: currentPage.path === page.path }"
                        :href="`#/${page.path}`"
                    >
                        {{ page.title }}
                    </a>
                </section>
            </aside>

            <div class="min-w-0">
                <section v-if="currentPage.type === 'home'" class="grid gap-8">
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
                                <button class="add-button" type="button" @click="addToCart(products[4])">
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

                <section v-else-if="['shop', 'products', 'deals', 'new-arrivals', 'best-sellers', 'search-results'].includes(currentPage.type)" class="page-shell">
                    <div class="page-head">
                        <div>
                            <p class="eyebrow">Catalog</p>
                            <h1>{{ currentPage.title }}</h1>
                            <p>Browse clean custom products and add them to your cart.</p>
                        </div>
                        <label class="search-box">
                            <Search :size="18" />
                            <input v-model="searchQuery" type="search" placeholder="Search products">
                        </label>
                    </div>

                    <div class="mb-6 flex gap-2 overflow-x-auto pb-2">
                        <button
                            v-for="category in categories"
                            :key="category"
                            class="category-pill"
                            :class="{ active: activeCategory === category }"
                            type="button"
                            @click="activeCategory = category"
                        >
                            {{ category }}
                        </button>
                    </div>

                    <div class="product-grid-list">
                        <article v-for="product in pageProducts" :key="product.id" class="product-card">
                            <div class="product-visual" :class="product.tone">
                                <span>{{ product.tag }}</span>
                                <img :src="logoUrl" alt="">
                            </div>
                            <div class="p-4">
                                <div class="mb-4 flex items-start justify-between gap-3">
                                    <div>
                                        <h3 class="font-semibold">{{ product.name }}</h3>
                                        <p class="mt-1 text-sm text-[#666]">{{ product.lead }}</p>
                                    </div>
                                    <a class="tiny-icon" href="#/wishlist" aria-label="Save product">
                                        <Heart :size="16" />
                                    </a>
                                </div>
                                <div class="flex items-center justify-between">
                                    <strong class="text-lg">${{ product.price }}</strong>
                                    <button class="add-button" type="button" @click="addToCart(product)">
                                        <Plus :size="17" />
                                        Add
                                    </button>
                                </div>
                            </div>
                        </article>
                    </div>
                </section>

                <section v-else-if="currentPage.type === 'product-details'" class="page-shell">
                    <div class="product-detail">
                        <div class="product-detail__image">
                            <img :src="logoUrl" alt="Signature Logo Hoodie">
                        </div>
                        <div>
                            <p class="eyebrow">Product Details</p>
                            <h1>{{ featuredProduct.name }}</h1>
                            <p>{{ featuredProduct.lead }} with clean logo placement, soft fabric, and bulk order options.</p>
                            <strong class="mt-5 block text-3xl">${{ featuredProduct.price }}</strong>
                            <div class="mt-6 flex flex-col gap-3 sm:flex-row">
                                <button class="primary-button" type="button" @click="addToCart(featuredProduct)">
                                    Add to cart
                                    <ShoppingBag :size="18" />
                                </button>
                                <a class="secondary-button" href="#/reviews">Read reviews</a>
                            </div>
                        </div>
                    </div>
                </section>

                <section v-else-if="currentPage.type === 'categories'" class="page-shell">
                    <PageTitle :page="currentPage" />
                    <div class="simple-grid">
                        <a v-for="category in categories.filter((item) => item !== 'All')" :key="category" class="info-card" href="#/shop">
                            <h3>{{ category }}</h3>
                            <p>{{ products.filter((product) => product.category === category).length }} products available.</p>
                        </a>
                    </div>
                </section>

                <section v-else-if="currentPage.type === 'collections'" class="page-shell">
                    <PageTitle :page="currentPage" />
                    <div class="simple-grid">
                        <div class="info-card"><h3>Launch Kits</h3><p>Starter bundles for new brands.</p></div>
                        <div class="info-card"><h3>Office Essentials</h3><p>Desk goods and team supplies.</p></div>
                        <div class="info-card"><h3>Gift Boxes</h3><p>Premium packs for clients.</p></div>
                    </div>
                </section>

                <section v-else-if="['cart', 'checkout', 'payment', 'confirmation', 'track'].includes(currentPage.type)" class="page-shell">
                    <PageTitle :page="currentPage" />
                    <div class="checkout-layout">
                        <div class="panel">
                            <div v-for="item in cart" :key="item.id" class="cart-line">
                                <div>
                                    <h3>{{ item.name }}</h3>
                                    <p>${{ item.price }} each</p>
                                </div>
                                <div class="quantity-control">
                                    <button type="button" @click="updateQuantity(item.id, -1)"><Minus :size="14" /></button>
                                    <span>{{ item.quantity }}</span>
                                    <button type="button" @click="updateQuantity(item.id, 1)"><Plus :size="14" /></button>
                                </div>
                            </div>
                        </div>
                        <div class="panel">
                            <h3>Order summary</h3>
                            <div class="summary-row"><span>Subtotal</span><span>${{ cartTotal }}</span></div>
                            <div class="summary-row"><span>Shipping</span><span>$12</span></div>
                            <div class="summary-row total"><span>Total</span><span>${{ cartTotal + 12 }}</span></div>
                            <a class="checkout-button mt-5 w-full" :href="currentPage.type === 'cart' ? '#/checkout' : '#/order-confirmation'">
                                Continue
                                <ArrowRight :size="18" />
                            </a>
                        </div>
                    </div>
                </section>

                <section v-else-if="['auth-login', 'auth-register', 'auth-forgot'].includes(currentPage.type)" class="page-shell narrow">
                    <PageTitle :page="currentPage" />
                    <form class="panel form-panel">
                        <label>Email address<input type="email" placeholder="you@example.com"></label>
                        <label v-if="currentPage.type !== 'auth-forgot'">Password<input type="password" placeholder="Password"></label>
                        <label v-if="currentPage.type === 'auth-register'">Full name<input type="text" placeholder="Your name"></label>
                        <button class="primary-button w-full" type="button">{{ currentPage.title }}</button>
                    </form>
                </section>

                <section v-else-if="['account', 'profile', 'orders', 'wishlist', 'addresses'].includes(currentPage.type)" class="page-shell">
                    <PageTitle :page="currentPage" />
                    <div class="simple-grid">
                        <div class="info-card"><UserRound :size="22" /><h3>Customer profile</h3><p>Manage your contact details and preferences.</p></div>
                        <div class="info-card"><ShoppingBag :size="22" /><h3>Recent order</h3><p>SHC-1042 is currently in proofing.</p></div>
                        <div class="info-card"><Heart :size="22" /><h3>Saved products</h3><p>Keep favorite products ready for your next order.</p></div>
                    </div>
                </section>

                <section v-else-if="['contact', 'support'].includes(currentPage.type)" class="page-shell">
                    <PageTitle :page="currentPage" />
                    <div class="checkout-layout">
                        <form class="panel form-panel">
                            <label>Name<input type="text" placeholder="Your name"></label>
                            <label>Email<input type="email" placeholder="you@example.com"></label>
                            <label>Message<textarea placeholder="How can we help?"></textarea></label>
                            <button class="primary-button" type="button">Send message</button>
                        </form>
                        <div class="panel">
                            <h3>Support details</h3>
                            <p>Email: support@starhubcustomize.test</p>
                            <p>Phone: +1 555 0100</p>
                            <p>Hours: Monday to Friday, 9 AM to 6 PM</p>
                        </div>
                    </div>
                </section>

                <section v-else-if="currentPage.type === 'faq'" class="page-shell">
                    <PageTitle :page="currentPage" />
                    <div class="panel stack">
                        <details open><summary>How long does production take?</summary><p>Most orders are proofed within 48 hours and produced after approval.</p></details>
                        <details><summary>Can I order in bulk?</summary><p>Yes, bulk packaging and shipping are available for teams and clients.</p></details>
                        <details><summary>Can I use my own logo?</summary><p>Yes, the storefront is ready for custom uploaded branding.</p></details>
                    </div>
                </section>

                <section v-else-if="['blog', 'careers', 'policy', 'info'].includes(currentPage.type)" class="page-shell">
                    <PageTitle :page="currentPage" />
                    <div class="simple-grid">
                        <article class="info-card"><Briefcase :size="22" /><h3>{{ currentPage.title }}</h3><p>This SPA page is ready for your real business content, images, and backend data.</p></article>
                        <article class="info-card"><PackageCheck :size="22" /><h3>Brand quality</h3><p>Simple layout, readable sections, and clean calls to action.</p></article>
                    </div>
                </section>

                <section v-else-if="['compare', 'reviews', 'notifications', 'vendor', 'affiliate'].includes(currentPage.type)" class="page-shell">
                    <PageTitle :page="currentPage" />
                    <div class="simple-grid">
                        <div class="info-card"><Bell :size="22" /><h3>Overview</h3><p>{{ currentPage.title }} content is separated as its own SPA view.</p></div>
                        <div class="info-card"><Home :size="22" /><h3>Next step</h3><p>Connect this view to real Laravel API data when backend modules are ready.</p></div>
                    </div>
                </section>
            </div>
        </div>

        <footer class="border-t border-black/10 bg-white">
            <div class="mx-auto flex max-w-7xl flex-col gap-3 px-5 py-6 text-sm text-[#666] md:flex-row md:items-center md:justify-between lg:px-8">
                <span>Star Hub Customize</span>
                <div class="flex flex-wrap gap-4">
                    <a href="#/privacy-policy">Privacy</a>
                    <a href="#/terms-conditions">Terms</a>
                    <a href="#/shipping-policy">Shipping</a>
                    <a href="#/refund-policy">Refund</a>
                </div>
            </div>
        </footer>
    </main>
</template>
