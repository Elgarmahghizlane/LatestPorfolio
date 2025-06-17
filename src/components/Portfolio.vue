<template>
  <div>
    <div class="border-t border-gray-300 mb-8 w-[18rem] mx-auto"></div>
    <div
      class="my-8 m-12 text-base md:mx-auto font-semibold border-b-4 tracking-wide border-yellow-300 w-24"
    >
      My work
    </div>
    <div class="flex justify-center gap-4 md:gap-8 mx-8">
      <div
        v-for="type in filterTypes"
        :key="type"
        @click="filtered = type"
        :class="[
          'px-4 py-2 text-sm  uppercase rounded-md cursor-pointer',
          filtered === type
            ? 'bg-yellow-300 font-semibold '
            : 'bg-white text-black  hover:bg-gray-100',
        ]"
      >
        {{ type }}
      </div>
    </div>
    <div class="grid grid-cols-1 md:grid-cols-3 gap-4 px-4 my-8">
      <div
        v-for="(work, index) in filteredWorks"
        :key="index"
        class="lg-width mx-auto w-[90%] h-[15rem] text-center cursor-pointer"
        @click="showModal(index)"
      >
        <img
          :src="work.imageUrl"
          :alt="work.name"
          class=" h-full w-full border-grey-400 border-2 transform transition duration-300 ease-in-out hover:scale-105 hover:shadow-xl rounded-lg"
        />
      </div>
    </div>
    <div
      v-if="isModalOpen"
      class="fixed inset-0 flex items-center justify-center bg-black bg-opacity-50 z-50"
    >
      <div class="modal bg-white rounded-lg relative">
        <div
          @click="closeModal"
          class="absolute right-2 top-4 text-gray-400 cursor-pointer flex justify-end"
        >
          <span
            class="rounded-full hover:bg-slate-200 hover:rounded-full hover:px-2 px-2 py-1"
          >
            x
          </span>
        </div>
        <div
          class="flex items-center justify-between px-8 mx-4 mb-4 gap-4 h-full"
        >
          <div
            class="p-2 hover:bg-slate-200 hover:rounded-full px-2 mr-2 mt-2 cursor-pointer"
            @click="prevImage"
          >
            <svg
              fill="none"
              stroke="gray"
              stroke-width="1.5"
              viewBox="0 0 24 24"
              xmlns="http://www.w3.org/2000/svg"
              aria-hidden="true"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                d="M10.5 19.5L3 12m0 0l7.5-7.5M3 12h18"
              ></path>
            </svg>
          </div>
          <div class="Gallery">
            <div class="carousel p-4 flex justify-center">
              <img :src="getScreenshotUrl()" class="carousel-image h-auto" />
            </div>
          </div>

          <div
            class="p-2 hover:bg-slate-200 hover:rounded-full px-2 mr-2 mt-2 cursor-pointer"
            @click="nextImage"
          >
            <svg
              fill="none"
              stroke="gray"
              stroke-width="1.5"
              viewBox="0 0 24 24"
              xmlns="http://www.w3.org/2000/svg"
              aria-hidden="true"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                d="M13.5 4.5L21 12m0 0l-7.5 7.5M21 12H3"
              ></path>
            </svg>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import { ref } from "vue";
import madaris from "../assets/img/Madaris.png";
import codingart from "../assets/img/Codingart.png";
import daba from "../assets/img/Daba.png";
import storeino from "../assets/img/Storeino.png";
import POS from "../assets/img/POS.png";
// Madaris
import accueil from "../assets/img/Madaris/accueil.png";
import elle from "../assets/img/Madaris/elle.png";
import form from "../assets/img/Madaris/form.png";
import maps from "../assets/img/Madaris/maps.png";
import lui from "../assets/img/Madaris/lui.png";
import msg from "../assets/img/Madaris/msg.png";
import wtsp from "../assets/img/Madaris/wtsp.png";
// daba
import home from "../assets/img/daba/home.png";
import admin from "../assets/img/daba/admin.png";
import adminSec from "../assets/img/daba/admin2.png";
import contact from "../assets/img/daba/contact.png";
import about from "../assets/img/daba/about.png";
import add from "../assets/img/daba/add.png";
import adminAdd from "../assets/img/daba/adminAdd.png";
import inbox from "../assets/img/daba/inbox.png";
import header from "../assets/img/daba/header.png";
import single from "../assets/img/daba/single.png";
import prod from "../assets/img/daba/prod.png";
// storeino
import homeS from "../assets/img/storeino/home.png";
import singleProd from "../assets/img/storeino/singleProd.jpg";
import singleProdS from "../assets/img/storeino/singleProdS.jpg";
import wishlist from "../assets/img/storeino/wishlist.jpg";
import addWishlist from "../assets/img/storeino/addWishlist.png";
import card from "../assets/img/storeino/card.jpg";
import cat from "../assets/img/storeino/categ.jpg";
import formS from "../assets/img/storeino/formS.jpg";
// etours
import landing from "../assets/img/etours/landingPage.png";
import acc from "../assets/img/etours/acc.png";
import bed from "../assets/img/etours/bed.png";
import bedInv from "../assets/img/etours/bedInv.png";
import bedInvCal from "../assets/img/etours/benInvCal.png";
import property from "../assets/img/etours/property.png";
import reserv from "../assets/img/etours/reserv.png";
import exp from "../assets/img/etours/exp.png";
import plan from "../assets/img/etours/plan.png";
import cutoff from "../assets/img/etours/cutOff.png";
// pos
import pos from "../assets/img/pos/pos.png";
import HomePos from "../assets/img/pos/HomePos.png";
import caisse from "../assets/img/pos/caisse.png";
import table from "../assets/img/pos/table.png";
import serveur from "../assets/img/pos/serveur.png";
import tickets from "../assets/img/pos/tickets.png";
import singleT from "../assets/img/pos/singleT.png";
import addClient from "../assets/img/pos/addClient.png";
//SMMA
import smma from "../assets/img/smma.png";
import smmaFlyer from "../assets/img/smmaFlyer.png";
//WeekEnd
import weekEnd from "../assets/img/WeekEnd.jpeg";
import weekendCover from "../assets/img/weekendCover.png";
//vsnTrajets
import Intro2 from "../assets/img/vsnTrajets/Intro2.png";
import vsnTrajets from "../assets/img/vsnTrajets/Intro1.png";
import Logo from "../assets/img/vsnTrajets/Logo.png";
import TrajetsPage1 from "../assets/img/vsnTrajets/TrajetsPage1.png";
import TrajetsPage2 from "../assets/img/vsnTrajets/TrajetsPage2.png";
import TrajetsPage3 from "../assets/img/vsnTrajets/TrajetsPage3.png";
import TrajetsPage4 from "../assets/img/vsnTrajets/TrajetsPage4.png";
import TrajetsPage5 from "../assets/img/vsnTrajets/TrajetsPage5.png";
import TrajetsPage6 from "../assets/img/vsnTrajets/TrajetsPage6.png";
import TrajetsPage7 from "../assets/img/vsnTrajets/TrajetsPage7.png";
import TrajetsPage8 from "../assets/img/vsnTrajets/TrajetsPage8.png";
import TrajetsPage9 from "../assets/img/vsnTrajets/TrajetsPage9.png";
import TrajetsPage10 from "../assets/img/vsnTrajets/TrajetsPage10.png";
import TrajetsPage11 from "../assets/img/vsnTrajets/TrajetsPage11.png";
import TrajetsPage12 from "../assets/img/vsnTrajets/TrajetsPage12.png";
import TrajetsPage13 from "../assets/img/vsnTrajets/TrajetsPage13.png";
import TrajetsPage14 from "../assets/img/vsnTrajets/TrajetsPage14.png";
//travelApp
import banner from"../assets/img/travelApp/banner.png"
import welcomePage from"../assets/img/travelApp/welcomePage.png"
import login from"../assets/img/travelApp/login.png"
import home1 from"../assets/img/travelApp/home1.png"
import page3 from"../assets/img/travelApp/page3.png"
import page4 from"../assets/img/travelApp/page4.png"
import page5 from"../assets/img/travelApp/page5.png"

export default {
  data() {
    return {
      isModalOpen: false,
      currentIndex: 0,
      currentScreenshotIndex: 0,
      myworks: ref([
        {
          name: "WeekEnd",
          imageUrl: weekendCover,
          madarisScreenshot: [{ imageUrl: weekEnd }],
        },
        {
          name: "Madaris",
          imageUrl: madaris,
          madarisScreenshot: [
            { imageUrl: accueil },
            { imageUrl: lui },
            { imageUrl: elle },
            { imageUrl: maps },
            { imageUrl: form },
            { imageUrl: msg },
            { imageUrl: wtsp },
          ],
        },
        {
          name: "Codingart",
          imageUrl: codingart,
          madarisScreenshot: [
            { imageUrl: landing },
            { imageUrl: acc },
            { imageUrl: bed },
            { imageUrl: bedInv },
            { imageUrl: bedInvCal },
            { imageUrl: property },
            { imageUrl: reserv },
            { imageUrl: exp },
            { imageUrl: plan },
            { imageUrl: cutoff },
          ],
        },
        {
          name: "Daba",
          imageUrl: daba,
          madarisScreenshot: [
            { imageUrl: home },
            { imageUrl: header },
            { imageUrl: prod },
            { imageUrl: single },
            { imageUrl: add },
            { imageUrl: about },
            { imageUrl: contact },
            { imageUrl: admin },
            { imageUrl: adminSec },
            { imageUrl: inbox },
            { imageUrl: adminAdd },
          ],
        },
        {
          name: "vsnTrajets",
          imageUrl: Logo,
          madarisScreenshot: [
            { imageUrl: vsnTrajets },
            { imageUrl: Intro2 },
            { imageUrl: TrajetsPage1 },
            { imageUrl: TrajetsPage2 },
            { imageUrl: TrajetsPage3 },
            { imageUrl: TrajetsPage4 },
            { imageUrl: TrajetsPage5 },
            { imageUrl: TrajetsPage6 },
            { imageUrl: TrajetsPage7 },
            { imageUrl: TrajetsPage8 },
            { imageUrl: TrajetsPage9 },
            { imageUrl: TrajetsPage10 },
            { imageUrl: TrajetsPage11 },
            { imageUrl: TrajetsPage12 },
            { imageUrl: TrajetsPage13 },
            { imageUrl: TrajetsPage14 },
          ],
        },
        {
          name: "Storeino",
          imageUrl: storeino,
          madarisScreenshot: [
            { imageUrl: homeS },
            { imageUrl: singleProd },
            { imageUrl: singleProdS },
            { imageUrl: addWishlist },
            { imageUrl: wishlist },
            { imageUrl: card },
            { imageUrl: cat },
            { imageUrl: formS },
          ],
        },
        {
          name: "travelApp",
          imageUrl: banner,
          madarisScreenshot: [
            { imageUrl: welcomePage },
            { imageUrl: home1 },
            { imageUrl: login },
            { imageUrl: page3 },
            { imageUrl: page4 },
            { imageUrl: page5 },
           
          ],
        },
        {
          name: "POS",
          imageUrl: POS,
          madarisScreenshot: [
            { imageUrl: pos },
            { imageUrl: HomePos },
            { imageUrl: caisse },
            { imageUrl: table },
            { imageUrl: serveur },
            { imageUrl: tickets },
            { imageUrl: singleT },
            { imageUrl: addClient },
          ],
        },
        {
          name: "SMMA",
          imageUrl: smmaFlyer,
          madarisScreenshot: [{ imageUrl: smma }],
        },
      ]),
      filtered: "All",
      // const filtered = ref('All')
      filterTypes: ["All", "Frontend", "Fullstack", "UI/UX"],
    };
  },
  computed: {
    filteredWorks() {
      if (this.filtered === "Fullstack") {
        return this.myworks.filter((work) =>
          ["Madaris", "Daba"].includes(work.name)
        );
      } else if (this.filtered === "Frontend") {
        return this.myworks.filter(
          (work) => !["Madaris", "Daba"].includes(work.name)
        );
      } else if (this.filtered === "UI/UX") {
        return this.myworks.filter(
          (work) => ["vsnTrajets","Daba","Madaris", "travelApp"].includes(work.name)
        );
      } else {
        return this.myworks;
      }
    },
  },
  methods: {
    showModal(index) {
      this.isModalOpen = true;
      this.currentIndex = index;
      this.currentScreenshotIndex = 0;
      window.addEventListener("keydown", this.handleKeyDown);
    },
    closeModal() {
      this.isModalOpen = false;
      window.removeEventListener("keydown", this.handleKeyDown);
    },
    getScreenshotUrl() {
      const work = this.myworks[this.currentIndex];
      return work.madarisScreenshot[this.currentScreenshotIndex].imageUrl;
    },

    getCurrentScreenshotName() {
      const work = this.myworks[this.currentIndex];
      return work.madarisScreenshot[this.currentScreenshotIndex].name;
    },

    prevImage() {
      const work = this.myworks[this.currentIndex];
      this.currentScreenshotIndex =
        (this.currentScreenshotIndex - 1 + work.madarisScreenshot.length) %
        work.madarisScreenshot.length;
    },

    nextImage() {
      const work = this.myworks[this.currentIndex];
      this.currentScreenshotIndex =
        (this.currentScreenshotIndex + 1) % work.madarisScreenshot.length;
    },
    handleKeyDown(event) {
      if (this.isModalOpen) {
        if (event.key === "ArrowLeft") {
          this.prevImage();
        } else if (event.key === "ArrowRight") {
          this.nextImage();
        }
      }
    },
  },
};
</script>
<style scoped>
/* .portfolio {
        width: 70rem;
        margin-left: auto;
        margin-right: auto;
    } */

/* .carousel-image {
    max-height: 500px;
} */
.carousel-image {
  /* max-height: 100%; */
  object-fit: contain;
}
.carousel {
  /* max-height: 100%; */
  overflow-y: auto; /* Scroll inside this if needed */
}

.modal {
  width: 80%;
  height: 90%;
  display: flex;
  flex-direction: column;
  overflow: hidden;
}
.Gallery {
  flex: 1;
  overflow-y: auto;
  max-height: 90%;
}

svg {
  width: 1rem;
  height: 1rem;
}
</style>
