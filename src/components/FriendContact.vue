<template>
  <li>
    <h2>{{ name }} {{ friendIsFavorite ? "(Favorite)" : "" }}</h2>
    <button @click="toggleFavorite">Toggle Favorite</button>
    <button @click="toggleDetails">
      {{ detailsAreVisible ? "Hide" : "Show" }} Details
    </button>
    <ul v-if="detailsAreVisible">
      <li>
        <strong>Phone:</strong>
        {{ phoneNumber }}
      </li>
      <li>
        <strong>Email:</strong>
        {{ emailAddress }}
      </li>
    </ul>
  </li>
</template>

<script>
export default {
  // props: [
  //   // define props use camel case
  //   // props should not be mutated
  //   "name",
  //   "phoneNumber",
  //   "emailAddress",
  //   "isFavorite",
  // ],
  props : {
    name: {
      type: String,
      required: true,
    },
    phoneNumber: {
      type: String,
      required: true,
    },
    emailAddress: {
      type: String,
      required: true,
    },
    isFavorite: {
      type: Boolean,
      required: false,
      default: false,
      // validator: function(value) {
      //   return value === '1' || value === '0';
      // }
    },
  },
  data() {
    return {
      detailsAreVisible: false,
      // if want mutated props value should inital new one
      friendIsFavorite: this.isFavorite
    };
  },
  methods: {
    toggleDetails() {
      this.detailsAreVisible = !this.detailsAreVisible;
    },
    // this function wiil be ERROR
    // because props should not be mutated (isFavorite) is came from App
    // toggleFavorite() {
    //   if (this.isFavorite === '1') {
    //     this.isFavorite = '0';
    //   } else {
    //     this.isFavorite = '1';
    //   }
    // }
    toggleFavorite() {
      this.friendIsFavorite = !this.friendIsFavorite
    }
  },
};
</script>