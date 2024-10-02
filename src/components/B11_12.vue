<template>
  <div class="todo-list">
    <h3>Danh sách công việc</h3>
    <div class="todo-input-container">
      <input
        v-model="nameJob"
        type="text"
        class="todo-input"
        placeholder="Nhập tên công việc"
      />
      <button v-if="!checkUpdate" @click="handleAdd" class="add-button">
        Thêm
      </button>
      <button v-else @click="updateJob" class="add-button">Edit</button>
    </div>

    <ul class="tasks-list">
      <li v-for="job in listJobs" :key="job.id" class="task-item">
        <input
          type="checkbox"
          class="task-checkbox"
          :checked="job.status"
          @change="toggleJobStatus(job.id)"
        />
        <label :class="{ completed: job.status }">{{ job.name }}</label>
        <div class="task-actions">
          <button @click="handleEdit(job.id)" class="edit-button">sửa</button>
          <button @click="deleteButton(job.id)" class="delete-button">
            xóa
          </button>
        </div>
      </li>
    </ul>

    <p class="task-counter">
      Công việc đã hoàn thành: {{ jobComplete }} / {{ listJobs.length }}
    </p>
  </div>
</template>

<script setup>
import { reactive, ref, watch } from "vue";

const nameJob = ref("");
const listJobs = ref(JSON.parse(localStorage.getItem("jobs")));
const editingJobId = ref(null);
const checkUpdate = ref(false);
const jobComplete = ref(0);
const updateJobComplete = () => {
  jobComplete.value = listJobs.value.filter(
    (job) => job.status === true
  ).length;
};
updateJobComplete();

const handleAdd = () => {
  const find = listJobs.value.find((job) => job.name === nameJob.value);
  if (!find) {
    const newJob = {
      id: listJobs.value.length + 1,
      name: nameJob.value,
      status: false,
    };
    listJobs.value.push(newJob);
    localStorage.setItem("jobs", JSON.stringify(listJobs.value));
    nameJob.value = "";
  }
};

const deleteButton = (id) => {
  listJobs.value = listJobs.value.filter((job) => job.id !== id);
  localStorage.setItem("jobs", JSON.stringify(listJobs.value));
  updateJobComplete();
};

const handleEdit = (id) => {
  const job = listJobs.value.find((job) => job.id === id);
  if (job) {
    nameJob.value = job.name;
    checkUpdate.value = true;
    editingJobId.value = id;
  }
};

const updateJob = () => {
  const jobIndex = listJobs.value.findIndex(
    (job) => job.id === editingJobId.value
  );
  if (jobIndex !== -1) {
    listJobs.value[jobIndex].name = nameJob.value;
    localStorage.setItem("jobs", JSON.stringify(listJobs.value));
    nameJob.value = "";
    checkUpdate.value = false;
    editingJobId.value = null;
  }
};

const toggleJobStatus = (id) => {
  const jobIndex = listJobs.value.findIndex((job) => job.id === id);
  if (jobIndex !== -1) {
    listJobs.value[jobIndex].status = !listJobs.value[jobIndex].status;
    localStorage.setItem("jobs", JSON.stringify(listJobs.value));
    updateJobComplete();
  }
};
</script>

<style>
.todo-list {
  margin-top: 20px;
  max-width: 600px;
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

h3 {
  text-align: center;
  color: #333;
  font-size: 24px;
  margin-bottom: 20px;
}

.todo-input-container {
  display: flex;
  gap: 20px;
  margin-bottom: 20px;
}

.todo-input {
  width: 80%;
  padding: 10px;
  font-size: 16px;
  border: 1px solid #ccc;
  border-radius: 5px;
  outline: none;
}

.todo-input:focus {
  border-color: #007bff;
}

.add-button {
  padding: 10px 20px;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  font-size: 16px;
}

.add-button:hover {
  background-color: #0056b3;
}

.tasks-list {
  list-style-type: none;
  padding: 0;
  margin: 0;
}

.task-item {
  display: flex;
  align-items: center;
  padding: 10px;
  background-color: white;
  border-radius: 5px;
  margin-bottom: 10px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  transition: transform 0.2s ease;
}

.task-checkbox {
  margin-right: 15px;
  width: 18px;
  height: 18px;
}

label {
  font-size: 16px;
  flex-grow: 1;
  color: #333;
}

label.completed {
  text-decoration: line-through;
}

.task-actions {
  display: flex;
  gap: 10px;
}

.edit-button {
  background-color: rgb(189, 189, 0);
  color: white;
}

.delete-button {
  background-color: red;
  color: white;
}

.task-counter {
  margin-top: 20px;
  font-weight: bold;
  font-size: 16px;
}
</style>
