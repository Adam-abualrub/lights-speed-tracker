<script setup>
</script>

<template>
  <main class="homepage">
    <h1 class="remaining-title">Remaining</h1>
    <p class="remaining-subtitle">This week · ends in 4 days</p>

    <section class="remaining-box">
      <h2 class="remaining-amount">Rp 325.000</h2>
      <p class="remaining-detail">of Rp 500.000 · 3 spent</p>
    </section>

    <h2 class="section-label">QUICK LOG</h2>

    <section class="quick-log-box">
      <input class="title-input" type="text" placeholder="Title · e.g. Nasi goreng" />
      <div class="quick-log-categories">
        <button class="category-pill active" type="button">Food</button>
        <button class="category-pill" type="button">Housing</button>
        <button class="category-pill" type="button">Health</button>
      </div>
      <div class="quick-log-row">
        <input class="amount-input" type="text" placeholder="25.000" />
        <button class="save-button" type="button">Save</button>
      </div>
    </section>

    <h2 class="section-label">RECENT</h2>

    <section class="recent-list">
      <div class="recent-item">
        <p>Nasi goreng · Food</p>
        <span>25.000</span>
      </div>
      <div class="recent-item">
        <p>Bus fare · Transport</p>
        <span>15.000</span>
      </div>
    </section>
  </main>
</template>

<style scoped>
.homepage {
  display: flex;
  flex-direction: column;
  gap: 1rem;
  background-color: rgb(245, 245, 243);
  max-width: 420px;
  margin: 0 auto;
  padding: 1rem;
  border-radius: 1.5rem;
}

.remaining-title {
  margin: 0;
  font-size: 2rem;
}

.remaining-subtitle {
  margin: 0;
  color: rgb(140, 140, 140);
}

.remaining-box {
  background-color: white;
  display: flex;
  flex-direction: column;
  padding: 1rem;
  border-radius: 1rem;
}

.remaining-amount {
  margin: 0;
  color: rgb(70, 120, 105);
  font-size: 2.2rem;
}

.remaining-detail {
  margin: 0;
  color: rgb(140, 140, 140);
}

.section-label {
  margin: 0;
  color: rgb(140, 140, 140);
  font-size: 0.9rem;
  font-weight: normal;
}

.quick-log-box {
  background-color: white;
  display: flex;
  flex-direction: column;
  gap: 0.75rem;
  padding: 1rem;
  border-radius: 1rem;
}

.title-input {
  background-color: rgb(245, 245, 243);
  border: none;
  border-radius: 0.75rem;
  padding: 0.75rem;
}

.quick-log-categories {
  display: flex;
  gap: 0.5rem;
}

.category-pill {
  border: none;
  border-radius: 2rem;
  padding: 0.5rem 1rem;
  background-color: rgb(235, 235, 232);
}

.category-pill.active {
  background-color: rgb(62, 107, 94);
  color: white;
}

.quick-log-row {
  display: flex;
  gap: 0.75rem;
}

.amount-input {
  background-color: rgb(245, 245, 243);
  border: none;
  border-radius: 0.75rem;
  padding: 0.75rem;
  width: 50%;
}

.save-button {
  border: none;
  border-radius: 0.75rem;
  background-color: rgb(62, 107, 94);
  color: white;
  width: 50%;
}

.recent-list {
  display: flex;
  flex-direction: column;
  gap: 0.75rem;
}

.recent-item {
  background-color: white;
  display: flex;
  justify-content: space-between;
  padding: 0.75rem 1rem;
  border-radius: 0.75rem;
}

.recent-item p {
  margin: 0;
}
</style>
