<script setup>
import { ref, computed } from "vue";
import { bugs } from "./data/bugs";
import qaceLogo from "./assets/qace-logo.png";

const currentScreen = ref("intro");
const selectedBug = ref(null);
const email = ref("");
const password = ref("");
const loginError = ref("");
const selectedSeverity = ref("All");

const filteredBugs = computed(() => {
  if (selectedSeverity.value === "All") {
    return bugs;
  }

  return bugs.filter((bug) => bug.severity === selectedSeverity.value);
});

function goToLogin() {
  currentScreen.value = "login";
}

function viewDetails(bug) {
  selectedBug.value = bug;
}

function closeDetails() {
  selectedBug.value = null;
}

function enterLab() {
  currentScreen.value = "login";
}

function login() {
  if (!email.value || !password.value) {
    loginError.value = "Please enter email and password.";
    return;
  }

  if (email.value !== "qa@qace.com" || password.value !== "123456") {
    loginError.value = "Invalid email or password.";
    return;
  }

  loginError.value = "";
  currentScreen.value = "dashboard";
}

function logout() {
  currentScreen.value = "login";

  email.value = "";
  password.value = "";
  loginError.value = "";
}
</script>

<template>
  <div class="container">
    <header>
      <img class="brand-logo" :src="qaceLogo" alt="QAce logo" />

      <p class="tagline">Catch, classify and manage software bugs.</p>
    </header>

    <section v-if="currentScreen === 'intro'" class="intro-screen">
      <h2>Welcome to QAce Bug Lab</h2>

      <p>Discover, classify and manage software bugs.</p>

      <p>
        A QA portfolio project focused on testing, quality assurance and
        continuous improvement.
      </p>

      <button @click="enterLab">Enter Bug Lab</button>
    </section>

    <section v-if="currentScreen === 'login'" class="login-screen">
      <h2>Login</h2>

      <p>Access the QAce Bug Lab environment.</p>

      <div class="demo-credentials">
        <strong>Demo Credentials</strong>

        <p>Email: qa@qace.com</p>

        <p>Password: 123456</p>
      </div>

      <input v-model="email" type="email" placeholder="Email" />

      <input v-model="password" type="password" placeholder="Password" />

      <p v-if="loginError" class="error-message">
        {{ loginError }}
      </p>

      <button @click="login">Login</button>
    </section>

    <main v-if="currentScreen === 'dashboard'">
      <div class="dashboard-header">
        <h2>Bug Dashboard</h2>

        <button @click="logout" class="logout-button">Logout</button>
      </div>

      <div class="filter-bar">
        <button
          :class="{ active: selectedSeverity === 'All' }"
          @click="selectedSeverity = 'All'"
        >
          All
        </button>

        <button
          :class="{ active: selectedSeverity === 'Critical' }"
          @click="selectedSeverity = 'Critical'"
        >
          Critical
        </button>

        <button
          :class="{ active: selectedSeverity === 'High' }"
          @click="selectedSeverity = 'High'"
        >
          High
        </button>

        <button
          :class="{ active: selectedSeverity === 'Medium' }"
          @click="selectedSeverity = 'Medium'"
        >
          Medium
        </button>

        <button
          :class="{ active: selectedSeverity === 'Low' }"
          @click="selectedSeverity = 'Low'"
        >
          Low
        </button>
      </div>

      <div class="cards-grid">
        <div class="bug-card" v-for="bug in filteredBugs" :key="bug.id">
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

.login-screen {
  max-width: 420px;
  margin: 40px auto;
  padding: 32px;
  background: white;
  border-radius: 16px;
  text-align: center;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.08);
}

.login-screen input {
  display: block;
  width: 100%;
  box-sizing: border-box;
  margin: 12px 0;
  padding: 10px;
  font-size: 1rem;
}

.login-screen button {
  width: 100%;
  margin-top: 16px;
}

.error-message {
  color: #c62828;
  font-weight: bold;
  margin-top: 12px;
}

.dashboard-header {
  position: relative;
  width: 90%;
  max-width: 1120px;
  margin: 0 auto 30px auto;
  text-align: center;
}

.dashboard-header h2 {
  margin: 0;
}

.logout-button {
  position: absolute;
  right: 0;
  top: 50%;
  transform: translateY(-50%);
  background: #c62828;
  color: white;
  border: none;
  border-radius: 8px;
  padding: 10px 18px;
  font-weight: bold;
  cursor: pointer;
}

.logout-button:hover {
  background: #b71c1c;
}

.filter-bar {
  display: flex;
  justify-content: center;
  gap: 10px;
  margin-bottom: 30px;
  flex-wrap: wrap;
}

.filter-bar button {
  border: none;
  border-radius: 999px;
  padding: 8px 16px;
  background: white;
  font-weight: bold;
  cursor: pointer;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.08);
}

.filter-bar button.active {
  background: #f4c542;
  color: #1f2933;
}
</style>
