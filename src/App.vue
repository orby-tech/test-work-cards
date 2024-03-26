<script setup lang="ts">
import { ref } from 'vue'

const isOpen = ref(false)

const openCard = () => {
  isOpen.value = !isOpen.value
}
</script>

<template>
  <main>
    <div class="table">
      <div class="table-row">
        <div class="card">
          <div class="card-inner"></div>
        </div>
      </div>
      <div class="table-row">
        <div class="card">
          <div class="card-inner" :class="{ 'is-opend': false }">
            <div class="card-front">
              <img src="@/assets/front.png" />
            </div>
            <div class="card-back"><img src="@/assets/back.png" /></div>
          </div>
        </div>
        <div class="card" ref="cardRef">
          <div class="card-inner" :class="{ 'is-opend': isOpen }">
            <div class="card-front">
              <img src="@/assets/front.png" />
            </div>
            <div class="card-back"><img src="@/assets/back.png" /></div>
          </div>
        </div>
        <div class="card">
          <div class="card-inner" :class="{ 'is-opend': false }">
            <div class="card-front">
              <img src="@/assets/front.png" />
            </div>
            <div class="card-back"><img src="@/assets/back.png" /></div>
          </div>
        </div>
      </div>
      <div>
        <button @click="openCard">{{ isOpen ? 'Close' : 'Open' }} Card</button>
      </div>
    </div>
  </main>
</template>

<style scoped>
.table {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 10px;
  width: 100%;
  height: 100vh;
}

.table-row {
  display: flex;
  justify-content: center;
  gap: 10px;
}

.card {
  perspective: 1000px;
}

.card-inner {
  width: 100px;
  height: 150px;
  position: relative;
  transition: 0.6s;
  transform-style: preserve-3d;
  transform: rotateY(-180deg);
}

.card-inner.is-opend {
  transform: rotateY(0deg) translateY(-150px);
}

@media screen and (max-width: 320px) {
  .card-inner {
    width: 50px;
    height: 75px;
  }
}

@media screen and (max-width: 640px) {
  .card-inner.is-opend {
    transform: rotateY(0deg) translateY(-200px) scale(1.5);
  }
}

.card-front,
.card-back {
  width: 100%;
  height: 100%;
  border-radius: 15px;

  position: absolute;
  backface-visibility: hidden;
}

.card-back {
  transform: rotateY(180deg);
}

.card-front > img,
.card-back > img {
  border-radius: 5px;
  max-width: 100%;
  height: 100%;
}
</style>
