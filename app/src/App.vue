<script setup>
import { ref } from "vue";
import { bugs } from "./data/bugs";
import qaceLogo from "./assets/qace-logo.png";

const selectedBug = ref(null);

function viewDetails(bug) {
  selectedBug.value = bug;
}

function closeDetails() {
  selectedBug.value = null;
}
</script>

<template>
  <div class="container">
    <header>
      <img class="brand-logo" :src="qaceLogo" alt="QAce logo" />

      <p class="tagline">Catch, classify and manage software bugs.</p>
    </header>

    <main>
      <h2>Bug Dashboard</h2>

      <div class="cards-grid">
        <div class="bug-card" v-for="bug in bugs" :key="bug.id">
          <div class="bug-icon">{{ bug.emoji }}</div>
          <h3>{{ bug.name }}</h3>

          <div class="badges">
            <span class="badge severity">{{ bug.severity }}</span>
            <span class="badge priority">{{ bug.priority }}</span>
            <span class="badge status">{{ bug.status }}</span>
          </div>

          <p class="bug-description">{{ bug.description }}</p>

          <button @click="viewDetails(bug)">View Details</button>
        </div>
      </div>

      <div v-if="selectedBug" class="modal-overlay">
        <div class="modal">
          <button class="close-button" @click="closeDetails">×</button>

          <div class="modal-icon">{{ selectedBug.emoji }}</div>
          <h2>{{ selectedBug.name }}</h2>

          <p><strong>Family:</strong> {{ selectedBug.family }}</p>
          <p><strong>Severity:</strong> {{ selectedBug.severity }}</p>
          <p><strong>Priority:</strong> {{ selectedBug.priority }}</p>
          <p><strong>Status:</strong> {{ selectedBug.status }}</p>
          <p><strong>Description:</strong> {{ selectedBug.description }}</p>
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

.brand-logo {
  max-width: 280px;
  width: 70%;
  height: auto;
  margin-bottom: 12px;
}

.tagline {
  margin-top: 0;
  color: #666;
  font-size: 1.1rem;
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

.bug-description {
  min-height: 80px;
}

button {
  margin-top: 10px;
  padding: 8px 16px;
  cursor: pointer;
}

.badges {
  display: flex;
  justify-content: center;
  gap: 8px;
  margin: 16px 0;
  flex-wrap: wrap;
}

.badge {
  padding: 4px 10px;
  border-radius: 999px;
  font-size: 0.85rem;
  font-weight: bold;
}

.severity {
  background: #ffebee;
  color: #c62828;
}

.priority {
  background: #fff3e0;
  color: #ef6c00;
}

.status {
  background: #e3f2fd;
  color: #1565c0;
}

.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.45);
  display: flex;
  align-items: center;
  justify-content: center;
}

.modal {
  position: relative;
  width: 90%;
  max-width: 500px;
  background: white;
  border-radius: 16px;
  padding: 40px 32px 32px;
  text-align: center;
  box-shadow: 0 8px 24px rgba(0, 0, 0, 0.25);
}

.modal-icon {
  font-size: 3rem;
  margin-bottom: 16px;
}

.modal h2 {
  margin: 0 0 24px 0;
}

.close-button {
  position: absolute;
  top: 12px;
  right: 16px;
  border: none;
  background: transparent;
  font-size: 2rem;
  cursor: pointer;
}
</style>
