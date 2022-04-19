<template>
  <div id="app" class="flex container h-screen w-full">
    <!-- side bar -->
    <div class="lg:w-1/5 border-r border-lighter px-2 lg:px-6 py-2 flex flex-col justify-between">
      <div>
        <button class="logo h-12 w-12 hover:bg-blue text-3xl text-blue">
          <i class="fa-brands fa-twitter"></i>
        </button>
        <div>
          <button
            :key="tab.id"
            v-for="tab in tabs"
            @click="clickHandler(tab.id)"
            :class="`hv hover:text-blue flex items-center py-2 px-4 hover:bg-lightblue founded-full mr-auto mb-3 ${
              id === tab.id ? 'tx-blue' : ''
            }`"
          >
            <i :class="`${tab.icon} text-2xl mr-4 text-left`"></i>
            <p class="text-lg font-semibold text-left hidden lg:block">
              {{ tab.title }}
            </p>
          </button>
        </div>
        <button
          class="bg-blue text-white rounded-full font-semibold focus:outline-none w-12 h-12 lg:w-full p-3 hover:bg-darkblue"
        >
          <p class="hidden lg:block">
            Twitter
          </p>
          <i class="fas fa-plus  lg:hidden"></i>
        </button>
      </div>
      <div class="lg:w-full relative">
        <button @click="dropdown = true" class="flex items-center w-full hover:bg-lightblue rounded-full p-2 focus:outline-none">
          <img src="https://cdn.pixabay.com/photo/2018/01/15/07/51/woman-3083376__340.jpg" class="w-10 h-10 rounded-full border border-lighter" />
          <div class="hidden lg:block ml-4">
            <p class="text-sm font-bold leading-tight"> Steph Dietz </p>
            <p class="text-sm leading-tight"> @SaaSyEth </p>
          </div>
          <i class="hidden lg:block fas fa-angle-down ml-auto text-lg"></i>
        </button>
        <div v-if="dropdown === true" class="absolute bottom-0 left-0 w-64 rounded-lg shadow-md border-lightest bg-white mb-16">
          <button @click="dropdown = false" class="p-3 flex items-center w-full hover:bg-lightest p-2 focus:outline-none">
            <img src="https://cdn.pixabay.com/photo/2018/01/15/07/51/woman-3083376__340.jpg" class="w-10 h-10 rounded-full border border-lighter" />
            <div class="ml-4">
              <p class="text-sm font-bold leading-tight"> Steph Dietz </p>
              <p class="text-sm leading-tight"> @SaaSyEth </p>
            </div>
            <i class="fas fa-check ml-auto test-blue"></i>
          </button>
          <button @click="dropdown = false" class="w-full text-left hover:bg-lightest border-t border-lighter p-3 test-sm focus:outline-none">
            Add an existing account
          </button>
          <button @click="dropdown = false" class="w-full text-left hover:bg-lightest border-t border-lighter p-3 test-sm focus:outline-none">
            Log out @SaaSyEth
          </button>
        </div>
      </div>
      <!-- <div class="w-full relative">
         <button class="flex justify-between w-full hover:bg-lightest rounded-full p-2">
            <img class="w-12 h-12 rounded-full" src="https://cdn.pixabay.com/photo/2018/01/15/07/51/woman-3083376__340.jpg" alt="">
            <div class="ml-4">
              <p class="text-sm font-bold leading-tight">Akhmadjon</p>
              <p class="text-sm leading-tight">@akhmadjon-dev</p>
            </div>
            <i class="fas fa-angle-down ml-auto text-lg"></i>
         </button>
          <div class="absolute bottom-0 left-0 w-64 rounded-lg shadow-md border-lightest bg-white">
              <button class="flex items-center w-full hover:bg-lightest p-2">
                  <img class="w-12 h-12 rounded-full" src="https://cdn.pixabay.com/photo/2018/01/15/07/51/woman-3083376__340.jpg" alt="">
                  <div class="ml-4">
                    <p class="text-sm font-bold leading-tight">Akhmadjon</p>
                    <p class="text-sm leading-tight">@akhmadjon-dev</p>
                  </div>
                  <i class="fas fa-check ml-auto text-blue"></i>
              </button>
         </div>
      </div> -->
    </div>
  </div>
</template>

<script>
// import Main from "./components/Main.vue";
export default {
  name: "App",
  components: {
    // Main,
  },
  methods: {
    clickHandler(id) {
      console.log(id);
      this.id = id;
    },
  },
  data() {
    return {
      tabs: [
        { icon: "fas fa-home", title: "Home", id: "home" },
        { icon: "fas fa-hashtag", title: "Explore", id: "explore" },
        { icon: "far fa-bell", title: "Notifications", id: "notifications" },
        { icon: "far fa-envelope", title: "Messages", id: "messages" },
        { icon: "far fa-bookmark", title: "Bookmarks", id: "bookmarks" },
        { icon: "fas fa-clipboard-list", title: "Lists", id: "lists" },
        { icon: "far fa-user", title: "Profile", id: "profile" },
        { icon: "fas fa-ellipsis-h", title: "More", id: "more" },
      ],
      id: "home",
      dropdown: false,
    };
  },
};
</script>

<style scoped>
i:hover {
  color: #1da1f2;
}
.hv:hover i,
.hv:hover p {
  color: #1da1f2;
}
.tx-blue {
  color: #1da1f2;
}
img{
  object-fit: cover ;
}
</style>
