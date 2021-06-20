<template>
  <li>
    <h2>{{ name }} {{ isFavorite ? "(Favorite)" : "" }}</h2>
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
    <button @click="$emit('delete', id)">Delete</button>
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
    id: {
      type: String,
      required: true
    },
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
  // tell which custom events this component will eventually emit
  emits: ['toggle-favorite', 'delete'],
  // emits: {
  //   'toggle-favorite': function(id) {
  //     if (id) {
  //       return ture;
  //     } else {
  //       console.log('Id is missing!');
  //       return false
  //     }
  //   }
  // },
  data() {
    return {
      detailsAreVisible: false,
      // if want mutated props value should inital new one
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
      // this.friendIsFavorite = !this.friendIsFavorite
      // .$emit() can call from inside a Vue component
      // allows to emit custom event to which you then 
      // can listen from inside the parent component
      // emit wants at least one argument, the name of the custom event
      this.$emit('toggle-favorite', this.id);
    },

  },
};
</script>