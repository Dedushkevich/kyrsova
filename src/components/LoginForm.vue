<template>
  <div class="form-main-wrapper">
    <FormKit
      type="form"
      :value="{
        email: '',
        password: '',
      }"
      @submit="handleSubmit"
    >
      <h1 class="form-main-title">Welcome Back</h1>

      <label>
        <p class="form-main-label">Email</p>
        <FormKit
        input-class="form-main-input"
          :classes="{
            inner: {
              $reset: true,
            },
            input: { $reset: true },
            outer: { $reset: true },
          }"
          type="email"
          name="email"
          validation="required|email|ends_with:.com"
          validation-visibility="none"
          placeholder="Email"
        />
      </label>

      <label
        ><p class="form-main-label">Password</p>
        <FormKit
        input-class="form-main-input"
          :classes="{
            inner: {
              $reset: true,
            },
            input: { $reset: true },
            outer: { $reset: true },
          }"
          type="text"
          name="password"
          validation="required"
          validation-visibility="none"
          placeholder="Password"
      /></label>
    </FormKit>

    <RouterLink class="form-main-link" to="/signup">Register</RouterLink>
  </div>
</template>

<script>
export default {
  methods: {
    handleSubmit(data) {
      this.$store.dispatch("SignIn", data);
    },
  },
};
</script>
