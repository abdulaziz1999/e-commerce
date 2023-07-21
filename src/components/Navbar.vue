<template>
    <div class="nav">
        <div class="navbar bg-base-100">
            <div class="navbar-start">
                <div class="dropdown">
                    <label tabindex="0" class="btn btn-ghost lg:hidden">
                        <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24"
                            stroke="currentColor">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                                d="M4 6h16M4 12h8m-8 6h16" />
                        </svg>
                    </label>
                    <ul tabindex="0"
                        class="menu menu-sm dropdown-content mt-3 z-[1] p-2 shadow bg-base-100 rounded-box w-52">
                        <li class=""><router-link to="/">Beranda</router-link></li>
                        <li class=""><router-link to="/products">Products</router-link></li>
                    </ul>
                </div>
                <router-link to="/" class="btn btn-ghost normal-case text-4xl font-bold text-success">SePatu</router-link>
            </div>
            <div class="navbar-center hidden lg:flex">
                <ul class="menu menu-horizontal px-1">
                    <li class=""><router-link to="/">Beranda</router-link></li>
                    <li class=""><router-link to="/products">Products</router-link></li>
                </ul>
            </div>
            <div class="navbar-end sm:px-5 md:px-5">
                <div class="dropdown dropdown-end">
                    <label tabindex="0" class="btn btn-ghost btn-circle">
                        <div class="indicator">
                            <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24"
                                stroke="currentColor">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                                    d="M3 3h2l.4 2M7 13h10l4-8H5.4M7 13L5.4 5M7 13l-2.293 2.293c-.63.63-.184 1.707.707 1.707H17m0 0a2 2 0 100 4 2 2 0 000-4zm-8 2a2 2 0 11-4 0 2 2 0 014 0z" />
                            </svg>
                            <span class="badge badge-sm bg-success text-white indicator-item">
                                {{ countCart ? countCart.length : carts.length }}
                            </span>
                        </div>
                    </label>
                    <div tabindex="0" class="mt-3 z-[1] card card-compact dropdown-content w-52 bg-base-100 shadow">
                        <div class="card-body">
                            <span class="font-bold text-lg">{{ countCart ? countCart.length : carts.length }} Items</span>
                            <span class="text-success">Total: Rp. {{ totalItem ? totalItem : cartTotal }}</span>
                            <div class="card-actions">
                                <router-link to="/cart" class="btn btn-sm bg-success font-serif text-white btn-block">View
                                    cart</router-link>
                            </div>
                        </div>
                    </div>
                </div>
                <button class="btn btn-ghost btn-circle">
                    <div class="indicator">
                        <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24"
                            stroke="currentColor">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                                d="M15 17h5l-1.405-1.405A2.032 2.032 0 0118 14.158V11a6.002 6.002 0 00-4-5.659V5a2 2 0 10-4 0v.341C7.67 6.165 6 8.388 6 11v3.159c0 .538-.214 1.055-.595 1.436L4 17h5m6 0v1a3 3 0 11-6 0v-1m6 0H9" />
                        </svg>
                        <span class="badge badge-xs badge-success indicator-item text-white">1</span>
                    </div>
                </button>
                <!-- <div class="btn btn-ghost btn-circle hidden lg:flex" > -->
                <label class="swap swap-rotate btn btn-ghost btn-circle md:flex-wrap">
                    <input type="checkbox" id="toggleTheme" @change="handleToggle"
                        :checked="theme == 'light' ? false : true" class="hidden" />
                    <svg class="swap-on fill-current w-6 h-6" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24">
                        <path
                            d="M5.64,17l-.71.71a1,1,0,0,0,0,1.41,1,1,0,0,0,1.41,0l.71-.71A1,1,0,0,0,5.64,17ZM5,12a1,1,0,0,0-1-1H3a1,1,0,0,0,0,2H4A1,1,0,0,0,5,12Zm7-7a1,1,0,0,0,1-1V3a1,1,0,0,0-2,0V4A1,1,0,0,0,12,5ZM5.64,7.05a1,1,0,0,0,.7.29,1,1,0,0,0,.71-.29,1,1,0,0,0,0-1.41l-.71-.71A1,1,0,0,0,4.93,6.34Zm12,.29a1,1,0,0,0,.7-.29l.71-.71a1,1,0,1,0-1.41-1.41L17,5.64a1,1,0,0,0,0,1.41A1,1,0,0,0,17.66,7.34ZM21,11H20a1,1,0,0,0,0,2h1a1,1,0,0,0,0-2Zm-9,8a1,1,0,0,0-1,1v1a1,1,0,0,0,2,0V20A1,1,0,0,0,12,19ZM18.36,17A1,1,0,0,0,17,18.36l.71.71a1,1,0,0,0,1.41,0,1,1,0,0,0,0-1.41ZM12,6.5A5.5,5.5,0,1,0,17.5,12,5.51,5.51,0,0,0,12,6.5Zm0,9A3.5,3.5,0,1,1,15.5,12,3.5,3.5,0,0,1,12,15.5Z" />
                    </svg>
                    <svg class="swap-off fill-current w-6 h-6" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24">
                        <path
                            d="M21.64,13a1,1,0,0,0-1.05-.14,8.05,8.05,0,0,1-3.37.73A8.15,8.15,0,0,1,9.08,5.49a8.59,8.59,0,0,1,.25-2A1,1,0,0,0,8,2.36,10.14,10.14,0,1,0,22,14.05,1,1,0,0,0,21.64,13Zm-9.5,6.69A8.14,8.14,0,0,1,7.08,5.22v.27A10.15,10.15,0,0,0,17.22,15.63a9.79,9.79,0,0,0,2.1-.22A8.11,8.11,0,0,1,12.14,19.73Z" />
                    </svg>
                </label>
                <!-- </div> -->
                <div class="dropdown dropdown-end">
                    <label tabindex="0" class="btn btn-ghost btn-circle avatar">
                        <div class="w-10 rounded-full">
                            <img src="https://daisyui.com/images/stock/photo-1534528741775-53994a69daeb.jpg" />
                        </div>
                    </label>
                    <ul tabindex="0"
                        class="menu menu-sm dropdown-content mt-3 z-[1] p-2 shadow bg-base-100 rounded-box w-52">
                        <li>
                            <a class="justify-between">
                                Profile
                                <span class="badge badge-success">New</span>
                            </a>
                        </li>
                        <li><a>Settings</a></li>
                        <li><a>Logout</a></li>
                    </ul>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import { defineComponent, onMounted, watch } from 'vue';
import { useCartStore } from '../router/store.js';
import axios from 'axios'
export default defineComponent({
    name: 'NavbarComp',
    data() {
        return {
            carts: [],
            theme: localStorage.getItem('theme') ? localStorage.getItem('theme') : 'light'
        }
    },
    props: ['countCart', 'sumHarga', 'totalItem'],
    methods: {
        setCart(data) {
            this.carts = data
        },
        setTheme(data) {
            this.theme = data
            this.setLocalTheme(data)
        },
        handleToggle(e) {
            if (e.target.checked) {
                this.setTheme('dark')
            } else {
                this.setTheme('light')
            }
        },
        setLocalTheme(data) {
            document.querySelector('html').setAttribute('data-theme', data)
            localStorage.setItem('theme', data)
        },
        setLocalThemeDefault() {
            localStorage.setItem('theme', this.theme)
            const localTheme = localStorage.getItem('theme')
            document.querySelector('html').setAttribute('data-theme', localTheme)
        },
        async getAllCart() {
            await axios.get('http://localhost:3000/carts')
                .then((res) => {
                    this.setCart(res.data)
                }).catch((err) => {
                    console.log(err)
                })
        }
    },
    mounted() {
        this.getAllCart()
        this.setLocalThemeDefault()
    },
    setup() {
        const cartStore = useCartStore();

        const setCart = (data) => {
            cartStore.items = data;
        };

        const getAllCart = async() => {
            await axios
                .get('http://localhost:3000/carts')
                .then((res) => {
                    setCart(res.data);
                })
                .catch((err) => {
                    console.log(err);
                });
        };

        const updateTotal = () => {
            cartStore.updateTotal();
        };

        // Watch for changes in cartStore.items
        watch(() => cartStore.items, () => {
            updateTotal();
        });

        // Load data from local storage when the component is mounted
        onMounted(() => {
            cartStore.loadFromLocalStorage();
        });

        // Called when the component is mounted
        getAllCart();

        return {
            cartItems: cartStore.cartItems,
            cartTotal: cartStore.total,
            cartItemCount: cartStore.cartItemCount,
            cartStore,
        };
    }
})
</script>

<style></style>