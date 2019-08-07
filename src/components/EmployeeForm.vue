<template>
  <div>
    <form @submit.prevent="handleSubmit">
      <label>Employee Name</label>
      <input v-model="employee.name" type="text" />
      <label>Employee Email</label>
      <input v-model="employee.email" type="text" />
      <button >Add</button>
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
      }
    };
  },
  methods: {
    handleSubmit () {
      console.log("testing submit");
    }
  }
};
</script>
