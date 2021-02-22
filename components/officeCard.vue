<template>
  <div>
    <header class="mt-20">
      <h1 class="mb-12 font-light text-6xl">Offices</h1>
      <FormNew @addTodo="newForms($event)" />
    </header>
    <ul class="office-card w-full">
      <li
        v-for="(office, index) in offices"
        :key="index"
        class="shadow-xl mb-6 bg-white rounded-lg w-full"
        @click="openOffices(office.id)"
      >
        <div
          class="w-full h-32 pt-8"
          :class="{
            openOffices: classOffice == office.id,
            closeOffices: visibleUser == office.id,
          }"
        >
          <hgroup class="pl-6 w-full">
            <h1 class="text-2xl font-bold">{{ office.title }}</h1>
            <p class="text-base font-light">{{ office.address }}</p>
            <svg
              width="18"
              :class="{ rotate: classOffice == office.id }"
              height="10"
              viewBox="0 0 18 10"
              fill="none"
              xmlns="http://www.w3.org/2000/svg"
            >
              <path
                d="M1 1L9 9L17 1"
                stroke="#33A6BA"
                stroke-linecap="round"
                stroke-linejoin="round"
              />
            </svg>
          </hgroup>
        </div>
        <article
          v-if="classOffice == office.id"
          class="pt-6 pr-6 pl-6 w-full"
          :class="{ closeOffices: visibleUser == office.id }"
        >
          <h1 class="font-bold text-xl pb-2">{{ office.name }}</h1>
          <p class="text-base font-normal pb-2">{{ office.position }}</p>
          <a
            class="text-base font-normal pb-2"
            :title="office.position"
            accesskey="m"
            >{{ office.email }}</a
          >
          <p class="text-base font-normal pb-4">{{ office.phone }}</p>
          <footer class="grid grid-flow-col auto-cols-max">
            <div>
              <a
                class="w-1/2 text-xs pb-6 pt-6"
                title="EDIT"
                accesskey="e"
                @click="editUser(office.id)"
              >
                <svg
                  width="20"
                  height="21"
                  viewBox="0 0 20 21"
                  fill="none"
                  xmlns="http://www.w3.org/2000/svg"
                >
                  <path
                    d="M13.232 3.23199L16.768 6.76799M14.732 1.73199C15.2009 1.26309 15.8369 0.999664 16.5 0.999664C17.1631 0.999664 17.7991 1.26309 18.268 1.73199C18.7369 2.2009 19.0003 2.83687 19.0003 3.49999C19.0003 4.16312 18.7369 4.79909 18.268 5.26799L4.5 19.036H1V15.464L14.732 1.73199Z"
                    stroke="#989EA7"
                    stroke-width="2"
                    stroke-linecap="round"
                    stroke-linejoin="round"
                  />
                </svg>
                <span class="pl-2">EDIT</span>
              </a>
            </div>
            <div>
              <a
                class="w-1/2 text-xs pb-6 pt-6"
                title="DELETE"
                accesskey="d"
                @click="deletarUser(office)"
              >
                <svg
                  width="18"
                  height="20"
                  viewBox="0 0 18 20"
                  fill="none"
                  xmlns="http://www.w3.org/2000/svg"
                >
                  <path
                    d="M7 9V15M11 9V15M1 5H17M16 5L15.133 17.142C15.0971 17.6466 14.8713 18.1188 14.5011 18.4636C14.1309 18.8083 13.6439 19 13.138 19H4.862C4.35614 19 3.86907 18.8083 3.49889 18.4636C3.1287 18.1188 2.90292 17.6466 2.867 17.142L2 5H16ZM12 5V2C12 1.73478 11.8946 1.48043 11.7071 1.29289C11.5196 1.10536 11.2652 1 11 1H7C6.73478 1 6.48043 1.10536 6.29289 1.29289C6.10536 1.48043 6 1.73478 6 2V5H12Z"
                    stroke="#FF7B92"
                    stroke-width="2"
                    stroke-linecap="round"
                    stroke-linejoin="round"
                  />
                </svg>
                <span class="pl-2">DELETE</span>
              </a>
            </div>
          </footer>
        </article>
        <article
          class="edit-location pt-6 pr-6 pl-6 w-full"
          v-show="visibleUser == office.id"
        >
          <FormEdit
            @addTodo="editForms($event, index)"
            :title="office.title"
            :address="office.address"
            :name="office.name"
            :position="office.position"
            :email="office.email"
            :phone="office.phone"
          />
        </article>
      </li>
    </ul>
  </div>
</template>

<script>
import FormEdit from "../components/FormEdit";
import FormNew from "../components/FormNew";

export default {
  data() {
    return {
      offices: [],
      classOffice: 0,
      visibleUser: 0,
    };
  },
  components: {
    FormEdit,
    FormNew,
  },
  methods: {
    newForms(params) {
      this.offices.push({
        id: this.offices.length + 1,
        title: params.title,
        address: params.address,
        name: params.name,
        position: params.position,
        email: params.email,
        phone: params.phone,
      });
      this.$emit("seeHeader", true);
      setTimeout(() => {
        this.$emit("seeHeader", false);
      }, 3000);
    },
    editForms(params, index) {
      Object.assign(this.offices[index], params);
      this.visibleUser = 0;
    },
    deletarUser: function (office) {
      this.offices.splice(this.offices.indexOf(office), 1);
      this.$emit("seeHeader", true);
      setTimeout(() => {
        this.$emit("seeHeader", false);
      }, 3000);
    },
    editUser: function (el) {
      this.visibleUser = el;
    },
    openOffices: function (el) {
      this.classOffice = el;
    },
  },
  watch: {
    offices: function (params) {},
  },
  async fetch() {
    this.offices = await this.$content("office").fetch();
  },
};
</script>

<style>
header h1 {
  text-align: center;
  color: #33a6ba;
}
ul.office-card li {
  position: relative;
  cursor: pointer;
}
ul.office-card li h1 {
  color: #313e4f;
}
ul.office-card li p {
  color: #989ea7;
}
ul.office-card li article p {
  color: #313e4f;
}
ul.office-card li .closeOffices {
  display: none;
}
ul.office-card li .openOffices {
  box-shadow: 0px 10px 15px -5px rgba(0, 0, 0, 0.1),
    0px 4px 6px rgba(0, 0, 0, 0.05);
  -webkit-border-top-left-radius: 0.5rem;
  -webkit-border-top-right-radius: 0.5rem;
  -moz-border-radius-topleft: 0.5rem;
  -moz-border-radius-topright: 0.5rem;
  border-top-left-radius: 0.5rem;
  border-top-right-radius: 0.5rem;
  -moz-transition: all 0.4s ease-in;
  -webkit-transition: all 0.4s ease-in;
  -o-transition: all 0.4s ease-in;
  transition: all 0.4s ease-in;
  background: #989ea7;
}
ul.office-card li .openOffices h1,
ul.office-card li .openOffices p {
  color: white;
}
hgroup {
  position: relative;
}
hgroup svg {
  position: absolute;
  display: block;
  right: 24px;
  top: 50%;
}

article h1 {
  color: #313e4f;
}
article p {
  color: #313e4f;
}
article a {
  color: #33a6ba;
  display: block;
}
article footer {
  border-top: 1px solid #e8edf3;
}
article footer a {
  cursor: pointer;
}
article footer div:first-child a {
  color: #989ea7;
}
article footer div:last-child a {
  color: #ff7b92;
  float: right;
}
article footer a svg {
  display: inline;
}
.rotate {
  animation: rotation 0.5s linear;
  transform: rotate(180deg);
  filter: brightness(10);
}

@keyframes rotation {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(180deg);
  }
}
</style>