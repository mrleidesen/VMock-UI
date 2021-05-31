<template>
  <div class="w-full h-screen flex flex-col overflow-hidden">
    <Header />
    <main class="w-full flex-1 overflow-auto bg-gray-50 box-border p-2">
      <router-view></router-view>
    </main>
    <Footer />
  </div>
</template>

<script>
import Header from '@/components/Header.vue'
import Footer from '@/components/Footer.vue'

export default {
  components: {
    Header, Footer
  },
}
</script>
