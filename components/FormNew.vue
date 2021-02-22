<template>
    <div>
      <button @click="showNewForm = !showNewForm" class="rounded-md w-full n-location h-16 mb-8" v-show="!showNewForm">
        <p class="font-normal text-base text-white pl-6">Add New Location</p>
        <svg width="17" height="16" viewBox="0 0 17 16" fill="none" xmlns="http://www.w3.org/2000/svg">
          <line x1="9" y1="5.37286e-08" x2="9" y2="16" stroke="white"/>
          <line x1="16.5" y1="8.5" x2="0.5" y2="8.5" stroke="white"/>
        </svg>
      </button>
      <div class="shadow-xl mb-6 bg-white rounded-lg w-full pt-6 pr-6 pl-6" v-show="showNewForm">
        <header class="w-full localization mb-10 left">
          <h1 class="text-base font-bold left">New Location</h1>
          <svg width="14" height="14" viewBox="0 0 14 14" fill="none" class="right" xmlns="http://www.w3.org/2000/svg" @click="showNewForm = !showNewForm">
            <path d="M1 13L13 1L1 13ZM1 1L13 13L1 1Z" fill="#989EA7"/><path d="M1 1L13 13M1 13L13 1L1 13Z" stroke="#989EA7" stroke-linecap="round" stroke-linejoin="round"/>
          </svg>
        </header>
        <form v-on:submit.prevent="checkForm()">
            <p v-if="errors.length">
              <b>Please fix the following errors:</b>
              <ul class="pb-6">
                <li v-for="error in errors" :key="error" class="error">{{ error }}</li>
              </ul>
            </p>
            <p>
              <label class="text-base mb-1" for="title">Title *</label>
              <input class="h-10 rounded mb-6 w-full" id="title" v-model="title" type="text" name="title">
            </p>
            <p>
              <label class="text-base mb-1" for="address">Enter the address *</label>
              <input class="h-10 rounded mb-6 w-full" id="address" v-model="address" type="text" name="address">
            </p>
            <p class="mb-4 hr text-xs font-normal mt-10">Contact information</p>
            <hr class="mb-8 w-full">
            <p>
              <label class="text-base mb-1" for="name">Full name *</label>
              <input class="h-10 rounded mb-6 w-full" id="name" v-model="name" type="text" name="name">
            </p>
            <p>
              <label class="text-base mb-1" for="position">Job Position *</label>
              <input class="h-10 rounded mb-6 w-full" id="position" v-model="position" type="text" name="position">
            </p>
            <p>
              <label class="text-base mb-1" for="email">Email address *</label>
              <input class="h-10 rounded mb-6 w-full" id="email" v-model="email" type="email" name="email">
            </p>
             <p>
              <label class="text-base mb-1" for="phone">Phone *</label>
              <input class="h-10 rounded mb-6 w-full" id="phone" v-model="phone" type="text" name="phone">
            </p>
            <p class="pb-6 w-full"><button type="submit" value="" :disabled='isDisabled' class="text-base rounded w-16 h-10">Save</button></p>
        </form>
        </div>
    </div>
</template>

<script>
export default {
  data() {
    return {
      showNewForm: false,
      errors: [],
      title: "",
      address: "",
      name: "",
      position: "",
      email: "",
      phone: "",
    };
  },
  computed: {
    isDisabled: function () {
      return (
        !this.title ||
        !this.address ||
        !this.name ||
        !this.position ||
        !this.email ||
        !this.phone
      );
    },
  },
  methods: {
    checkForm: function ($event) {
      this.errors = [];
      if (!this.title) {
        this.errors.push("Title is required.");
      }
      if (!this.address) {
        this.errors.push("Address is required.");
      }
      if (!this.name) {
        this.errors.push("Name is required.");
      }
      if (!this.position) {
        this.errors.push("Position is required.");
      }
      if (!this.email) {
        this.errors.push("Email is required.");
      } else if (!this.validEmail(this.email)) {
        this.errors.push("Use a valid email address.");
      }
      if (!this.phone) {
        this.errors.push("Phone is required.");
      }
      if (!this.errors.length) {
        this.$emit("addTodo", {
          title: this.title,
          address: this.address,
          name: this.name,
          position: this.position,
          email: this.email,
          phone: this.phone,
          //component: this,
        });
        this.title = "";
        this.address = "";
        this.name = "";
        this.position = "";
        this.email = "";
        this.phone = "";
        this.showNewForm = !this.showNewForm;
        return true;
      }
    },
    validEmail: function (email) {
      var re = /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
      return re.test(email);
    },
    closeEdit: function ($event) {
      this.$emit("addTodo", {
        component: this,
      });
    },
  },
};
</script>

<style>
form p label {
  display: block;
  color: #313e4f;
}
form p input {
  box-shadow: 0px 1px 2px rgba(0, 0, 0, 0.06), 0px 1px 3px rgba(0, 0, 0, 0.1);
  border: 1px solid #313e4f;
  background: #ffffff;
  color: #313e4f;
  padding: 0 12px;
  display: block;
}
form p input:focus {
  border: 1px solid #33a6ba;
}
input[type="text"] {
  -webkit-transition: 0.5s;
  transition: 0.5s;
  outline: none;
}

input[type="text"]:focus {
  border: 1px solid #33a6ba;
}
.localization h1 {
  color: #313e4f;
  text-align: left;
}
p.hr {
  text-transform: uppercase;
  color: #33a6ba;
}
form button {
  background: #33a6ba;
  display: block;
  color: white;
}
li.error {
  color: #ff7b92;
}
.n-location {
  box-shadow: 0px 10px 15px -5px rgba(0, 0, 0, 0.1),
    0px 4px 6px rgba(0, 0, 0, 0.05);
  background: #33a6ba;
  position: relative;
  text-align: left;
}
.n-location svg {
  position: absolute;
  display: block;
  right: 24px;
  top: 35%;
}
header svg {
  cursor: pointer;
}
button:disabled,
button[disabled] {
  background: #989ea7;
  color: white;
  opacity: 0.5;
}
</style>