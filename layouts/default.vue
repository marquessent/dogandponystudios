<template>
  <div>
    <Header :visibledMod="this.visibledMod" />
    <div class="container mx-auto px-4 max-w-sm min-w-sm">
      <officeCard @seeHeader="editForms($event)" />
      <baseboard />
    </div>
  </div>
</template>

<script>
import Header from "../components/Header";
import baseboard from "../components/baseboard";
import officeCard from "../components/officeCard";

export default {
  data() {
    return {
      name: "",
      visibledMod: false,
    };
  },
  components: {
    officeCard,
    baseboard,
    Header,
  },
  methods: {
    editForms(params, index) {
      this.visibledMod = params;
    },
  },
};
</script>

<style>
body {
  background: #e8edf3;
}
.clearfix {
  display: block;
  content: "";
  clear: both;
}
.left {
  float: left;
}
.right {
  float: right;
}
</style>