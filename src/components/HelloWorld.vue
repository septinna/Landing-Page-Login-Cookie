<template>
  <div class="hello">
    <nav class="navbar navbar-light bg-light">
      <div class="container">
        <a class="navbar-brand" href="#">
          <img alt="Vue logo" src="../assets/login.png" width="90" height="90">
        </a>
        <div>
          <h1 class="text-warning">Selamat datang kembali!</h1>
          <p>Masuklah untuk melanjutkan petualangan cookie Anda. Website ini punya Septinna Choirunisa.</p>
          <p>Tak perlu ragu, masuklah ke dunia kami yang penuh dengan kelezatan. Mari nikmati setiap gigitan dengan membawa sejuta kenangan bersama kami.</p>
        </div>
        <button type="button" class="btn btn-primary btn-lg" data-bs-toggle="modal" data-bs-target="#loginModal">
          Login
        </button>
      </div>
    </nav>

    <LoginComponent />    <!--Component-->
    <div id="rr">                                                                     <!--Implementasi Transition-->
      <button class="btn btn-primary btn-lg" @click="toggleShow" style="margin-right: 100px;">&#9776;</button>
      <transition name="fade">
        <a v-if="show" href="/home">
          <p>Home</p>
        </a>
      </transition>
      <transition name="fade">
        <a v-if="show" href="/about">
          <p>About</p>
        </a>
      </transition>
      <transition name="fade">
        <a v-if="show" href="/contact">
          <p>Contact</p>
        </a>
      </transition>
    </div>
    <button type="button" class="btn btn-primary btn-lg" onclick="window.location.href='formulir.html'" style="margin-right: 100px;">
      Pesan
    </button>
    <button type="button" class="btn btn-primary btn-lg" onclick="window.location.href='komentar.html'">
      Review
    </button>
    <transition name="fade">                                                                <!--Mode Transisi-->
      <div id="oke">
        <button class="btn btn-success btn-lg" @click="toggleShowOke">Klik</button>
        <transition v-bind:name="showOke ? 'fade-slide' : 'fade'" mode="out-in">
          <div v-if="showOke" class="image-container">
            <img src="../assets/kupon.png" alt="Potongan 50%">
          </div>
          <p v-else>Ingin Voucher? Klik sekali lagi!</p>
        </transition>
      </div>
    </transition>
  </div>
</template>

<script>
import LoginComponent from './LoginComponent.vue' // Component

export default {
  name: 'HelloWorld',
  components: {
    LoginComponent
  },
  data () {
    return {
      items: ['Belanja', 'Alamat', 'Chat Admin'],
      showApp: false,
      showOke: false,
      currentIndex: 0,
      show: false
    }
  },
  computed: { // Penggunaan Computed Properties
    jumlahItems () {
      return this.items.length
    }
  },
  methods: {
    toggleShowApp () {
      this.showApp = !this.showApp
    },
    toggleShowOke () {
      this.showOke = !this.showOke
    },
    addItem () {
      const newItem = this.items[this.currentIndex]
      this.items.push(newItem)
      this.currentIndex = (this.currentIndex + 1) % this.items.length
    },
    toggleShow () {
      this.show = !this.show
    }
  }
}
</script>

<style scoped>
  #rr {
    display: inline-block;
    vertical-align: top;
    margin-left: 190px;
    text-align: left;
  }

  #oke {
    display: inline-block;
    vertical-align: top;
    margin-left: 100px;
    text-align: left;
    position: relative;
  }

  .image-container {
    display: flex;
    justify-content: left;
    align-items: left;
  }

  .fade-enter-active,
  .fade-leave-active {
    transition: opacity 0.5s ease;
  }

  .fade-enter,
  .fade-leave-to {
    opacity: 0;
  }

  .fade-slide-enter-active,
  .fade-slide-leave-active {
    transition: opacity 0.5s ease, transform 0.5s ease;
  }

  .fade-slide-enter,
  .fade-slide-leave-to {
    opacity: 0;
    transform: translateY(-20px);
  }
</style>
