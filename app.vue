<template>
  <div>
    <h1>{{ name }}</h1>
    <h2>{{ Title1 }}</h2>
    <ul>
      <li v-for="Project in Projects" :key="Project.name">
        <h2>{{ Project.name }}</h2>
        <p>{{ Project.description }}</p>
      </li>
    </ul>
    <h2>{{ Title2 }}</h2>
    <ul>
      <li v-for="Blog in Blogs" :key="Blog.Title">
        <h2>{{ Blog.Title }}</h2>
        <p>{{ Blog.Content }}</p>
        <p>{{ Blog.Date }}</p>
      </li>
    </ul>
  </div>
</template>

<script setup>
const name = "Lasitha Hasaranga";
const Title1 = "Projects";
// const Projects = [
//   {
//     name : 'L1 Project',
//     description : 'Object Identification Toy for Childeren',
//   },
//   {
//     name : 'L2 Project',
//     description : 'LMS System for Students in High School',
//   },
// ];
const {data:Projects, pending1, error1} = useFetch('http://localhost:5000/Projects');
const Title2 = "Blogs";
const {data:Blogs, pending2, error2} = useFetch('http://localhost:5000/blogs');
</script>

<style>
</style>