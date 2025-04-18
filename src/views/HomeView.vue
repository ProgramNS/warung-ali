<script setup>
import NavigationHome from '@/components/navigation/NavigationHome.vue'
import GlobalBtn from '@/components/button/GlobalBtn.vue'
</script>

<template>
    <header>
        <NavigationHome />
    </header>
    <main>
        <section id="Home" class="bg-yellow-50 h-screen flex items-center justify-center">
            <div class="text-center">
                <h1 class="text-4xl font-bold text-yellow-700">Welcome to Ali Catering</h1>
                <p class="mt-4 text-lg text-gray-600">Your one-stop solution for all catering needs.</p>
                <GlobalBtn />
            </div>
        </section>

        <section id="About" class="bg-white h-screen flex items-center justify-center">
            <div class="text-center">
                <h2 class="text-3xl font-bold text-yellow-700">About Us</h2>
                <p class="mt-4 text-lg text-gray-600">We provide the best catering services in town.</p>
            </div>
        </section>

        <section id="ContactUs" class="bg-yellow-50 h-screen flex items-center justify-center">
            <div class="text-center">
                <h2 class="text-3xl font-bold text-yellow-700">Contact Us</h2>
                <p class="mt-4 text-lg text-gray-600">Get in touch with us for your catering needs.</p>
            </div>
        </section>

        <section id="Order" class="bg-white h-screen flex items-center justify-center">
            <div class="text-center">
                <h2 class="text-3xl font-bold text-yellow-700">Order Now</h2>
                <p class="mt-4 text-lg text-gray-600">Place your order today!</p>
            </div>
        </section>

        <section id="Footer" class="bg-yellow-50 h-screen flex items-center justify-center">
            <div class="text-center">
                <h2 class="text-3xl font-bold text-yellow-700">Footer</h2>
                <p class="mt-4 text-lg text-gray-600">Thank you for visiting our website.</p>
            </div>
        </section>
    </main>
</template>