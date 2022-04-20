<template>
  <div id="app" class="flex h-screen w-full">
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
          <img src="https://cdn.pixabay.com/photo/2012/04/18/23/36/boy-38262__340.png" class="w-10 h-10 rounded-full border border-lighter" />
          <div class="hidden lg:block ml-4">
            <p class="text-sm font-bold leading-tight"> Akhmadjon A </p>
            <p class="text-sm leading-tight"> @Akhmadjon-dev </p>
          </div>
          <i class="hidden lg:block fas fa-angle-down ml-auto text-lg"></i>
        </button>
        <div v-if="dropdown === true" class="absolute bottom-0 left-0 w-64 rounded-lg shadow-md border-lightest bg-white mb-16">
          <button @click="dropdown = false" class="p-3 flex items-center w-full hover:bg-lightest p-2 focus:outline-none">
            <img src="https://cdn.pixabay.com/photo/2012/04/18/23/36/boy-38262__340.png" class="w-10 h-10 rounded-full border border-lighter" />
            <div class="ml-4">
              <p class="text-sm font-bold leading-tight"> Akhmadjon A </p>
              <p class="text-sm leading-tight"> @Akhmadjon-dev </p>
            </div>
            <i class="fas fa-check ml-auto test-blue"></i>
          </button>
          <button @click="dropdown = false" class="w-full text-left hover:bg-lightest border-t border-lighter p-3 test-sm focus:outline-none">
            Add an existing account
          </button>
          <button @click="dropdown = false" class="w-full text-left hover:bg-lightest border-t border-lighter p-3 test-sm focus:outline-none">
            Log out @Akhmadjon-dev
          </button>
        </div>
      </div>
    </div>
    <!-- tweets -->
    <div class="w-1/2 h-full overflow-y-scroll">
      <div class="px-5 py-3 border-b border-lighter flex items-center justify-between">
        <h1 class="text-xl font-bold">Home</h1>
        <i class="far fa-star text-xl text-blue"></i>
      </div>
       <div class="px-5 py-3 border-b-8 border-lighter flex">
        <div class="flex-none">
          <img src="https://cdn.pixabay.com/photo/2012/04/18/23/36/boy-38262__340.png" class="flex-none w-12 h-12 rounded-full border border-lighter"/>
        </div>
        <form @submit= "addNewTweet" class="w-full px-4 relative">
          <input v-model="tweet.content" placeholder="What's up?" class="mt-3 pb-3 w-full focus:outline-none"/>
          <div class="flex items-center">
            <i class="text-lg text-blue mr-4 far fa-image"></i>
            <i class="text-lg text-blue mr-4 fas fa-film"></i>
            <i class="text-lg text-blue mr-4 far fa-chart-bar"></i>
            <i class="text-lg text-blue mr-4 far fa-smile"></i>
          </div>
          <button type="submit" class="h-10 px-4 text-white font-semibold bg-blue hover:bg-darkblue focus:outline-none rounded-full absolute bottom-0 right-0">
            Tweet
          </button>
        </form>
      </div>
      <div class="flex flex-col-reverse">
        <div :key="tweet.content" v-for="tweet in tweets" class="w-full p-4 border-b hover:bg-lighter flex">
          <div class="flex-none mr-4">
            <img src="https://cdn.pixabay.com/photo/2012/04/18/23/36/boy-38262__340.png" class="h-12 w-12 rounded-full flex-none"/>
          </div>
          <div class="w-full">
            <div class="flex items-center w-full">
              <p class="font-semibold"> Steph Dietz </p>
              <p class="text-sm text-dark ml-2"> @SaaSyEth </p>
              <p class="text-sm text-dark ml-2"> 1 sec </p>
              <i class="fas fa-angle-down text-dark ml-auto"></i>
            </div>
            <p class="py-2">
              {{ tweet.content }}
            </p>
            <div class="flex items-center justify-between w-full">
              <div class="flex items-center text-sm text-dark">
                <i class="far fa-comment mr-3"></i>
                <p> 0 </p>
              </div>
              <div class="flex items-center text-sm text-dark">
                <i class="fas fa-retweet mr-3"></i>
                <p> 0 </p>
              </div>
              <div class="flex items-center text-sm text-dark">
                <i class="fas fa-heart mr-3"></i>
                <p> 1 </p>
              </div>
              <div class="flex items-center text-sm text-dark">
                <i class="fas fa-share-square mr-3"></i>
              </div>
            </div>
          </div>
        </div>
      </div>
      <div :key="follow.comment" v-for="follow in following" class="w-full p-4 border-b hover:bg-lighter flex">
        <div class="flex-none mr-4 ">
          <img class="h-12 w-12 rounded-full flex-none" :src="`${follow.src}`" alt="">
        </div>
        <div class="w-full">
          <div class="flex items-center w-full">
            <p class="font-semibold">
              {{follow.name}}
            </p>
            <p class="text-sm text-dark ml-2">
              {{follow.handle}}
            </p>
            <p class="text-sm text-dark ml-2">
              {{follow.time}}
            </p>
            <i class="fas fa-angle-down text-dark ml-auto"></i>
          </div>
          <p class="py-2 ">
            {{follow.tweet}}
          </p>
          <div class="flex items-center justify-between w-full">
            <div class="flex items-center text-sm text-dark">
              <i class="far fa-comment mr-3"></i>
              <p>
                {{follow.comment}}
              </p>
            </div>
            <div class="flex items-center text-sm text-dark">
              <i class="far fa-comment mr-3"></i>
              <p>
                {{follow.retweets}}
              </p>
            </div>
            <div class="flex items-center text-sm text-dark">
              <i class="fas fa-retweet mr-3"></i>
              <p>
                {{follow.like }}
              </p>
            </div>
            <div class="flex items-center text-sm text-dark">
              <i class="fas fa-heart mr-3"></i>
            </div> 
          </div>
        </div>
      </div>
    </div>
    <!-- trending -->
    <div class="md:block hidden bg-light w-1/3 h-full border-l items-center border-lighter py-2 px-6 overflow-y-scroll relative">
      <input class="pl-12 rounded-full w-full bg-lighter p-2 text-sm"  placeholder="Search twitter"/>
      <i class="fas fa-search absolute left-0 top-0 mt-5 ml-12 text-sm text-light"></i>
      <div class="w-full rounded-lg bg-lightest mt-12">
        <div class="flex items-center justify-between p-3">
          <p class="text-lg font-bold">Trends for You</p>
          <i class="fas fa-cog text-lg font-bold tx-blue"></i>
        </div>
        <button :key="trend.title" v-for="trend in trends" class="w-full flex justify-between hover:bg-lighter p-3 border-t border-lighter">
          <div>
            <p class="text-sm text-left leading-tight text-dark">
              {{ trend.top }}
            </p>
            <p class="font-bold text-left leading-tight">
              {{ trend.title }}
            </p>
            <p class=" text-left leading-tight text-dark">
              {{ trend.bottom }}
            </p>
          </div>
          <i class="fas fa-angle-down text-lg text-dark"></i>
        </button>
        <button class="pt-3 w-full hover:bg-lighter text-left tx-blue border-t border-lighter">
          Show more
        </button>
      </div>
      <div class="w-full rounded-lg bg-lightest my-4">
        <div class=" p-3">
          <p class="text-lg font-bold">Who to Follow</p>
        </div>
        <button :key="friend.id" v-for="friend in friends" class="w-full flex hover:bg-lighter p-3 border-t border-lighter">
          <img :src="`${ friend.src }`" class="w-12 h-12 rounded-full border border-lighter" />
          <div class="hidden lg:block ml-4">
            <p class="text-sm font-bold leading-tight"> {{ friend.name }} </p>
            <p class="text-sm leading-tight"> {{ friend.handle }} </p>
          </div>
          <button class="ml-auto text-sm tx-blue py-1 px-4 rounded-full border-2 border-blue">
            Follow
          </button>
        </button>
        <button class="p-3 w-full hover:bg-lighter text-left tx-blue border-t border-lighter">
          Show More
        </button>
      </div>
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
      trends: [
        {top: 'Trending in TX', title: 'Gigi', bottom: 'Trending with: Rip Gigi'},
        {top: 'Music', title: 'We Won', bottom: '135K Tweets'},
        {top: 'Pop', title: 'Blue Ivy', bottom: '40k tweets'},
        {top: 'Trending in US', title: 'Denim Day', bottom: '40k tweets'},
        {top: 'Trending', title: 'When Beyonce', bottom: '25.4k tweets'},
      ],
      friends: [
        {src: 'https://cdn.pixabay.com/photo/2015/06/22/08/40/child-817373__480.jpg', name: 'Elon Musk', handle: '@teslaBoy'},
        {src: 'https://cdn.pixabay.com/photo/2014/04/05/13/05/boy-317041__480.jpg', name: 'Adrian Monk', handle: '@detective:)'},
        {src: 'https://cdn.pixabay.com/photo/2016/03/12/21/05/boy-1252771__480.jpg', name: 'Kevin Hart', handle: '@miniRock'}
      ],
       following: [
        {src: 'https://cdn.pixabay.com/photo/2012/04/18/23/36/boy-38262__340.png', name: 'Elon Musk', handle: '@teslaBoy', time: '20 min', tweet: 'Should I just quarantine on mars??', comments: '1,000', retweets: '550', like: '1,000,003'},
        {src: 'https://cdn.pixabay.com/photo/2016/03/23/04/01/woman-1274056__340.jpg', name: 'Kevin Hart', handle: '@miniRock', time: '55 min', tweet: 'Should me and the rock do another sub-par movie together????', comments: '2,030', retweets: '50', like: '20,003'},
        {src: 'https://cdn.pixabay.com/photo/2012/04/18/23/36/boy-38262__340.png', name: 'Elon Musk', handle: '@teslaBoy', time: '1.4 hr', tweet: 'Haha just made a flame thrower. Shld I sell them?', comments: '100,000', retweets: '1,000,002', like: '5,000,003'},
        {src: 'https://cdn.pixabay.com/photo/2012/04/18/23/36/boy-38262__340.png', name: 'Elon Musk', handle: '@teslaBoy', time: '1.4 hr', tweet: 'Just did something crazyyyyyyy', comments: '100,500', retweets: '1,000,032', like: '5,000,103'}
      ],
       tweets: [
        {content: 'It is so nice outside!'}
      ],
      tweet: {content: ''}
    };
    
  },
  methods: {
    clickHandler(id) {
      console.log(id);
      this.id = id;
    },
    addNewTweet(e) {
      e.preventDefault()
      let newTweet = {
        content: this.tweet.content
      };
      this.tweet.content = ''
      this.tweets.push (newTweet)
    }
  }
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
