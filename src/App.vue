<template>
  <div id="app" class="small-container">
    <h1>Employees</h1>
    <employee-form @add:employee="addEmployee" />
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
          id: 0,
          name: "User Name",
          email: "user@user.com"
        },
        {
          id: 1,
          name: "Admin User",
          email: "admin@user.com"
        }
      ]
    };
  },
  methods: {
    addEmployee(employee) {
      const id = this.employees.length > 0 ? this.employees.length : 0;
      console.log(employee.name);
      employee = { ...employee, id };
      this.employees = [...this.employees, employee];
    }
  }
};
</script>

<style></style>
