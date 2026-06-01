<script setup>
import { bugs } from "./data/bugs";
</script>

<template>
  <div class="container">
    <header>
      <div class="logo">🐞</div>

      <h1>QAce Bug Lab</h1>

      <p>Catch, classify and manage software bugs.</p>
    </header>

    <main>
      <h2>Bug Dashboard</h2>

      <div class="cards-grid">
        <div class="bug-card" v-for="bug in bugs" :key="bug.id">
          <div class="bug-icon">{{ bug.emoji }}</div>

          <h3>{{ bug.name }}</h3>

          <p class="severity">{{ bug.severity }}</p>

          <p>{{ bug.description }}</p>

          <button>View Details</button>
        </div>
      </div>
    </main>
  </div>
</template>

<style>
body {
  margin: 0;
  font-family: Arial, Helvetica, sans-serif;
  background: #f5f7fa;
}

.container {
  max-width: 1200px;
  margin: 40px auto;
  padding: 20px;
}

header {
  text-align: center;
  margin-bottom: 50px;
}

.logo {
  font-size: 3rem;
  margin-bottom: 15px;
}

h1 {
  font-size: 3rem;
  margin: 0 0 20px 0;
}

header p {
  margin-top: 0;
  color: #666;
}

main h2 {
  text-align: center;
  margin-bottom: 24px;
}

.cards-grid {
  display: flex;
  justify-content: center;
  gap: 24px;
  flex-wrap: wrap;
}

.bug-card {
  width: 280px;
  background: white;
  border-radius: 12px;
  padding: 30px 20px 24px;
  text-align: center;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.08);
}

.bug-icon {
  font-size: 3rem;
  margin-bottom: 15px;
}

.bug-card h3 {
  margin: 0 0 20px 0;
  color: #555;
}

.severity {
  font-weight: bold;
  color: #c62828;
}

button {
  margin-top: 10px;
  padding: 8px 16px;
  cursor: pointer;
}
</style>
