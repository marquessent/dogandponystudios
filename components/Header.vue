<template>
  <div>
    <header
      class="w-full header bg-white h-20"
      :class="{ visibledMod: visibledMod }"
    >
      <div class="container mx-auto px-4 max-w-xs min-w-xs">
        <p class="mt-8 text-xs font-normal">
          <svg
            width="16"
            height="12"
            viewBox="0 0 16 12"
            fill="none"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path
              d="M1 7L5 11L15 1"
              stroke="#33A6BA"
              stroke-width="2"
              stroke-linecap="round"
              stroke-linejoin="round"
            /></svg
          >The locaton has been updated.
        </p>
      </div>
      <svg
        @click="visibledMod = !visibledMod"
        width="15"
        height="14"
        viewBox="0 0 15 14"
        fill="none"
        xmlns="http://www.w3.org/2000/svg"
      >
        <path
          d="M1.16406 13L13.4928 1L1.16406 13ZM1.16406 1L13.4928 13L1.16406 1Z"
          fill="#989EA7"
        />
        <path
          d="M1.16406 1L13.4928 13M1.16406 13L13.4928 1L1.16406 13Z"
          stroke="#989EA7"
          stroke-width="2"
          stroke-linecap="round"
          stroke-linejoin="round"
        />
      </svg>
    </header>
  </div>
</template>

<script>
export default {
  data() {
    return {};
  },
  props: {
    visibledMod: Boolean,
  },
};
</script>

<style>
header.header {
  -moz-transition: opacity 0.4s ease-in-out;
  -o-transition: opacity 0.4s ease-in-out;
  -webkit-transition: opacity 0.4s ease-in-out;
  transition: opacity 0.4s ease-in-out;
  border-top: 2px solid #33a6ba;
  box-sizing: content-box;
  position: fixed;
  z-index: 999;
  opacity: 0;
  left: 0;
  top: 0;
}
header.header.visibledMod {
  opacity: 1;
}
header.header p {
  text-transform: uppercase;
  text-align: center;
  color: #313e4f;
}
header.header svg {
  float: left;
}
header.header > svg {
  position: absolute;
  right: 1%;
  top: 35%;
}
</style>