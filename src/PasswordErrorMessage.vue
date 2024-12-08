<template>
    <p class="field-error">Password should have at least 8 characters</p>
</template>
  
<script>
export default {
name: "PasswordErrorMessage",
};
</script>
  
<style scoped>
.field-error {
color: red;
font-size: 0.85em;
margin-top: 5px;
}
</style>
  