<template>
  <div class="sellect-lang">

    <section class="mx-auto relative  w-40  ">
      <div class="langBar" @click="toggleLangItem">
        <div class="bg-blue-400 p-2 rounded-md flex items-center gap-2">
          <img :src="selectedFlag.img" alt="" class="object-cover rounded-md" style="width: 25px; height: 20px;">
        </div>
      </div>

      <div class="absolute langItem px-2 hidden   left-0  top-12 right-0 mt-2 flex flex-col gap-1 ">
        <div class="langItem" v-show="showLangItem">
          <div v-for="flag in data.flag" :key="flag.name" @click="changeLang(flag.name)"
            class="flex rounded-md p-2 bg-red-200 items-center gap-2">
            <img :src="flag.img" alt="" class="object-cover rounded-md" style="width: 25px; height: 20px;">
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
import { defineComponent } from 'vue'
import { useRouter } from 'vue-router'

export default defineComponent({
  data() {
    return {
      data: {
        active: "En",
        flag: [
          {
            name: "Ru",
            img: "https://wikiflag.ru/wp-content/uploads/2022/03/1.jpg",
          },
          {
            name: "En",
            img: "https://media.baamboozle.com/uploads/images/41367/1593085639_60643",
          },
          {
            name: "Uz",
            img: "https://i.pinimg.com/originals/31/59/7f/31597f5024d357ed5cbac66f4bd61d3b.png",
          },
        ],
      },
      showLangItem: false,
      selectedFlag: {},
    };
  },
  mounted() {
    this.selectedFlag = this.data.flag.find((flag) => flag.name === this.data.active);
  },
  methods: {
    toggleLangItem() {
      this.showLangItem = !this.showLangItem;
    },
    changeLang(name) {
      this.data.active = name;
      this.selectedFlag = this.data.flag.find((flag) => flag.name === name);
      this.showLangItem = false;
    },
  },
});
</script>