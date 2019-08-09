<template>
  <div id="employee-table">
    <p v-if="employees.length < 1">No Employee Data</p>
    <table v-if="employees.length > 0">
      <tbody>
        <tr v-for="employee in employees" :key="employee.id">
          <td v-if="editing">
            <input type="text" v-model="employee.name" />
            <input type="text" v-model="employee.email" />
          </td>
          <td v-else>{{ employee.name }}{{ employee.email }}</td>
          <button @click="editMode(employee.id)">
            Edit
          </button>
          <button @click="$emit('delete:employee', employee.id)">
            Delete
          </button>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: 'employee-table',
  props: {
    employees: Array,
  },
  data() {
    return {
      editing: null,
    };
  },
  methods: {
    editMode(employeeId) {
      this.editing = employeeId;
    },
    editEmployee(employee) {
      if (!employee.name || !employee.email) return;
      this.$emit('edit:employee', employee.id, employee);
      this.editing = null;
    },
  },
};
</script>

<style scoped>
button {
  background: purple;
  border: none;
  width: max-content;
  padding: 10px;
  margin: 0 2px;
  transition: all 0.2s ease-in-out;
}

button:hover {
  transform: scale(1.05);
}
</style>
