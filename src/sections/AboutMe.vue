<script setup lang="ts">
import SectionTitle from "@/components/SectionTitle.vue";
import AboutMeContent from "@/components/AboutMeContent.vue";
import colors from "tailwindcss/colors.js";
</script>

<template>
  <section
    id="about-me"
    class="p-4 md:p-8 w-full lg:min-h-screen lg:mt-24 flex flex-col lg:flex-row lg:items-stretch"
  >
    <div class="my-12 lg:flex-1 lg:my-0">
      <div class="w-fit mx-auto px-2 py-10 lg:sticky lg:top-1/2">
        <SectionTitle
          primaryText="ABOUT"
          secondaryText="ME"
          :color="colors.sky[500]"
        />
      </div>
    </div>
    <div class="lg:flex-1">
      <div
        class="bg-gradient-to-tr from-transparent to-[#00a6f466] p-4 flex flex-col gap-2 text-center rounded-xl text-xl"
      >
        <p>
          &#128075; Hi, I am Nguyen Hong Phong, a Junior Frontend Developer. I've been
          working with <span class="text-sky-500">React</span> and
          <span class="text-sky-500">NextJS</span> for over
          <span class="text-sky-500">two years</span>, building beautiful and
          user-frendly web applications.
        </p>
        <p>
          &#128210; I am eager to learn new technologies and continuously improve my
          skills, aiming to become a Full-stack Developer in the future, with a
          current focus on mastering Node.js and database technologies
        </p>
      </div>
      <div class="mt-8">
        <p class="text-center text-3xl font-bold italic">EXPERIENCE</p>
        <AboutMeContent
          title="Intern Frontend Developer"
          :subTitle="['GEEK Up', '06/2022 - 08/2022']"
        >
          <ul class="list-disc ml-8 [&_>li]:not-first:mt-1">
            <li>
              Collaborated with fellow interns and coaches in an internship
              program to develop a web application using UmiJS and Ant Design.
            </li>
            <li>
              Responsible for building the UI and integrating with the backend
              API.
            </li>
          </ul>
        </AboutMeContent>
        <AboutMeContent
          title="ReactJS Developer"
          :subTitle="['TMA Solutions', '10/2022 - 12/2024']"
        >
          <ul class="list-disc ml-8 [&_>li]:not-first:mt-1">
            <li>
              Maintained a CRM web application (ReactJS, NodeJS) by
              investigating issues, fixing bugs, and implementing unit tests to
              ensure application stability and quality.
            </li>
            <li>
              Contributed to the development of several web applications using
              ReactJS and NextJS.
            </li>
          </ul>
        </AboutMeContent>
      </div>

      <div class="mt-8">
        <p class="text-center text-3xl font-bold italic">EDUCATION</p>
        <AboutMeContent
          title="Bachelor of Science in Information Technology"
          :subTitle="['University of Information Technology', '']"
        />
      </div>
    </div>
  </section>
</template>

<style scoped></style>
