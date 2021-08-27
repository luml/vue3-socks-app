<template>
  <form class="review-form" @submit.prevent="onSubmit">
    <h3>Leave a review</h3>

    <!-- <label for="name">Name:</label> -->
    <!-- <input id="name" v-model="name" /> -->
    <BaseInput v-model="name" label="Name" type="text" />

    <label for="review">Review:</label>
    <textarea id="review" placeholder="Anything" v-model="review"></textarea>

    <!-- <label for="rating">Rating:</label>
    <select id="rating" v-model.number="rating">
      <option>5</option>
      <option>4</option>
      <option>3</option>
      <option>2</option>
      <option>1</option>
    </select> -->
    <base-select :options="rates" v-model="rating" label="Rating" />

    <!-- solution -->
    <!-- <label for="recommend">Would you recommend this product?</label>
    <select id="recommend" v-model="recommend">
      <option>Yes</option>
      <option>No</option>
    </select> -->
    <BaseSelect
      :options="recommends"
      v-model="recommend"
      label="Would you recommend this product?"
    />

    <!-- solution -->
    <!-- <input class="button" type="submit" value="Submit" /> -->
    <BaseInput v-model="Submit" label="Submit" type="submit" />

    <!-- other extra base -->
    <h3>Extras</h3>
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

    <h3>Are Pets allowed ?</h3>
    <div>
      <BaseRadioGroup
        v-model="event.pets"
        name="pets"
        :options="petOptions"
        vertical
      ></BaseRadioGroup>
    </div>
  </form>
</template>

<script>
export default {
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

<style lang="scss" scoped></style>
