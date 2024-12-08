<template>
  <div class="app">
    <form @submit.prevent="handleSubmit">
      <fieldset>
        <h2>Sign Up</h2>

        <div class="field">
          <label>
            First name <sup>*</sup>
          </label>
          <input
            type="text"
            placeholder="First name"
            v-model="firstName"
          />
        </div>

        <div class="field">
          <label>Last name</label>
          <input
            type="text"
            placeholder="Last name"
            v-model="lastName"
          />
        </div>

        <div class="field">
          <label>
            Email address <sup>*</sup>
          </label>
          <input
            type="email"
            placeholder="Email address"
            v-model="email"
          />
        </div>

        <div class="field">
          <label>
            Password <sup>*</sup>
          </label>
          <input
            type="password"
            placeholder="Password"
            v-model="password.value"
            @blur="setPasswordTouched"
          />
          <PasswordErrorMessage
            v-if="password.isTouched && password.value.length > 0 && password.value.length < 8"
          />
        </div>

        <div class="field">
          <label>
            Role <sup>*</sup>
          </label>
          <select v-model="role">
            <option value="role">Role</option>
            <option value="individual">Individual</option>
            <option value="business">Business</option>
          </select>
        </div>

        <button type="submit" :disabled="!isFormValid">
          Create account
        </button>
      </fieldset>
    </form>
  </div>
</template>

<script>
import { ref, computed } from "vue";
import PasswordErrorMessage from "./PasswordErrorMessage.vue"; // Import PasswordErrorMessage component

export default {
  name: "App",
  components: {
    PasswordErrorMessage,
  },
  setup() {
    const firstName = ref("");
    const lastName = ref("");
    const email = ref("");
    const password = ref({
      value: "",
      isTouched: false,
    });
    const role = ref("role");

    // Password error message visibility
    const setPasswordTouched = () => {
      password.value.isTouched = true;
    };

    // Validation function
    const validateEmail = (email) => {
      const re = /^[a-zA-Z0-9._-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,6}$/;
      return re.test(email);
    };

    // Form validity check
    const isFormValid = computed(() => {
      return (
        //password.value.length >= 8 &&
        validateEmail(email.value) &&
        (role.value === "individual" || role.value === "business")
      );
    });

    // Clear form fields
    const clearForm = () => {
      firstName.value = "";
      lastName.value = "";
      email.value = "";
      password.value = { value: "", isTouched: false };
      role.value = "role";
    };

    // Handle form submission
    const handleSubmit = () => {
      alert("Account created!");
      clearForm();
    };

    return {
      firstName,
      lastName,
      email,
      password,
      role,
      isFormValid,
      setPasswordTouched,
      handleSubmit,
    };
  },
};
</script>

<style scoped>
/* General Styles */
body {
  font-family: Arial, sans-serif;
  margin: 0;
  padding: 0;
  background-color: #f0f4f8;
}

/* Center the form on the page */
.app {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

/* Form container */
form {
  background-color: #fff;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
  width: 100%;
  max-width: 400px;
}

fieldset {
  border: none;
  padding: 0;
}

/* Form header */
h2 {
  text-align: center;
  color: #333;
  font-size: 1.6em;
  margin-bottom: 20px;
}

/* Field container */
.field {
  margin-bottom: 15px;
}

.field label {
  font-size: 0.9em;
  color: #333;
  display: block;
  margin-bottom: 5px;
}

.field input,
.field select {
  width: 100%;
  padding: 10px;
  margin: 5px 0;
  border: 1px solid #ccc;
  border-radius: 4px;
  font-size: 1em;
}

.field input:focus,
.field select:focus {
  border-color: #4caf50;
  outline: none;
}

/* Error message for password field */
.field .FieldError {
  color: red;
  font-size: 0.85em;
  margin-top: 5px;
}

/* Button Styles */
button {
  background-color: #4caf50;
  color: white;
  border: none;
  padding: 12px 20px;
  border-radius: 4px;
  font-size: 1.1em;
  cursor: pointer;
  width: 100%;
  margin-top: 20px;
}

button:disabled {
  background-color: #ddd;
  cursor: not-allowed;
}

button:hover:not(:disabled) {
  background-color: #45a049;
}

/* Responsive Design */
@media (max-width: 480px) {
  .app {
    padding: 10px;
  }

  form {
    width: 100%;
    padding: 15px;
  }

  h2 {
    font-size: 1.4em;
  }

  button {
    font-size: 1em;
  }
}
</style>
