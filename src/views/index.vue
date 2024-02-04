<template>
  <main>
    <header class="lg:w-full h-36 bg-[url('/images/bg-header-desktop.svg')]">
      <!-- <img src="" alt="" > -->
    </header>

    <!-- ///////////////////////////////////////////////////////////// -->
 
    <section
      class="w-full border flex flex-col gap-y-10 lg:gap-y-0 items-center bg-[#effafa] h-auto relative"
    >
      <div
        class="absolute top-[-120px] left-[65px] lg:top-[-35px] lg:left-[190px] lg:w-full flex"
      >
        <div
          class="flex flex-col gap-y-3 lg:flex-row justify-between items-center w-[90%] lg:w-[80%] lg:h-16 border bg-[#fff] rounded-[15px] px-5"
        >
          <!-- ///////////input/// -->
          <div>
            <input
              class="flex items-center lg:gap-5 w-full h-full placeholder:text-center placeholder:font-bold placeholder:text-xl border-none"
              type="text"
              placeholder="serch"
              v-model="inputSerch"
            />
          </div>
             <TransitionGroup name="list" tag="ul">
   
    </TransitionGroup>

          <!-- ////////////////// -->
          <div class="flex gap-x-5">
              <TransitionGroup name="slide" tag="div">
            <div
              class="w-5/6 justify-center items-center grid grid-cols-2 lg:grid-cols-3 gap-3"
            >
                <span
                  class="h-5 w-22 pl-2 bg-[#effafa] text-[#5ba4a4] flex justify-between text-sm items-center lg:gap-x-3 rounded-[10px]"
                  v-for="(item, index) in selectedFilter"
                  :key="index"
                  >{{ item }}
                  <svg
                    xmlns="http://www.w3.org/2000/svg"
                    fill="none"
                    viewBox="0 0 24 24"
                    stroke-width="1.5"
                    stroke="currentColor"
                    class="w-5 h-4 text-white bg-[#5ba4a4] cursor-pointer"
                    @click="close(item)"
                  >
                    <path
                      stroke-linecap="round"
                      stroke-linejoin="round"
                      d="M6 18 18 6M6 6l12 12"
                    />
                  </svg>
                </span>
            </div>
              </TransitionGroup>

            <!-- //////////////// -->
            <div class="w-1/6 p-5 lg:px-10">
              <span
                class="text-gray-500 font-bold text-sm lg:text-xl cursor-pointer"
                @click="clear"
                >clear</span
              >
            </div>
          </div>
          <!-- ///////////// -->
        </div>
      </div>
      <div
        class="lg:w-[80%] w-[90%] lg:h-40 h-auto mt-10 bg-white lg:flex items-center lg:justify-between rounded-[5px] px-5 border-l-4 border-[#5ba4a4]"
        v-for="(cart, index) in serchFilterItem"
        :key="index"
      >
        <!-- ///////////////////////////////// -->
        <section class="lg:flex gap-x-5 mt-10 lg:mt-0 h-auto relative">
          <img
            :src="cart.img"
            alt=""
            class="lg:w-28 lg:h-28 absolute top-[-85px] left-[10px] lg:relative lg:top-0 lg:left-0"
          />
          <div class="flex flex-col gap-y-3 pt-5 lg:pt-0">
            <div class="flex gap-x-3">
              <h2 class="font-bold text-2xl text-[#5ba4a4]">
                {{ cart.tittle }}
              </h2>
              <span
                class="bg-[#5ba4a4] flex justify-center font-bold items-center p-2 text-sm rounded-[15px] text-[#fff]"
                v-if="cart.isNew"
                >NEW</span
              >
              <span
                class="bg-black text-[#fff] font-bold flex justify-center items-center px-2 text-sm rounded-[16px]"
                v-if="cart.isFetured"
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
        <div
          class="lg:flex grid grid-cols-3 gap-y-3 lg:flex-row gap-x-5 mt-10 lg:mt-0 py-4 relative"
        >
          <span
            class="absolute md:hidden top-[-30px] border w-full h-[1px]"
          ></span>
          <span
            @click="filterCard(span)"
            v-for="(span, indexs) in cart.span"
            :key="indexs"
            class="bg-[#effafa] text-[#5ba4a4] font-bold rounded-[4px] flex justify-center items-center py-1 px-2 text-center text-sm cursor-pointer hover:bg-[#10b981] hover:text-white"
            >{{ span }}</span
          >
        </div>
      </div>

      <!-- //////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////// -->

      <!-- //////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////// -->
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
          isNew: true,
          isFetured: true,
          span: ["Frontend", "Senior", "HTML", "CSS", "JavaScript"],
        },
        {
          img: "/images/manage.svg",
          tittle: "Manage",
          p: "Fullstack Developer",
          isNew: true,
          isFetured: true,
          span: ["Fullstack", "Midweight", "Python", "React"],
        },
        {
          img: "/images/account.svg",
          tittle: "Account",
          p: "Junior Frontend Developer",
          isNew: true,
          isFetured: false,
          span: ["Frontend", "Junior", "JavaScript", "React", "Sass"],
        },
        {
          img: "/images/myhome.svg",
          tittle: "MyHome",
          p: "Junior Frontend Developer",
          isNew: false,
          isFetured: false,
          span: ["Frontend", "Junior", "CSS", "JavaScript"],
        },
        {
          img: "/images/loop-studios.svg",
          tittle: "Loop Studios",
          p: "Software Engineer",
          isNew: false,
          isFetured: false,
          span: ["Fullstack", "Midweight", "JavaScript", "Ruby", "Sass"],
        },
        {
          img: "/images/faceit.svg",
          tittle: "FaceIt",
          p: "Junior Backend Developer",
          isNew: false,
          isFetured: false,
          span: ["Backend", "Junior", "Ruby", "RoR"],
        },
        {
          img: "/images/shortly.svg",
          tittle: "Shortly",
          p: "Junior Developer",
          isNew: false,
          isFetured: false,
          span: ["Frontend", "Junior", "HTML", "JavaScript", "Sass"],
        },
        {
          img: "/images/insure.svg",
          tittle: "Insure",
          p: "Junior Frontend Developer",
          isNew: false,
          isFetured: false,
          span: ["Frontend", "Junior", "JavaScript", "Vue", "Sass"],
        },
        {
          img: "/images/eyecam-co.svg",
          tittle: "Eyecam Co.",
          p: "Full Stack Engineer",
          isNew: false,
          isFetured: false,
          span: ["Fullstack", "Midweight", "JavaScript", "Python", "Django"],
        },
        {
          img: "/images/the-air-filter-company.svg",
          tittle: "The Air Filter Company",
          p: "Front-end Dev",
          isNew: false,
          isFetured: false,
          span: ["Frontend", "Junior", "JavaScript", "React", "Sass"],
        },
      ],
      selectedFilter: [],
      inputSerch: "",
      items: [{ num: 1 }, { num: 2 }],
    };
  },
  watch: {},
  computed: {
    filteredCards() {
      if (this.selectedFilter.length > 0) {
        return this.cards.filter(
          (item) =>
            this.selectedFilter.every((filter) => {
              if (item.span.includes(filter)) {
                return item;
              }
            })
          // item.span.some((word) => {
          //   if (this.selectedFilter.includes(word)) {
          //     return word;
          //   }
          // })
          // item.span.every((span)=>{
          //   if(this.selectedFilter.includes(span)){

          //     return span
          //   }
          // })
        );
      } else {
        return this.cards;
      }
    },

    serchFilterItem() {
      return this.filteredCards.filter((cart) => {
        if (
          cart.tittle
            .toLocaleLowerCase()
            .includes(this.inputSerch.toLocaleLowerCase())
        ) {
          return true;
        } else {
          return false;
        }
      });
    },
  },
  methods: {
    filterCard(event) {
      if (!this.selectedFilter.includes(event)) {
        this.selectedFilter.push(event);
      }
    },

    close(item) {
      this.selectedFilter = this.selectedFilter.filter((word) => {
        if (word == item) {
          return false;
        } else {
          return true;
        }
      });
    },

    clear() {
      this.selectedFilter = [];
    },
  },
};
</script>


<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
body,
main {
  overflow-x: hidden;
}

.slide-enter-from {
  opacity: 0;
  transform: translateX(-500px);
}
.slide-enter-to {
  opacity: 1;
  transform: translateX(0);
}
.slide-enter-active {
  transition: all 0.5s ease-in-out;
}
.slide-leave-from {
  opacity: 1;
  transform: translateX(0) translateX(0);
}
.slide-leave-to {
  opacity: 0;
  transform: translateX(500px) translateY(0);
}
.slide-leave-active {
  transition: all 0.5s ease-in-out;
  position: absolute;
}
.slide-move {
  transition: all 0.5s ease;
}

/* //////////////////////////////////////////////////////////////////// */

.list-enter-active,
.list-leave-active {
  transition: all 0.5s ease;
  
}
.list-enter-from,
.list-leave-to {
  opacity: 0;
  transform: translateX(30px);
}
</style>