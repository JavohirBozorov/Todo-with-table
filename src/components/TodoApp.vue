<template>
  <div id="list-complete-demo" class="container w-75 demo">
    <!-- Title -->
    <h3 class="py-4 mx-auto title">My To Do App</h3>

    <!-- Input -->
    <div class="d-flex input">
      <input
        v-model.lazy="task"
        @keyup.enter="sendTask"
        type="text"
        placeholder="Enter Your Chores..."
        aria-describedby="basic-addon2"
        class="form-control"
      />
      <button @click="sendTask()" id="basic-addon2" class="btn">Submit</button>
    </div>

    <!-- Table -->
    <table class="table table-bordered mt-5">
      <thead>
        <tr>
          <th class="width" scope="col">Vazifa</th>
          <th class="width" scope="col">Holati</th>
          <th class="width" scope="col">Tahrirlash</th>
          <th class="width" scope="col">O'chirish</th>
        </tr>
      </thead>
      <transition-group tag="tbody" name="fade">
        <tr v-for="(task, index) in tasks" :key="index">
          <td class="name">{{ task.name }}</td>
          <td class="status">
            <span @click="changeStatus(index)" class="pointer">
              {{ task.status }}
            </span>
          </td>
          <td>
            <div @click="editTask(index)">
              <span class="fas fa-pen"></span>
            </div>
          </td>
          <td>
            <div @click="deleteTask(index)">
              <span class="fas fa-trash"></span>
            </div>
          </td>
        </tr>
      </transition-group>
    </table>
  </div>
</template>

<script>
import "animate.css";

export default {
  name: "ToDoApp",
  props: {
    msg: String,
  },
  data() {
    return {
      task: "",
      editedTask: null,
      clicked: false,
      statuses: ["Bajarilmagan", "Bajarilmoqda", "Bajarildi"],
      tasks: [
        {
          name: "Yangi mavzuni o'zlashtirish",
          status: "Bajarildi",
        },
        {
          name: "Yangi darsni o'zlashtirish",
          status: "Bajarilmagan",
        },
        {
          name: "Photoshop dasturini o'rganish",
          status: "Bajarilmoqda",
        },
        {
          name: "Reactni o'rganish",
          status: "Bajarilmagan",
        },
      ],
    };
  },
  methods: {
    sendTask() {
      if (this.task.trim() == 0) return;

      if (this.editedTask === null) {
        this.tasks.push({
          name: this.task,
          status: "Bajarilmagan",
        });
      } else {
        this.tasks[this.editedTask].name = this.task;
        this.editedTask = null;
      }

      this.task = "";
    },

    deleteTask(index) {
      this.tasks.splice(index, 1);
    },

    editTask(index) {
      this.task = this.tasks[index].name;
      this.editedTask = index;
    },

    changeStatus(index) {
      let newIndex = this.statuses.indexOf(this.tasks[index].status);
      if (++newIndex > 2) newIndex = 0;
      this.tasks[index].status = this.statuses[newIndex];
    },
  },
};
</script>

<style scoped>
  .title,
  table {
    text-align: center;
  }
  table {
    background-color: #fff;
    border-radius: 2rem;
    border-color: paleturquoise;
  }
  .btn,
  textarea:focus,
  input[type="text"]:focus,
  .uneditable-input:focus {
    box-shadow: none;
    outline: none;
  }
  .btn {
    background-color: #80daff;
    border: 1px solid #ccc;
    margin-left: -1rem;
    border-radius: 0 1rem 1rem 0;
  }
  .form-control {
    border-radius: 1rem 0 0 1rem;
  }
  .width {
    width: 80px;
    border-bottom: 2px solid paleturquoise;
  }
  .pointer {
    cursor: pointer;
  }
  .status {
    width: 120px;
  }
  .fa-pen,
  .fa-trash {
    color: #555;
  }
  /* Fade animation */
  .fade-enter-active,
  .fade-leave-active {
    transition: all 0.4s ease;
    overflow: hidden;
  }
  .fade-enter, 
  .fade-leave-to {
    opacity: 0;
    transform: translateY(20px);
    overflow: hidden;
  }
</style>
