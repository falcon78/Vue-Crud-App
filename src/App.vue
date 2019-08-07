<template>
  <div id="app" class="small-container">
    <h1>Employees</h1>
    <employee-form></employee-form>
    <employee-table :employees="employees" />
  </div>
</template>

<script>
import EmployeeTable from "./components/EmployeeTable";
import EmployeeForm from "./components/EmployeeForm";
export default {
  name: "app",
  components: {
    EmployeeTable,
    EmployeeForm
  },
  data() {
    return {
      employees: [
        {
          id: 1,
          name: "User Name",
          email: "user@user.com"
        },
        {
          id: 2,
          name: "Admin User",
          email: "admin@user.com"
        }
      ]
    };
  }
};
</script>

<style></style>
