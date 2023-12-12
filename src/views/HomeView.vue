<template>
  <div class="page-wrapper">
    <div class="page-content-wrapper">
      <form class="form-categories">
        <h1 class="form-categories-title">Categories</h1>

        <CategoriesList />

        <button
          type="button"
          class="form-categories-add-categorie"
          @click="handleModalOpen"
        >
          Add Categorie
        </button>
      </form>
      <div class="task-wrapper">
        <h1 class="task-title">Tasks</h1>

        <TaskList />

        <button class="task-add-signout-btn width" @click="addTask">
          Add task
        </button>
      </div>

      <div class="signout-btn-wrapper">
        <p class="email">{{ email }}</p>
        <button class="task-add-signout-btn" @click="signOut">Sign Out</button>
      </div>

      <ModalCategoriesVue v-if="isModalOpen" />
    </div>
  </div>
</template>

<script>
import TaskList from "@/components/TaskList.vue";
import CategoriesList from "@/components/CategoriesList.vue";
import ModalCategoriesVue from "@/components/ModalCategories.vue";

export default {
  components: { TaskList, CategoriesList, ModalCategoriesVue },

  created() {
    if (localStorage.getItem("uid") && localStorage.getItem("isLoggedIn")) {
      const data = {
        uid: localStorage.getItem("uid"),
        isLoggedIn: localStorage.getItem("isLoggedIn"),
        email: localStorage.getItem("email"),
      };

      this.$store.dispatch("setDataFromLs", data);
    }

    if (!this.isLoggedIn) {
      this.$router.push("/signin");
      return;
    }

    this.$store.dispatch("fetchBoard");
  },

  computed: {
    uid() {
      return this.$store.getters.uid;
    },

    isLoggedIn() {
      return this.$store.getters.isLoggedIn;
    },

    email() {
      return this.$store.getters.email;
    },

    categories() {
      return this.$store.getters.categories;
    },

    isModalOpen() {
      return this.$store.getters.isModalOpen;
    },
  },

  methods: {
    handleModalOpen() {
      this.$store.dispatch("toggleModal");
    },

    addTask() {
      const d = new Date();

      const datestring =
        ("0" + d.getDate()).slice(-2) +
        "-" +
        ("0" + (d.getMonth() + 1)).slice(-2) +
        "-" +
        d.getFullYear() +
        " " +
        ("0" + d.getHours()).slice(-2) +
        ":" +
        ("0" + d.getMinutes()).slice(-2);

      const newTask = {
        id: Date.now(),
        uid: this.uid,
        text: "",
        categorie: this?.categories[0]?.id || null,
        created: datestring,
        closed: null,
      };

      this.$store.dispatch("addTask", newTask);
    },

    signOut() {
      this.$store.dispatch("SignOut");
    },
  },
};
</script>

<style>
.page-wrapper {
  padding: 8px 0;
}

.page-content-wrapper {
  display: flex;
  justify-content: space-between;
}

.email {
  margin-right: 16px;
}

.signout-btn-wrapper {
  text-align: end;
  margin-bottom: 16px;
  display: flex;
  position: absolute;

  bottom: 5%;
  right: 12%;
  align-items: center;
}

.form-categories {
  padding: 4px;

  width: 220px;

  margin-bottom: 10px;

  background-color: transparent;
}

.form-categories-title {
  padding-top: 12px;
  margin-bottom: 8px;
  color: #000;
  text-align: center;
}

.form-categories-list {
  max-height: 565px;
  margin-bottom: 16px;

  overflow: auto;
}

.form-categories-item {
  display: flex;

  background-color: rgba(0, 0, 0, 0.3);

  padding: 8px;

  border-radius: 12px;

  justify-content: space-between;
  align-items: center;

  margin-bottom: 8px;
}

.form-categories-label {
  font-size: 16px;
}

.form-filter-input {
  display: none;
}

.form-filter-checked {
  color: rgb(43, 43, 43);
}

.form-filter-uncheked {
  color: rgb(0, 0, 0);
}

.form-categories-delete-categorie {
  cursor: pointer;
  border: none;
  background-color: transparent;
}

.form-categories-add-categorie {
  display: block;
  margin: 0 auto;
  padding: 10px 16px;
  font-size: 16px;
  border: none;
  cursor: pointer;
  border-radius: 5px;
  background-color: rgba(0, 0, 0, 0.3);
  color: #000000;
}

.backdrop {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100vh;
}

.modal {
  position: absolute;
  top: 50%;
  left: 25%;
  transform: translate(-50%, -50%);
  width: 400px;
  padding: 15px;
  border-radius: 5px;
  background-color: rgb(0, 0, 0, 0.3);
}

.modal-input {
  width: 100%;
  margin-bottom: 8px;
  font-size: 16px;
  border: none;
  outline: none;
  border-bottom: 20px solid rgba(0, 0, 0, 0.3)0.308
}

.modal-btn {
  padding: 10px 30px;
  width: 100%;
  font-size: 16px;
  border: none;
  border-radius: 5px;
  background: #adadad;
  color: #ffffff;
}

.task-wrapper {
  align-self: flex-start;
  width: 1000px;
  padding: 20px 40px;

  background-color: transparent;
  border-radius: 12px;
}

.task-title {
  padding-top: 1px;
  color: black;
}

.task-list {
  max-height: 565px;
  margin-bottom: 16px;

  overflow: auto;
}

.task-item {
  position: relative;
  display: flex;
  justify-content: space-between;

  padding: 8px 8px;

  background-color: rgba(0, 0, 0, 0.3);

  border-radius: 12px;

  margin-bottom: 8px;
}

.task-textarea {
  resize: none;
  width: 600px;
  height: 30px;
  padding: 4px 12px;

  font-size: 16px;

  border: none;
  outline: none;

  background-color: rgba(0, 0, 0, 0.4);
}

.task-created {
  font-size: 12px;

  color: #000000;
}

.task-completed-wrapper {
  position: absolute;
  top: 0;
  left: 0;

  width: 100%;
  height: 100%;

  border-radius: 12px;

  background-color: rgba(26, 92, 0, 0.4);
}

.task-select {
  align-self: center;

  border: none;
  outline: none;

  background-color: transparent;
}

.task-btn {
  align-self: center;

  width: 20px;
  height: 20px;

  border: none;

  cursor: pointer;

  background-color: transparent;
}

.task-btn.del {
  z-index: 999;
}

.task-add-signout-btn {
  border-radius: 5px;
  align-self: center;
  padding: 10px 30px;
  font-size: 20px;
  outline: none;
  border: none;
  cursor: pointer;
  background-color: rgba(0, 0, 0, 0.3);
  color: rgb(0, 0, 0);
}

.width {
  width: 100%;
}
</style>
