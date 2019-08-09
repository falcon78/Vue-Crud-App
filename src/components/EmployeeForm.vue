<template>
  <div>
    <form @submit.prevent="handleSubmit">
      <label>Employee Name</label>
      <input
        :class="{'error': isInvalidName && submitting}"
        v-model="employee.name"
        type="text"
      />
      <label>Employee Email</label>
      <input
        :class="{'error': isInvalidEmail && submitting }"
        v-model="employee.email"
        type="text"
      />
      <p v-if="!success && submitting">
        ❗Please fill out all required fields
      </p>
      <p v-if="added">
        ✅ Employee successfully added
      </p>
      <button>Add</button>
    </form>
  </div>
</template>

<script>
export default {
  name: 'employee-from',
  data() {
    return {
      added: false,
      submitting: null,
      employee: {
        name: '',
        email: '',
      },
      emailRegex: new RegExp(
          '^[a-zA-Z0-9.!#$%&’*+/=?^_`{|}~-]+@[a-zA-Z0-9-]+(?:.[a-zA-Z0-9-]+)*$'
      ),
    };
  },
  computed: {
    isInvalidName() {
      return !this.employee.name;
    },
    isInvalidEmail() {
      return !this.emailRegex.test(this.employee.email);
    },
    success() {
      return this.isInvalidName && this.isInvalidEmail;
    },
  },
  methods: {
    handleSubmit() {
      this.submitting = true;
      this.clearStatus();
      if (this.isInvalidName || this.isInvalidEmail) {
        this.isInvalidName ? (this.nameError = true) : (this.emailError = true);
        return false;
      }
      this.error = null;
      this.submitting = false;
      this.success = true;
      this.added = true;
      this.$emit('add:employee', this.employee);
    },
    clearStatus() {
      ;(this.emailError = false), (this.nameError = false), (this.added = false);
    },
  },
};
</script>


<style>
.danger {
  color: red;
  font-size: 1em;
}

.error {
  border-width: 2px;
  border-color: red;
  border-style: solid;
}
</style>
