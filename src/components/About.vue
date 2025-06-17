<template>
    <div class="md:grid md:grid-cols-2 ">
        <div class="flex justify-center m-12">
            <div class="egg p-2 mt-50 md:w-[390px] md:h-[340px] bg-[#fbdb7c] flex justify-center">
                <img :src="about" class="md:w-200 md:h-80 mx-auto" alt="">
            </div>
        </div>
        <div class="md:m-4 m-12 flex flex-col justify-start gap-4 md:mt-12">
            <h1 class="md:mt-16 text-base  font-semibold border-b-4 border-yellow-300 w-24"> About me</h1>
            <div class="text-lg font-semibold ">
                I am Front-end Web Developer <br> And Creative UI/UX Designer
            </div>
            <p class="text-gray-400">I'm based in Agadir,Morocco.<br>I am dynamic, motivated and passionate about my job, I
                ambition to feed my curiosity and to develop my efficiency work in group.</p>
            <div @click="downloadFile"
                class="my-4 p-2 bg-yellow-300 text-center rounded-lg float-left md:w-[14rem] w-[12rem] shadow-md uppercase font-bold cursor-pointer md:text-sm text-xs ">
                Download Resume
            </div>
        </div>
    </div>
</template>
<script  >
import about from '../assets/img/about.png';
import pdf from '../assets/GhizlaneELGARMAH2025.pdf';
export default {
    data() {
        return {
            about: about,
            pdf:pdf
        }
    },
    methods: {
        downloadFile() {
            const link = document.createElement('a');
            link.href = this.pdf; 
            link.setAttribute('download', 'GhizlaneELGARMAH-Cv.pdf'); 
            document.body.appendChild(link);
            link.click();
        }
    }
}
</script>
<style>
.egg {
    border-radius: 50% 50% 50% 50% / 60% 60% 40% 40%;
}
</style>