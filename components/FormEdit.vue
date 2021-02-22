<template>
    <div>
        <header class="w-full localization mb-10 left">
          <h1 class="text-base font-bold left">Edit Location</h1>
          <svg width="14" height="14" viewBox="0 0 14 14" fill="none" class="right" xmlns="http://www.w3.org/2000/svg" @click="closeEdit()">
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
              <input class="h-10 rounded mb-6 w-full" id="title" v-model="nTitle" type="text" name="title">
            </p>
            <p>
              <label class="text-base mb-1" for="address">Enter the address *</label>
              <input class="h-10 rounded mb-6 w-full" id="address" v-model="nAddress" type="text" name="address">
            </p>
            <p class="mb-4 hr text-xs font-normal mt-10">Contact information</p>
            <hr class="mb-8 w-full">
            <p>
              <label class="text-base mb-1" for="name">Full name *</label>
              <input class="h-10 rounded mb-6 w-full" id="name" v-model="nName" type="text" name="name">
            </p>
            <p>
              <label class="text-base mb-1" for="position">Job Position *</label>
              <input class="h-10 rounded mb-6 w-full" id="position" v-model="nPosition" type="text" name="position">
            </p>
            <p>
              <label class="text-base mb-1" for="email">Email address *</label>
              <input class="h-10 rounded mb-6 w-full" id="email" v-model="nEmail" type="email" name="email">
            </p>
             <p>
              <label class="text-base mb-1" for="phone">Phone *</label>
              <input class="h-10 rounded mb-6 w-full" id="phone" v-model="nPhone" type="text" name="phone">
            </p>
            <p class="pb-6 w-full"><button type="submit" value="" :disabled='isDisabled' class="text-base rounded w-16 h-10">Save</button></p>
        </form>
    </div>
</template>

<script>
export default {
  data() {
    return {
      errors: [],
      nTitle: this.title,
      nAddress: this.address,
      nName: this.name,
      nPosition: this.position,
      nEmail: this.email,
      nPhone: this.phone,
    };
  },
  computed: {
    isDisabled: function () {
      return (
        !this.nTitle ||
        !this.nAddress ||
        !this.nName ||
        !this.nPosition ||
        !this.nEmail ||
        !this.nPhone
      );
    },
  },
  props: {
    title: String,
    address: String,
    name: String,
    position: String,
    email: String,
    phone: String,
  },
  methods: {
    checkForm: function ($event) {
      this.errors = [];
      if (!this.nTitle) {
        this.errors.push("Title is required.");
      }
      if (!this.nAddress) {
        this.errors.push("Address is required.");
      }
      if (!this.nName) {
        this.errors.push("Name is required.");
      }
      if (!this.nPosition) {
        this.errors.push("Position is required.");
      }
      if (!this.nEmail) {
        this.errors.push("Email is required.");
      } else if (!this.validEmail(this.nEmail)) {
        this.errors.push("Use a valid email address.");
      }
      if (!this.nPhone) {
        this.errors.push("Phone is required.");
      }
      if (!this.errors.length) {
        this.$emit("addTodo", {
          title: this.nTitle,
          address: this.nAddress,
          name: this.nName,
          position: this.nPosition,
          email: this.nEmail,
          phone: this.nPhone,
          component: this,
        });
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
</style>