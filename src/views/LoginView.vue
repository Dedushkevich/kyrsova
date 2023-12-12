<template>
  <LoginForm />
</template>

<script>
import LoginForm from "@/components/LoginForm.vue";

export default {
  components: { LoginForm },
};
</script>

<style>
button.formkit-input {
  padding: 10px 30px!important;

  font-size: 16px !important;

  border-radius: 5px !important;

  background: rgba(46, 46, 46, 0.3) !important;
  color: #000000 !important;

}

.form-main-input {
  width: 100%;
  margin-bottom: 32px;
  padding: 8px 0;

  font-size: 20px;

  border: none;
  outline: none;
  border-bottom: 2px solid #050505;

  background-color: transparent;

  transition: border-color 250ms cubic-bezier(0.4, 0, 0.2, 1);
}

.form-main-input::placeholder{
  color: #000;
}

.form-main-wrapper {
  width: 400px;

  margin: 200px auto;
  padding: 20px 50px;

  text-align: center;

  background-color: rgb(0, 0, 0, 0.3);

  overflow: auto;
}

.form-main-title {
  font-size: 32px;
}

.form-main-link-wrapper {
  color: #000;
}

.form-main-link {
  text-decoration: none;

  color: black;
}
</style>
