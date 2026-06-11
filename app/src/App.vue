<script setup>
import { ref, computed, watch } from "vue";
import { bugs } from "./data/bugs";
import qaceLogo from "./assets/qace-logo.png";

const currentScreen = ref("intro");
const selectedBug = ref(null);
const showCreateModal = ref(false);
const isEditingBug = ref(false);
const editBugName = ref("");
const editBugFamily = ref("");
const editBugSeverity = ref("");
const editBugPriority = ref("");
const editBugStatus = ref("");
const editBugDescription = ref("");
const newBugName = ref("");
const newBugFamily = ref("");
const newBugSeverity = ref("Critical");
const newBugPriority = ref("High");
const newBugDescription = ref("");
const createBugError = ref("");
const createBugSuccess = ref("");
const editBugSuccess = ref("");
const email = ref("");
const password = ref("");
const loginError = ref("");
const selectedSeverity = ref("All");
const searchTerm = ref("");
const savedBugs = localStorage.getItem("qace-bugs");

const bugList = ref(savedBugs ? JSON.parse(savedBugs) : [...bugs]);

watch(
  bugList,
  (newBugList) => {
    localStorage.setItem("qace-bugs", JSON.stringify(newBugList));
  },
  { deep: true },
);

const filteredBugs = computed(() => {
  const search = searchTerm.value.toLowerCase().trim();

  return bugList.value.filter((bug) => {
    const matchesSeverity =
      selectedSeverity.value === "All" ||
      bug.severity === selectedSeverity.value;

    const matchesSearch =
      bug.name.toLowerCase().includes(search) ||
      bug.family.toLowerCase().includes(search) ||
      bug.description.toLowerCase().includes(search);

    return matchesSeverity && matchesSearch;
  });
});

function goToLogin() {
  currentScreen.value = "login";
}

function viewDetails(bug) {
  selectedBug.value = bug;
}

function closeDetails() {
  selectedBug.value = null;
  isEditingBug.value = false;
}

function openCreateModal() {
  showCreateModal.value = true;
}

function closeCreateModal() {
  showCreateModal.value = false;
}

function saveBug() {
  if (
    !newBugName.value.trim() ||
    !newBugFamily.value.trim() ||
    !newBugDescription.value.trim()
  ) {
    createBugError.value = "Please fill in all required fields.";
    return;
  }

  createBugError.value = "";

  const bugAlreadyExists = bugList.value.some(
    (bug) => bug.name.toLowerCase() === newBugName.value.trim().toLowerCase(),
  );

  if (bugAlreadyExists) {
    createBugError.value = "A bug with this name already exists.";
    return;
  }

  const newBug = {
    id: Date.now(),
    emoji: "🕸️",
    name: newBugName.value.trim(),
    family: newBugFamily.value.trim(),
    severity: newBugSeverity.value,
    priority: newBugPriority.value,
    status: "Open",
    description: newBugDescription.value.trim(),
  };

  bugList.value.push(newBug);

  createBugSuccess.value = "Bug created successfully.";

  setTimeout(() => {
    createBugSuccess.value = "";
  }, 3000);

  newBugName.value = "";
  newBugFamily.value = "";
  newBugSeverity.value = "Critical";
  newBugPriority.value = "High";
  newBugDescription.value = "";

  closeCreateModal();
}

function startEditBug() {
  editBugName.value = selectedBug.value.name;
  editBugFamily.value = selectedBug.value.family;
  editBugSeverity.value = selectedBug.value.severity;
  editBugPriority.value = selectedBug.value.priority;
  editBugStatus.value = selectedBug.value.status;
  editBugDescription.value = selectedBug.value.description;

  isEditingBug.value = true;
}

function saveEditedBug() {
  selectedBug.value.name = editBugName.value;
  selectedBug.value.family = editBugFamily.value;
  selectedBug.value.severity = editBugSeverity.value;
  selectedBug.value.priority = editBugPriority.value;
  selectedBug.value.status = editBugStatus.value;
  selectedBug.value.description = editBugDescription.value;
  editBugSuccess.value = "Bug updated successfully.";

  setTimeout(() => {
    editBugSuccess.value = "";
  }, 3000);

  isEditingBug.value = false;
}

function cancelEditBug() {
  isEditingBug.value = false;
}

function enterLab() {
  currentScreen.value = "login";
}

function login() {
  if (!email.value || !password.value) {
    loginError.value = "Please enter email and password.";
    return;
  }

  if (email.value !== "qa@qace.dev" || password.value !== "123456") {
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

        <p>Email: qa@qace.dev</p>

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
      <div class="dashboard-actions">
        <button class="add-bug-button" @click="openCreateModal">
          + Add Bug
        </button>

        <button @click="logout" class="logout-button">Logout</button>
      </div>

      <p v-if="createBugSuccess" class="success-message">
        {{ createBugSuccess }}
      </p>

      <div class="search-bar">
        <input v-model="searchTerm" type="text" placeholder="Search bugs..." />
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

      <div v-if="filteredBugs.length === 0" class="empty-state">
        <h3>No bugs found</h3>
        <p>Try another search term or change the severity filter.</p>
      </div>

      <div v-else class="cards-grid">
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

      <div v-if="showCreateModal" class="modal-overlay">
        <div class="modal">
          <button class="close-button" @click="closeCreateModal">×</button>

          <h2 class="modal-title">Create New Bug</h2>

          <div class="create-bug-form">
            <input v-model="newBugName" type="text" placeholder="Bug Name" />

            <input
              v-model="newBugFamily"
              type="text"
              placeholder="Bug Family"
            />

            <select v-model="newBugSeverity">
              <option>Critical</option>
              <option>High</option>
              <option>Medium</option>
              <option>Low</option>
            </select>

            <select v-model="newBugPriority">
              <option>High</option>
              <option>Medium</option>
              <option>Low</option>
            </select>

            <textarea
              v-model="newBugDescription"
              rows="4"
              placeholder="Bug Description"
            ></textarea>

            <p v-if="createBugError" class="error-message">
              {{ createBugError }}
            </p>

            <button class="save-bug-button" @click="saveBug">Save Bug</button>
          </div>
        </div>
      </div>

      <div v-if="selectedBug" class="modal-overlay">
        <div class="modal">
          <button class="close-button" @click="closeDetails">×</button>

          <div class="modal-icon">{{ selectedBug.emoji }}</div>
          <h2 v-if="!isEditingBug" class="modal-title">
            {{ selectedBug.name }}
          </h2>

          <input v-else v-model="editBugName" class="edit-input" type="text" />

          <div v-if="!isEditingBug">
            <p><strong>Family:</strong> {{ selectedBug.family }}</p>
          </div>

          <div v-else class="edit-field">
            <label>Family</label>

            <input v-model="editBugFamily" class="edit-input" type="text" />
          </div>
          <p v-if="!isEditingBug">
            <strong>Severity:</strong> {{ selectedBug.severity }}
          </p>

          <div v-else class="edit-field">
            <label>Severity</label>

            <select v-model="editBugSeverity" class="edit-input">
              <option>Critical</option>
              <option>High</option>
              <option>Medium</option>
              <option>Low</option>
            </select>
          </div>
          <div v-if="!isEditingBug">
            <p><strong>Priority:</strong> {{ selectedBug.priority }}</p>
          </div>

          <div v-else class="edit-field">
            <label>Priority</label>

            <select v-model="editBugPriority" class="edit-input">
              <option>High</option>
              <option>Medium</option>
              <option>Low</option>
            </select>
          </div>
          <div v-if="!isEditingBug">
            <p><strong>Status:</strong> {{ selectedBug.status }}</p>
          </div>

          <div v-else class="edit-field">
            <label>Status</label>

            <select v-model="editBugStatus" class="edit-input">
              <option>Open</option>
              <option>In Progress</option>
              <option>Closed</option>
            </select>
          </div>
          <div v-if="!isEditingBug">
            <p><strong>Description:</strong> {{ selectedBug.description }}</p>
          </div>

          <div v-else class="edit-field">
            <label>Description</label>

            <textarea
              v-model="editBugDescription"
              class="edit-input"
              rows="4"
            ></textarea>
          </div>

          <p v-if="editBugSuccess" class="success-message">
            {{ editBugSuccess }}
          </p>

          <button
            v-if="!isEditingBug"
            class="edit-bug-button"
            @click="startEditBug"
          >
            Edit Bug
          </button>
          <button
            v-if="isEditingBug"
            class="save-bug-button"
            @click="saveEditedBug"
          >
            Save Changes
          </button>
          <button
            v-if="isEditingBug"
            class="cancel-edit-button"
            @click="cancelEditBug"
          >
            Cancel
          </button>
        </div>
      </div>
    </main>
  </div>
</template>

<style>
/* Base */
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

/* Header */
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

/* Dashboard Actions */
.dashboard-actions {
  display: flex;
  justify-content: center;
  gap: 10px;
  flex-wrap: wrap;
  margin-bottom: 24px;
}

/* Buttons */
button {
  margin-top: 10px;
  padding: 8px 16px;
  cursor: pointer;
}

.add-bug-button,
.save-bug-button {
  background: #2e7d32;
  color: white;
  border: none;
  border-radius: 8px;
  font-weight: bold;
  cursor: pointer;
}

.add-bug-button {
  padding: 10px 18px;
}

.save-bug-button {
  padding: 12px;
}

.add-bug-button:hover,
.save-bug-button:hover {
  background: #1b5e20;
}

.edit-bug-button {
  background: #1565c0;
  color: white;
  border: none;
  border-radius: 8px;
  padding: 10px 18px;
  font-weight: bold;
  cursor: pointer;
}

.edit-bug-button:hover {
  background: #0d47a1;
}

.cancel-edit-button {
  background: #6b7280;
  color: white;
  border: none;
  border-radius: 8px;
  padding: 12px;
  font-weight: bold;
  cursor: pointer;
  margin-left: 8px;
}

.cancel-edit-button:hover {
  background: #4b5563;
}

.logout-button {
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

.close-button {
  position: absolute;
  top: 12px;
  right: 16px;
  border: none;
  background: transparent;
  color: #111827;
  font-size: 2rem;
  font-weight: bold;
  line-height: 1;
  cursor: pointer;
  opacity: 1;
  z-index: 10;
}

.close-button:hover {
  color: #c62828;
}

/* Login */
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

/* Search */
.search-bar {
  display: flex;
  justify-content: center;
  margin-bottom: 20px;
}

.search-bar input {
  width: 100%;
  max-width: 420px;
  padding: 12px 16px;
  border: none;
  border-radius: 999px;
  font-size: 1rem;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.08);
}

/* Filters */
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
  color: #111827;
  font-weight: bold;
  cursor: pointer;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.08);
}

.filter-bar button.active {
  background: #f4c542;
  color: #1f2933;
}

/* Cards */
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

/* Badges */
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

/* Modals */
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
  color: #1f2933;
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

.modal-title {
  color: #111827;
  font-weight: 700;
  opacity: 1;
}

.modal p,
.modal strong {
  color: #4b5563;
  opacity: 1;
}

.edit-input {
  width: 100%;
  box-sizing: border-box;
  padding: 10px;
  border: 1px solid #d1d5db;
  border-radius: 8px;
  font-size: 1rem;
  margin-bottom: 16px;
}

/* Create Bug Form */
.create-bug-form {
  display: flex;
  flex-direction: column;
  gap: 12px;
}

.create-bug-form input,
.create-bug-form select,
.create-bug-form textarea {
  padding: 10px;
  border: 1px solid #d1d5db;
  border-radius: 8px;
  font-size: 1rem;
}

.edit-input {
  width: 100%;
  box-sizing: border-box;
  padding: 10px;
  border: 1px solid #d1d5db;
  border-radius: 8px;
  font-size: 1rem;
  margin-bottom: 16px;
}

.edit-field {
  margin-bottom: 16px;
  text-align: left;
}

.edit-field label {
  display: block;
  font-weight: bold;
  margin-bottom: 6px;
  color: #4b5563;
}

/* States */
.empty-state {
  text-align: center;
  margin-top: 40px;
  padding: 40px;
  background: white;
  border-radius: 16px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.08);
  max-width: 500px;
  margin-left: auto;
  margin-right: auto;
}

.empty-state h3 {
  margin-bottom: 12px;
  color: #555;
}

.empty-state p {
  color: #777;
}

.error-message {
  color: #c62828;
  font-weight: bold;
  margin-top: 12px;
}

.modal .error-message {
  color: #c62828;
}

.modal .success-message {
  color: #2e7d32;
  font-weight: bold;
}
</style>
