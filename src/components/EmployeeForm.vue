<template>
  <div>
    <form @submit.prevent="handleSubmit">
      <label>Employee Name</label>
      <input v-model="employee.name" type="text" />
      <label>Employee Email</label>
      <input v-model="employee.email" type="text" />
      <div v-if="error">{{error}}</div>
      <button>Add</button>
    </form>
  </div>
</template>

<script>
export default {
  name: "employee-from",
  data() {
    return {
      employee: {
        name: "",
        email: ""
      },
      error: null
    };
  },
  methods: {
    handleSubmit() {
      if (!this.employee.name || !this.employee.email){
        this.error = "Please input correct value";
        return false;
      }
      this.error = null;
      this.$emit("add:employee", this.employee);
    }
  },


};
</script>
