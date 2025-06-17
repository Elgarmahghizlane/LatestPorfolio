<template>
    <div class="">
        <div class="md:grid md:grid-cols-2 bg-black p-4">
            <div class="font-bold" style="">
                <h1 class="text-[32px] text-gray-500 text-center">
                    Hello,
                </h1>
                <h1 class="text-white md:text-[32px] text-[28px] text-center ">
                    I'm Ghizlane EL GARMAH,
                </h1>
                <h1 class="text-center text-gray-500 text-[28px] ">
                    Web Developer
                </h1> <br />
                <div class="border border-yellow-300 text-yellow-300 p-2 w-[9rem] text-center mx-auto cursor-pointer">
                    <a :href="linkedinLink" >
                        HIRE ME 
                    </a>
                  
                </div>
            </div>
            <div class="bg-black ">
                <img :src="bannerImg" class="w-auto h-80 mx-auto" alt="">
            </div>
        </div>
        <div class="bg-black flex justify-center items-end" style="height:4rem; clip-path: polygon(50% 100%, 100% 38%, 100% 0, 0 0, 0% 38%);">
            <div class="md:w-10 w-8 ">
                <svg fill="none" stroke="white" stroke-width="2" viewBox="0 0 24 24"
                    xmlns="http://www.w3.org/2000/svg" aria-hidden="true">
                    <path stroke-linecap="round" stroke-linejoin="round"
                        d="M19.5 5.25l-7.5 7.5-7.5-7.5m15 6l-7.5 7.5-7.5-7.5"></path>
                </svg>
            </div>
        </div>
    </div>
</template>

<script>
import banner from '../assets/img/banner.png';
export default {
    data() {
        return {
            bannerImg: banner
        }
    },
    computed:{
        linkedinLink() {
            return 'https://www.linkedin.com/in/ghizlane-el-garmah-b357421b6';
        },
    }

}
</script>
<style></style>