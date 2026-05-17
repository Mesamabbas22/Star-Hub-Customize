<script setup>
import { computed, onMounted, onUnmounted, ref } from 'vue';
import { Menu, Search, ShoppingBag, UserRound, X } from '@lucide/vue';
import AccountPage from './pages/AccountPage.vue';
import AuthPage from './pages/AuthPage.vue';
import CatalogPage from './pages/CatalogPage.vue';
import CategoriesPage from './pages/CategoriesPage.vue';
import CheckoutPage from './pages/CheckoutPage.vue';
import CollectionsPage from './pages/CollectionsPage.vue';
import ContactPage from './pages/ContactPage.vue';
import ExtraPage from './pages/ExtraPage.vue';
import FaqPage from './pages/FaqPage.vue';
import HomePage from './pages/HomePage.vue';
import InfoPage from './pages/InfoPage.vue';
import ProductDetailsPage from './pages/ProductDetailsPage.vue';
import AdminCustomersPage from './pages/admin/AdminCustomersPage.vue';
import AdminDashboardPage from './pages/admin/AdminDashboardPage.vue';
import AdminLoginPage from './pages/admin/AdminLoginPage.vue';
import AdminOrdersPage from './pages/admin/AdminOrdersPage.vue';
import AdminProductsPage from './pages/admin/AdminProductsPage.vue';

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

const adminStats = [
    { label: 'Revenue', value: '$12,480', note: '+18% this month', icon: 'revenue' },
    { label: 'Orders', value: '186', note: '24 pending proof', icon: 'orders' },
    { label: 'Products', value: '64', note: '8 low stock', icon: 'products' },
    { label: 'Customers', value: '1,248', note: '42 new this week', icon: 'customers' },
];

const adminOrders = [
    { id: 'SHC-1048', customer: 'Avery Stone', items: 'Welcome Box x2', status: 'Proofing', statusTone: 'warning', total: 184 },
    { id: 'SHC-1047', customer: 'Maya Chen', items: 'Logo Hoodie x12', status: 'Production', statusTone: 'info', total: 576 },
    { id: 'SHC-1046', customer: 'Noah Brooks', items: 'Desk Identity Kit x4', status: 'Ready', statusTone: 'success', total: 256 },
    { id: 'SHC-1045', customer: 'Olivia Hart', items: 'Orbit Mug x24', status: 'Shipped', statusTone: 'success', total: 432 },
    { id: 'SHC-1044', customer: 'Liam Carter', items: 'Laser Bottle Pro x10', status: 'Payment due', statusTone: 'danger', total: 340 },
];

const adminCustomers = [
    { name: 'Avery Stone', email: 'avery@example.com', orders: 8, spent: 1460, status: 'Active', statusTone: 'success' },
    { name: 'Maya Chen', email: 'maya@example.com', orders: 5, spent: 1128, status: 'Active', statusTone: 'success' },
    { name: 'Noah Brooks', email: 'noah@example.com', orders: 3, spent: 624, status: 'New', statusTone: 'info' },
    { name: 'Olivia Hart', email: 'olivia@example.com', orders: 12, spent: 2890, status: 'VIP', statusTone: 'warning' },
    { name: 'Liam Carter', email: 'liam@example.com', orders: 2, spent: 340, status: 'Payment due', statusTone: 'danger' },
];

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

const adminPages = [
    { path: 'admin-login', title: 'Admin Login', type: 'admin-login' },
    { path: 'admin', title: 'Dashboard', type: 'admin-dashboard' },
    { path: 'admin-products', title: 'Admin Products', type: 'admin-products' },
    { path: 'admin-orders', title: 'Admin Orders', type: 'admin-orders' },
    { path: 'admin-customers', title: 'Admin Customers', type: 'admin-customers' },
];

const allPages = [...pageGroups.flatMap((group) => group.links), ...adminPages];
const categories = ['All', ...new Set(products.map((product) => product.category))];
const featuredProduct = products[0];

const currentPage = computed(() => allPages.find((page) => page.path === route.value) ?? allPages[0]);
const cartTotal = computed(() => cart.value.reduce((sum, product) => sum + product.price * product.quantity, 0));
const cartCount = computed(() => cart.value.reduce((sum, product) => sum + product.quantity, 0));
const isAdminPage = computed(() => currentPage.value.type.startsWith('admin-'));

const pageComponent = computed(() => {
    if (currentPage.value.type === 'admin-login') {
        return AdminLoginPage;
    }

    if (currentPage.value.type === 'admin-dashboard') {
        return AdminDashboardPage;
    }

    if (currentPage.value.type === 'admin-products') {
        return AdminProductsPage;
    }

    if (currentPage.value.type === 'admin-orders') {
        return AdminOrdersPage;
    }

    if (currentPage.value.type === 'admin-customers') {
        return AdminCustomersPage;
    }

    if (currentPage.value.type === 'home') {
        return HomePage;
    }

    if (['shop', 'products', 'deals', 'new-arrivals', 'best-sellers', 'search-results'].includes(currentPage.value.type)) {
        return CatalogPage;
    }

    if (currentPage.value.type === 'product-details') {
        return ProductDetailsPage;
    }

    if (currentPage.value.type === 'categories') {
        return CategoriesPage;
    }

    if (currentPage.value.type === 'collections') {
        return CollectionsPage;
    }

    if (['cart', 'checkout', 'payment', 'confirmation', 'track'].includes(currentPage.value.type)) {
        return CheckoutPage;
    }

    if (['auth-login', 'auth-register', 'auth-forgot'].includes(currentPage.value.type)) {
        return AuthPage;
    }

    if (['account', 'profile', 'orders', 'wishlist', 'addresses'].includes(currentPage.value.type)) {
        return AccountPage;
    }

    if (['contact', 'support'].includes(currentPage.value.type)) {
        return ContactPage;
    }

    if (currentPage.value.type === 'faq') {
        return FaqPage;
    }

    if (['blog', 'careers', 'policy', 'info'].includes(currentPage.value.type)) {
        return InfoPage;
    }

    return ExtraPage;
});

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

const currentPageProps = computed(() => {
    if (currentPage.value.type === 'admin-dashboard') {
        return { stats: adminStats, orders: adminOrders };
    }

    if (currentPage.value.type === 'admin-products') {
        return { products };
    }

    if (currentPage.value.type === 'admin-orders') {
        return { orders: adminOrders };
    }

    if (currentPage.value.type === 'admin-customers') {
        return { customers: adminCustomers };
    }

    if (currentPage.value.type === 'home') {
        return { products, logoUrl };
    }

    if (['shop', 'products', 'deals', 'new-arrivals', 'best-sellers', 'search-results'].includes(currentPage.value.type)) {
        return {
            page: currentPage.value,
            products: pageProducts.value,
            categories,
            logoUrl,
            searchQuery: searchQuery.value,
            activeCategory: activeCategory.value,
        };
    }

    if (currentPage.value.type === 'product-details') {
        return { product: featuredProduct, logoUrl };
    }

    if (currentPage.value.type === 'categories') {
        return { page: currentPage.value, categories, products };
    }

    if (['cart', 'checkout', 'payment', 'confirmation', 'track'].includes(currentPage.value.type)) {
        return { page: currentPage.value, cart: cart.value, cartTotal: cartTotal.value };
    }

    return { page: currentPage.value };
});

function normalizeHash() {
    if (window.location.pathname.startsWith('/admin')) {
        const adminSlug = window.location.pathname.replace(/^\/admin\/?/, '').replace(/\/$/, '');

        if (!adminSlug) {
            return 'admin';
        }

        if (['login', 'products', 'orders', 'customers'].includes(adminSlug)) {
            return `admin-${adminSlug}`;
        }

        return 'admin';
    }

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
    <main class="min-h-screen bg-[var(--page-bg)] text-[var(--ink)]">
        <header class="app-header sticky top-0 z-30 backdrop-blur">
            <div class="mx-auto flex max-w-[1920px] items-center justify-between px-5 py-4 lg:px-10 2xl:px-14">
                <a class="flex items-center gap-3" href="#/home" aria-label="Star Hub Customize home">
                    <img class="h-10 w-10 rounded-md object-cover" :src="logoUrl" alt="Star Hub Customize logo">
                    <span class="text-sm font-semibold uppercase tracking-[0.18em]">Star Hub Customize</span>
                </a>

                <nav class="hidden items-center gap-6 text-sm font-medium text-[var(--muted)] lg:flex">
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

            <nav v-if="menuOpen" class="mx-5 grid max-h-[70vh] gap-5 overflow-auto border-t border-[var(--line)] py-4 text-sm lg:hidden">
                <section v-for="group in pageGroups" :key="group.title">
                    <h3 class="mb-2 text-xs font-bold uppercase tracking-[0.18em] text-[var(--soft-text)]">{{ group.title }}</h3>
                    <div class="grid grid-cols-2 gap-2">
                        <a v-for="page in group.links" :key="page.path" class="mobile-link" :href="`#/${page.path}`">{{ page.title }}</a>
                    </div>
                </section>
            </nav>
        </header>

        <div
            class="mx-auto grid max-w-[1920px] gap-8 px-5 py-8 lg:px-10 2xl:px-14"
            :class="isAdminPage ? '' : 'lg:grid-cols-[280px_1fr] 2xl:grid-cols-[310px_1fr]'"
        >
            <aside v-if="!isAdminPage" class="side-nav hidden lg:block">
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
                <component
                    :is="pageComponent"
                    v-bind="currentPageProps"
                    @add-to-cart="addToCart"
                    @update-quantity="updateQuantity"
                    @update:activeCategory="activeCategory = $event"
                    @update:searchQuery="searchQuery = $event"
                />
            </div>
        </div>

        <footer class="border-t border-[var(--line)] bg-[var(--surface)]">
            <div class="mx-auto flex max-w-[1920px] flex-col gap-3 px-5 py-6 text-sm text-[var(--muted)] md:flex-row md:items-center md:justify-between lg:px-10 2xl:px-14">
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
