<template>
  <form class="review-form" @submit.prevent="onSubmit">
    <h3>Leave a review</h3>

    <BaseInput
      v-model="name"
      label="Name"
      type="text"
      error="This input has error"
    />
    <label for="review">Review:</label>
    <textarea id="review" placeholder="Anything" v-model="review"></textarea>

    <BaseSelect :options="rates" v-model="rating" label="Rating" />

    <BaseSelect
      :options="recommends"
      v-model="recommend"
      label="Would you recommend this product?"
    />

    <BaseInput v-model="Submit" label="Submit" type="submit" />
  </form>
  <section>
    <!-- other extra base -->
    <fieldset>
      <legend>Extras</legend>
      <div>
        <BaseCheckbox
          v-model="event.extras.catering"
          label="Catering"
        ></BaseCheckbox>
      </div>
      <div>
        <BaseCheckbox
          v-model="event.extras.music"
          label="Live Music"
        ></BaseCheckbox>
      </div>
    </fieldset>

    <fieldset>
      <legend>Are Pets allowed ?</legend>
      <div>
        <BaseRadioGroup
          v-model="event.pets"
          name="pets"
          :options="petOptions"
          vertical
        ></BaseRadioGroup>
      </div>
    </fieldset>
  </section>
</template>

<script>
export default {
  emits: ["review-submitted"],
  data() {
    return {
      name: "",
      name1: "",
      review: "",
      rating: null,
      rates: [5, 4, 3, 2, 1],
      // solution
      recommend: null,
      recommends: ["Yes", "No"],
      // solution
      Submit: "",
      // event for from data
      event: {
        category: "",
        title: "",
        description: "",
        location: "",
        pets: 1,
        extras: {
          catering: false,
          music: false,
        },
      },
      petOptions: [
        { label: "yes", value: 1 },
        { label: "No", value: 0 },
      ],
    };
  },
  setup() {
    return {};
  },
  methods: {
    onSubmit() {
      if (
        this.name === "" ||
        this.review === "" ||
        this.rating === null ||
        this.recommend === null
      ) {
        alert("Review is incomplete. Please fill out every field.");
        return;
      }
      let productReview = {
        name: this.name,
        review: this.review,
        rating: this.rating,
        recommend: this.recommend,
      };
      this.$emit("review-submitted", productReview);
      this.name = "";
      this.review = "";
      this.rating = null;
    },
    isRequired(value) {
      if (value && value.trim()) {
        return true;
      }

      return "This is required";
    },
  },
};
</script>

<style scoped>
section {
  width: 60%;
}
</style>
