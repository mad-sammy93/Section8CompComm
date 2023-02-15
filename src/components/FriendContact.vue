<template>
  <li>
    <h2>{{ name }} </h2>
    <button @click="toggleDetails">{{ detailsAreVisible ? 'Hide' : 'Show' }} Details</button>
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
  // props:[
  //   'name',
  //   'phoneNumber',
  //   'emailAddress',
  //   'isFavourite'
  // ],
  props:{
    id:{
      type: String,
      required:true,
    },
    name: {
      type:String,
      required:true
    },
    phoneNumber: {
      type:String,
      required:true
    },
    emailAddress: {
      type:String,
      required:true
    },
    isFavourite: {
      type:String,
      required:true,
      default: 0,
      validator: function(){
        return value === '1' || value === '0';
      }
    },
  },

  data() {
    return {
      detailsAreVisible: false,
      // friend: {
      //   id: "manuel",
      //   name: "Manuel Lorenz",
      //   phone: "0123 45678 90",
      //   email: "manuel@localhost.com",
      // },
      friendIsFavourite:this.isFavourite,
    };
  },
  methods: {
    toggleDetails() {
      this.detailsAreVisible = !this.detailsAreVisible;
    },
    toggleFavourite(){
      // this.friendIsFavourite = !this.friendIsFavourite;   
      this.$emit('toggle-favourite', this.id);   
    }
  }
};
</script>