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
  <div>
    <h1>Create a New Project</h1>
    <form @submit.prevent="createProject">
      <table>
        <tr>
          <td><label for="name">Project Name:</label></td>
          <td><input type="text" v-model="newProject.name" id="name" required></td>
        </tr>
        <tr>
          <td><label for="description">Project Description:</label></td>
          <td><textarea id="description" v-model="newProject.description" required></textarea></td>
        </tr>
        <tr>
          <td></td>
          <td><button type="submit">Create Project</button></td>
        </tr>
      </table>
    </form>
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

const newProject = ref({
  name: '', 
  description: '',
});

const createProject = async () => {
  console.log(newProject.value);

  try{
    const response = await fetch('http://localhost:5000/Projects', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
      },
      body: JSON.stringify(newProject.value),
    });

    if(!response.ok){
      throw new Error('Failed to create a new project');
    }

    const result = await response.json();
    Projects.value.push(result);//Add new project to the list

    //clear the form
    newProject.value.name = '';
    newProject.value.description = '';
  }catch(error){
    console.error(error);
  }
};
</script>

<style>
</style>