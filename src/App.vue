<script setup>
import { ref, onMounted, onUnmounted } from "vue";
import { Heart, CalendarDays, MapPin, ChevronDown } from "lucide-vue-next";

const isOpened = ref(false);
const isAnimating = ref(false);

function openEnvelope() {
  if (isAnimating.value || isOpened.value) return;
  isAnimating.value = true;
  // Wait for envelope open animation, then reveal the invitation
  setTimeout(() => {
    isOpened.value = true;
  }, 1400);
}

const couple = {
  groom: "Mohd. Nabil",
  bride: "Nur Nabillah",
  date: "30 November 2026",
  venue: "(put location here)",
};

const weddingDate = new Date("2026-11-30T10:00:00+08:00");

const countdown = ref({
  days: 0,
  hours: 0,
  minutes: 0,
  seconds: 0,
});

let countdownTimer;

function updateCountdown() {
  const remaining = Math.max(0, weddingDate.getTime() - Date.now());

  countdown.value = {
    days: Math.floor(remaining / 86400000),
    hours: Math.floor((remaining % 86400000) / 3600000),
    minutes: Math.floor((remaining % 3600000) / 60000),
    seconds: Math.floor((remaining % 60000) / 1000),
  };
}

onMounted(() => {
  updateCountdown();
  countdownTimer = setInterval(updateCountdown, 1000);
});

onUnmounted(() => {
  clearInterval(countdownTimer);
});
</script>

<template>
  <main class="wedding">
    <Transition name="envelope-fade">
      <section v-if="!isOpened" class="envelope-screen">
        <div class="envelope-card">
          <p class="envelope-bismillah">
            بِسْمِ اللَّهِ الرَّحْمَٰنِ الرَّحِيمِ
          </p>
          <p class="envelope-kicker">TO CELEBRATE A BEAUTIFUL BEGINNING</p>

          <div class="envelope-art" :class="{ opened: isAnimating }">
            <div class="envelope-back"></div>
            <div class="envelope-letter">
              <span class="letter-monogram">N <i>&</i> N</span>
              <span class="letter-caption">WEDDING INVITATION</span>
            </div>
            <div class="envelope-flap"></div>
            <div class="envelope-front"></div>
            <button
              class="wax-seal"
              @click="openEnvelope"
              aria-label="Open invitation"
            >
              <i>N & N</i>
            </button>
          </div>

          <h1 class="envelope-title">You're Invited</h1>
          <p class="envelope-subtitle">Mohd. Nabil & Nur Nabillah</p>
          <p class="envelope-date">30 · 11 · 2026</p>

          <p class="envelope-note">A special invitation, made with love.</p>
        </div>
      </section>
    </Transition>

    <section v-show="isOpened" class="countdown-section">
      <p class="eyebrow dark">COUNTING DOWN TO FOREVER</p>
      <h2>Our Day Is Almost Here</h2>
      <p class="countdown-subtitle">
        Every second brings us closer to our special day.
      </p>

      <div class="countdown-grid">
        <div class="countdown-box">
          <strong>{{ countdown.days }}</strong>
          <span>DAYS</span>
        </div>
        <div class="countdown-box">
          <strong>{{ countdown.hours }}</strong>
          <span>HOURS</span>
        </div>
        <div class="countdown-box">
          <strong>{{ countdown.minutes }}</strong>
          <span>MINUTES</span>
        </div>
        <div class="countdown-box">
          <strong>{{ countdown.seconds }}</strong>
          <span>SECONDS</span>
        </div>
      </div>

      <p class="countdown-date">30 NOVEMBER 2026 · 10:00 AM</p>
    </section>

    <div v-show="isOpened" class="wedding-content">
      <nav class="navigation">
        <a href="#" class="logo">N <span>&</span> N</a>
        <a href="#invitation" class="nav-link">THE INVITATION</a>
      </nav>
      <section class="hero">
        <div class="hero-image"></div>
        <div class="hero-shade"></div>

        <div class="hero-content">
          <div class="islamic-mark">۞</div>
          <p class="bismillah">بِسْمِ اللَّهِ الرَّحْمَٰنِ الرَّحِيمِ</p>
          <p class="eyebrow">THE BEGINNING OF FOREVER</p>

          <h1>
            {{ couple.groom }}
            <span class="ampersand">&</span>
            {{ couple.bride }}
          </h1>

          <div class="gold-divider">
            <span></span>
            <Heart :size="15" />
            <span></span>
          </div>

          <p class="wedding-date">{{ couple.date }}</p>
          <p class="wedding-venue">{{ couple.venue }}</p>

          <a class="discover-button" href="#invitation">
            DISCOVER OUR INVITATION
            <ChevronDown :size="15" />
          </a>
        </div>

        <p class="vertical-label">WITH LOVE & BLESSINGS</p>
      </section>

      <section class="invitation" id="invitation">
        <p class="eyebrow dark">A JOYFUL BEGINNING</p>
        <h2>A celebration of love,<br />faith & forever.</h2>

        <div class="small-ornament">❦</div>

        <p class="invitation-copy">
          With the blessings of Allah SWT and our beloved families, we joyfully
          invite you to celebrate the beginning of our new chapter together.
        </p>

        <div class="couple-names">
          <span>{{ couple.groom }}</span>
          <Heart :size="20" />
          <span>{{ couple.bride }}</span>
        </div>

        <div class="event-preview">
          <div class="event-item">
            <CalendarDays :size="22" />
            <p class="event-label">THE DATE</p>
            <p>{{ couple.date }}</p>
          </div>

          <div class="event-item">
            <MapPin :size="22" />
            <p class="event-label">THE VENUE</p>
            <p>{{ couple.venue }}</p>
          </div>
        </div>
      </section>

      <footer>
        <p>بَارَكَ اللَّهُ لَكُمَا</p>
        <div class="footer-names">{{ couple.groom }} & {{ couple.bride }}</div>
        <p class="footer-date">30 · 11 · 2026</p>
      </footer>
    </div>
  </main>
</template>

<style>
@import url("https://fonts.googleapis.com/css2?family=Cormorant+Garamond:wght@400;500;600&family=DM+Sans:wght@300;400;500;600&display=swap");

:root {
  font-family: "DM Sans", sans-serif;
  color: #354737;
  background: #f7f3eb;
  font-synthesis: none;
  text-rendering: optimizeLegibility;
  scroll-behavior: smooth;
}

* {
  box-sizing: border-box;
}

body {
  margin: 0;
  min-width: 320px;
}

a {
  color: inherit;
  text-decoration: none;
}

.wedding {
  overflow: hidden;
  background: #f7f3eb;
}

.wedding-content {
  position: relative;
}

.navigation {
  position: absolute;
  top: 0;
  left: 0;
  z-index: 5;
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 24px 7%;
  color: #fffaf0;
  border-bottom: 1px solid rgba(255, 255, 255, 0.22);
}

.logo {
  font-family: "Cormorant Garamond", serif;
  font-size: 30px;
  letter-spacing: 2px;
}

.logo span {
  color: #d6bd88;
  font-style: italic;
}

.nav-link {
  font-size: 9px;
  letter-spacing: 2px;
}

.hero {
  min-height: 720px;
  min-height: 100svh;
  position: relative;
  display: grid;
  place-items: center;
  color: #fffaf0;
  background: #354737;
}

.hero-image,
.hero-shade {
  position: absolute;
  inset: 0;
}

.hero-image {
  background-image: url("https://images.unsplash.com/photo-1519741497674-611481863552?auto=format&fit=crop&w=2000&q=90");
  background-size: cover;
  background-position: center;
  transform: scale(1.02);
}

.hero-shade {
  background: linear-gradient(
    180deg,
    rgba(25, 39, 29, 0.58),
    rgba(25, 39, 29, 0.72)
  );
}

.hero-content {
  position: relative;
  z-index: 2;
  text-align: center;
  padding: 120px 20px 80px;
  width: 100%;
  animation: appear 1s ease both;
}

.islamic-mark {
  font-size: 46px;
  color: #d6bd88;
  margin-bottom: 12px;
}

.bismillah {
  font-size: 19px;
  color: #f0dfb9;
  margin: 0 0 38px;
}

.eyebrow {
  font-size: 10px;
  letter-spacing: 4px;
  line-height: 1.9;
}

.hero .eyebrow {
  color: #e0cda2;
}

.hero h1 {
  display: flex;
  flex-direction: column;
  gap: 0;
  font-family: "Cormorant Garamond", serif;
  font-size: clamp(72px, 12vw, 128px);
  font-weight: 400;
  line-height: 0.77;
  margin: 35px 0;
}

.ampersand {
  color: #d6bd88;
  font-size: 0.56em;
  font-style: italic;
  line-height: 1.25;
}

.gold-divider {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 15px;
  color: #d6bd88;
  margin: 30px 0;
}

.gold-divider span {
  width: 45px;
  height: 1px;
  background: #d6bd88;
}

.wedding-date {
  font-size: 12px;
  letter-spacing: 4px;
}

.wedding-venue {
  font-size: 12px;
  color: #e1ddcf;
  margin-top: 10px;
}

.discover-button {
  margin-top: 32px;
  padding: 15px 23px;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 13px;
  border: 1px solid rgba(224, 205, 162, 0.8);
  font-size: 9px;
  letter-spacing: 2px;
  transition:
    background 0.25s ease,
    color 0.25s ease;
}

.discover-button:hover {
  background: #d6bd88;
  color: #354737;
}

.vertical-label {
  position: absolute;
  right: 24px;
  top: 50%;
  writing-mode: vertical-rl;
  font-size: 8px;
  letter-spacing: 3px;
  color: rgba(255, 250, 240, 0.75);
}

.invitation {
  padding: 110px 22px;
  text-align: center;
  max-width: 850px;
  margin: auto;
}

.dark {
  color: #a38a56;
}

.invitation h2 {
  font-family: "Cormorant Garamond", serif;
  font-weight: 400;
  font-size: clamp(42px, 7vw, 65px);
  line-height: 1.02;
  margin: 22px 0;
}

.small-ornament {
  color: #b69b63;
  font-size: 30px;
  margin: 28px 0;
}

.invitation-copy {
  max-width: 520px;
  margin: auto;
  color: #77776a;
  font-size: 13px;
  line-height: 2.1;
}

.couple-names {
  margin: 42px auto;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-wrap: wrap;
  gap: 18px;
  color: #b3975e;
}

.couple-names span {
  font-family: "Cormorant Garamond", serif;
  font-size: clamp(34px, 6vw, 48px);
}

.event-preview {
  display: grid;
  grid-template-columns: repeat(2, minmax(0, 1fr));
  border-top: 1px solid #ddd4c2;
  border-bottom: 1px solid #ddd4c2;
  margin-top: 55px;
}

.event-item {
  padding: 35px 15px;
  color: #52624d;
}

.event-item + .event-item {
  border-left: 1px solid #ddd4c2;
}

.event-item svg {
  color: #b3975e;
}

.event-item p {
  font-size: 12px;
  line-height: 1.8;
}

.event-label {
  font-size: 9px !important;
  letter-spacing: 2px;
  color: #9c8559;
  margin-top: 18px;
}

footer {
  text-align: center;
  padding: 45px 20px;
  background: #354737;
  color: #f7f3eb;
}

footer > p:first-child {
  color: #d6bd88;
  font-size: 21px;
}

.footer-names {
  font-family: "Cormorant Garamond", serif;
  font-size: 34px;
  margin: 14px 0;
}

.footer-date {
  font-size: 10px;
  letter-spacing: 3px;
  color: #d6bd88;
}

@keyframes appear {
  from {
    opacity: 0;
    transform: translateY(15px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@media (max-width: 600px) {
  .navigation {
    padding: 20px;
  }

  .hero {
    min-height: 680px;
    min-height: 100svh;
  }

  .hero h1 {
    font-size: 76px;
  }

  .bismillah {
    font-size: 17px;
  }

  .vertical-label {
    right: 9px;
    font-size: 7px;
  }

  .invitation {
    padding: 80px 22px;
  }

  .event-preview {
    grid-template-columns: 1fr;
  }

  .event-item + .event-item {
    border-left: none;
    border-top: 1px solid #ddd4c2;
  }
}

@media (prefers-reduced-motion: reduce) {
  *,
  *::before,
  *::after {
    animation: none !important;
    scroll-behavior: auto !important;
    transition: none !important;
  }
}

.envelope-screen {
  position: fixed;
  inset: 0;
  z-index: 20;
  display: grid;
  place-items: center;
  overflow-y: auto;
  padding: 35px 20px;
  background: radial-gradient(ellipse at top, #fffdf7 0%, #f1e9d8 75%), #f7f3eb;
}

.envelope-card {
  width: min(100%, 460px);
  text-align: center;
  padding: 30px 10px;
}

.envelope-bismillah {
  color: #8f7748;
  font-size: 20px;
  margin-bottom: 18px;
}

.envelope-kicker {
  font-size: 9px;
  letter-spacing: 2px;
  color: #8a816d;
  line-height: 1.8;
}

.envelope-art {
  position: relative;
  width: min(310px, 85vw);
  height: 210px;
  margin: 35px auto 28px;
  perspective: 1000px;
  filter: drop-shadow(0 15px 16px rgba(55, 57, 38, 0.12));
}

.envelope-back {
  position: absolute;
  inset: 0;
  background: #d8c6a2;
  border: 1px solid #b49a66;
}

.envelope-letter {
  position: absolute;
  z-index: 1;
  left: 12%;
  right: 12%;
  top: 8%;
  height: 84%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  gap: 12px;
  background: #fffdf7;
  border: 1px solid #d8c8a8;
  transition: transform 1.1s cubic-bezier(0.22, 0.61, 0.36, 1) 0.45s;
}

.letter-monogram {
  font-family: "Cormorant Garamond", serif;
  font-size: 38px;
  color: #354737;
  white-space: nowrap;
  text-align: center;
  line-height: 1;
}

.letter-monogram i {
  color: #b3975e;
}

.letter-caption {
  font-size: 8px;
  letter-spacing: 2px;
  color: #8f7748;
}

.envelope-flap {
  position: absolute;
  z-index: 3;
  inset: 0;
  background: #e8d9b9;
  clip-path: polygon(0 0, 100% 0, 50% 58%);
  transform-origin: top center;
  transition: transform 0.7s ease;
}

.envelope-front {
  position: absolute;
  z-index: 2;
  inset: 0;
  background: #d7c39c;
  clip-path: polygon(0 0, 50% 55%, 100% 0, 100% 100%, 0 100%);
  border-bottom: 1px solid #b49a66;
}

.wax-seal {
  position: absolute;
  z-index: 4;
  left: 50%;
  top: 52%;
  transform: translate(-50%, -50%);
  display: grid;
  place-items: center;
  width: 55px;
  height: 55px;
  border-radius: 50%;
  background: #536347;
  border: 2px solid #d7c39c;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.15);
  color: #fff7e5;
  font-family: "Cormorant Garamond", serif;
  font-size: 17px;
  cursor: pointer;
  padding: 0;
  transition:
    opacity 0.45s ease,
    transform 0.45s ease,
    background 0.2s ease,
    box-shadow 0.2s ease;
}

.wax-seal:hover {
  background: #4b624c;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.25);
}

.wax-seal:focus-visible {
  outline: 2px solid #d7c39c;
  outline-offset: 3px;
}

.wax-seal span {
  color: #d7c39c;
  font-style: italic;
}

.envelope-art.opened .envelope-flap {
  transform: rotateX(180deg);
  z-index: 0;
}

/* Letter rises up out of the envelope */
.envelope-art.opened .envelope-letter {
  transform: translateY(-72%);
}

.envelope-art.opened .wax-seal {
  opacity: 0;
  transform: translate(-50%, -50%) scale(0.4);
  transition-delay: 0s;
}

/* end envelope open states */

.envelope-title {
  font-family: "Cormorant Garamond", serif;
  font-size: 48px;
  font-weight: 400;
  color: #354737;
  margin: 10px 0;
}

.envelope-subtitle {
  color: #8f7748;
  font-family: "Cormorant Garamond", serif;
  font-size: 25px;
  margin: 5px 0;
}

.envelope-date {
  color: #77776a;
  font-size: 10px;
  letter-spacing: 3px;
  margin: 15px 0 25px;
}

.envelope-note {
  font-size: 10px;
  color: #918775;
  margin-top: 20px;
  font-style: italic;
}

.envelope-fade-leave-active {
  transition:
    opacity 0.8s ease,
    transform 0.8s ease;
}

.envelope-fade-leave-to {
  opacity: 0;
  transform: scale(1.04);
}

.countdown-section {
  padding: 85px 20px;
  text-align: center;
  background: #eeeadf;
}

.countdown-section h2 {
  font-family: "Cormorant Garamond", serif;
  font-size: clamp(38px, 6vw, 56px);
  font-weight: 400;
  color: #354737;
  margin: 18px 0;
}

.countdown-subtitle {
  color: #77776a;
  font-size: 12px;
  line-height: 1.8;
}

.countdown-grid {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
  gap: 12px;
  margin: 35px auto;
}

.countdown-box {
  display: flex;
  flex-direction: column;
  justify-content: center;
  gap: 8px;
  width: 105px;
  min-height: 105px;
  border: 1px solid #c7b58f;
  background: rgba(255, 253, 247, 0.55);
}

.countdown-box strong {
  font-family: "Cormorant Garamond", serif;
  font-size: 38px;
  font-weight: 400;
  color: #354737;
}

.countdown-box span {
  font-size: 8px;
  letter-spacing: 2px;
  color: #9c8559;
}

.countdown-date {
  font-size: 9px;
  letter-spacing: 3px;
  color: #8f7748;
}

@media (max-width: 480px) {
  .countdown-box {
    width: calc(50% - 8px);
    max-width: 130px;
  }
}
</style>
