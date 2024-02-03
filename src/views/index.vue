<template>
  <main>
    <header class="w-full h-36 bg-[url('/images/bg-header-desktop.svg')]">
      <img src="" alt="" />
    </header>

    <!-- ///////////////////////////////////////////////////////////// -->

    <section
      class="w-full border flex flex-col items-center bg-[#effafa] relative"
    >
      <div class="absolute top-[-35px] left-[190px] w-full flex " v-if="selectedFilter.length">
        <div class="flex justify-between items-center w-[80%] h-16 border bg-[#fff] rounded-[15px] px-10">
            <span
          class="flex  items-center gap-5"
        >
          <span
            class="px-2 bg-[#effafa] text-[#5ba4a4] flex justify-center items-center gap-x-3 rounded-[10px]"
            v-for="(item, index) in selectedFilter"
            :key="index"
            >{{ item }}
            <svg
              xmlns="http://www.w3.org/2000/svg"
              fill="none"
              viewBox="0 0 24 24"
              stroke-width="1.5"
              stroke="currentColor"
              class="w-7 h-5  text-white bg-[#5ba4a4] rounded-[10px] cursor-pointer"
              @click="close(item)"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                d="M6 18 18 6M6 6l12 12"
              />
            </svg>
          </span>

        </span>
        <span class="text-gray-500 font-bold text-xl" @click="clear">clear</span>
        </div>
          
      </div>
      <div
        class="lg:w-[80%] w-[90%] lg:h-40 h-72 mt-10 bg-white lg:flex items-center lg:justify-between rounded-[5px] lg:px-5 border-l-4 border-[#5ba4a4]"
        v-for="(cart, index) in filteredCards"
        :key="index"
      >
        <!-- ///////////////////////////////// -->
        <section class="lg:flex gap-x-5">
          <img :src="cart.img" alt="" class="w-28 h-28" />
          <div class="flex flex-col gap-y-3">
            <div class="flex gap-x-3">
              <h2 class="font-bold text-2xl text-[#5ba4a4]">
                {{ cart.tittle }}
              </h2>
              <span
                class="bg-[#5ba4a4] flex justify-center font-bold items-center p-2 text-sm rounded-[15px] text-[#fff]"
                >NEW</span
              >
              <span
                class="bg-black text-[#fff] font-bold flex justify-center items-center px-2 text-sm rounded-[16px]"
                >FEATURED</span
              >
            </div>
            <p class="text-black font-bold text-[1.2rem]">{{ cart.p }}</p>
            <div class="flex">
              <ul class="flex gap-x-4">
                <li class="text-gray-500 text-sm font-bold">1d ago</li>
                <li class="text-gray-500 text-sm font-bold">Full Time</li>
                <li class="text-gray-500 text-sm font-bold">USA Only</li>
              </ul>
            </div>
          </div>
        </section>
        <!-- ////////////////////////// -->

        <!-- <div class="flex gap-x-5  mt-10 lg:mt-0">
                <span v-if="cart.span1" class="bg-[#effafa] text-[#5ba4a4] font-bold rounded-[4px] flex justify-center items-center py-1 px-2  text-center text-sm">{{cart.span1}}</span>
                    <span v-if="cart.span2" class="bg-[#effafa] text-[#5ba4a4] font-bold rounded-[4px] flex justify-center items-center py-1 px-2  text-center text-sm">{{cart.span2}}</span>
                    <span v-if="cart.span3" class="bg-[#effafa] text-[#5ba4a4] font-bold rounded-[4px] flex justify-center items-center py-1 px-2   text-center text-sm">{{cart.span3}}</span>
                    <span v-if="cart.span4" class="bg-[#effafa] text-[#5ba4a4] font-bold rounded-[4px] flex justify-center items-center py-1 px-2  text-center text-sm">{{cart.span4}}</span>
                    <span v-if="cart.span5" class="bg-[#effafa] text-[#5ba4a4] font-bold rounded-[4px] flex justify-center items-center py-1 px-2  text-center text-sm">{{cart.span5}}</span>
            </div> -->
        <div class="flex gap-x-5 mt-10 lg:mt-0">
          <span
            @click="filterCard(span)"
            v-for="(span, indexs) in cart.span"
            :key="indexs"
            class="bg-[#effafa] text-[#5ba4a4] font-bold rounded-[4px] flex justify-center items-center py-1 px-2 text-center text-sm"
            >{{ span }}</span
          >
        </div>
      </div>
    </section>
  </main>
</template>

<script>
export default {
  data() {
    return {
      cards: [
        {
          img: "/images/photosnap.svg",
          tittle: "Photosnap",
          p: "Senior Frontend Developer",
          span: ["Frontend", "Senior", "HTML", "CSS", "JavaScript"],
        },
        {
          img: "/images/manage.svg",
          tittle: "Manage",
          p: "Fullstack Developer",

          span: ["Fullstack", "Midweight", "Python", "React"],
        },
        {
          img: "/images/account.svg",
          tittle: "Account",
          p: "Junior Frontend Developer",
          span: ["Frontend", "Junior", "JavaScript", "React", "Sass"],
        },
        {
          img: "/images/myhome.svg",
          tittle: "MyHome",
          p: "Junior Frontend Developer",
          span: ["Frontend", "Junior", "CSS", "JavaScript"],
        },
        {
          img: "/images/loop-studios.svg",
          tittle: "Loop Studios",
          p: "Software Engineer",
          span: ["Fullstack", "Midweight", "JavaScript", "Ruby", "Sass"],
        },
        {
          img: "/images/faceit.svg",
          tittle: "FaceIt",
          p: "Junior Backend Developer",
          span: ["Backend", "Junior", "Ruby", "RoR"],
        },
        {
          img: "/images/shortly.svg",
          tittle: "Shortly",
          p: "Junior Developer",
          span: ["Frontend", "Junior", "HTML", "JavaScript", "Sass"],
        },
        {
          img: "/images/insure.svg",
          tittle: "Insure",
          p: "Junior Frontend Developer",
          span: ["Frontend", "Junior", "JavaScript", "Vue", "Sass"],
        },
        {
          img: "/images/eyecam-co.svg",
          tittle: "Eyecam Co.",
          p: "Full Stack Engineer",
          span: ["Fullstack", "Midweight", "JavaScript", "Python", "Django"],
        },
        {
          img: "/images/the-air-filter-company.svg",
          tittle: "The Air Filter Company",
          p: "Front-end Dev",
          span: ["Frontend", "Junior", "JavaScript", "React", "Sass"],
        },
      ],
      selectedFilter: [],
    };
  },
  computed: {
    filteredCards() {
      if (this.selectedFilter.length) {
        return this.cards.filter((item) =>
          item.span.some((word) => {
            if (this.selectedFilter.includes(word)) {
              return word;
            }
          })
        );
      } else {
        return this.cards;
      }
    },
  },
  methods: {
    filterCard(event) {
      
      if(!this.selectedFilter.includes(event)){
        this.selectedFilter.push(event);
      }
      
      
    },

    close(item){
        this.selectedFilter=this.selectedFilter.filter(word =>{
            if(word==item){
                return false
            }else{
                return true
            }
        })
        
    },

    clear(){
        this.selectedFilter=[]
    }
  },
};
</script>


<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
</style>