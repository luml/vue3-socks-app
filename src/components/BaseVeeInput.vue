<template>
  <form class="review-form" @submit.prevent="onSubmit">
    <h3>Vee-Validtae</h3>
    <label for="name">Demo:</label>
    <Form>
      <Field name="field" :rules="isRequired" />
      <ErrorMessage name="field" />
    </Form>
    <input class="button" type="submit" value="Submit" />
  </form>
</template>

<script>
import { ref } from "vue";
import { Field, Form, ErrorMessage } from "vee-validate";
export default {
  components: {
    Field,
    Form,
    ErrorMessage,
  },
  setup() {
    const field = ref("");
    return {
      field,
    };
  },
  methods: {
    isRequired(value) {
      if (value && value.trim()) {
        return true;
      }

      return "This is required";
    },
    onSubmit() {
      if (this.field === "") {
        alert("Field is incomplete. Please fill out every field.");
        return;
      }
      console.log(this.field);
    },
  },
};
</script>

<style lang="scss" scoped>
</style>