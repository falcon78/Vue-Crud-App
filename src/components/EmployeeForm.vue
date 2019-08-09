<template>
  <div>
    <form @submit.prevent="handleSubmit">
      <label>Employee Name</label>
      <input
        ref="first"
        :class="{ error: isInvalidName && submitting }"
        v-model="employee.name"
        type="text"
        @focus="clearStatus"
        @keypress="clearStatus"
      />
      <label>Employee Email</label>
      <input
        :class="{ error: emailError && submitting }"
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
    }
  },
  computed: {
    isInvalidName() {
      return !this.employee.name
    },
    isInvalidEmail() {
      return !this.emailRegex.test(this.employee.email)
    },
    success() {
      return !this.isInvalidName && !this.isInvalidEmail
    },
  },
  methods: {
    handleSubmit() {
      this.submitting = true
      this.emailError = false
      this.clearStatus()
      if (this.isInvalidName || this.isInvalidEmail) {
        this.nameError = !!this.isInvalidName
        this.emailError = !!this.isInvalidEmail
        return false
      }
      this.$emit('add:employee', this.employee)
      this.error = null
      this.submitting = false
      this.success = true
      this.added = true
      this.$refs.first.focus()
      this.employee.name = this.employee.email = ''
    },
    clearStatus() {
      this.emailError = false
      this.added = false
    },
  },
}
</script>

<style scoped>
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
