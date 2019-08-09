<template>
  <div id="app" class="small-container">
    <h1>Employees</h1>
    <employee-form @add:employee="addEmployee" />
    <employee-table
      @delete:employee="deleteEmployee"
      @edit:employee="editEmployee"
      :employees="employees"
    />
  </div>
</template>

<script>
import EmployeeTable from './components/EmployeeTable';
import EmployeeForm from './components/EmployeeForm';
export default {
  name: 'app',
  components: {
    EmployeeTable,
    EmployeeForm,
  },
  data() {
    return {
      employees: [
        {
          id: 0,
          name: 'User Name',
          email: 'user@user.com',
        },
        {
          id: 1,
          name: 'Admin User',
          email: 'admin@user.com',
        },
      ],
    };
  },
  methods: {
    deleteEmployee(index) {
      console.log(index);
      this.employees = this.employees.filter(employee => {
        return employee.id !== index;
      });
      console.log(this.employees);
    },
    addEmployee(employee) {
      const id = this.employees.length > 0 ? this.employees.length : 0;
      employee = {...employee, id};
      this.employees = [...this.employees, employee];
    },
    editEmployee(id, updatedEmployee) {
      this.$set(this.employees, id, {id, ...updatedEmployee});
    },
  },
};
</script>
