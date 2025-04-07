<template>
    <header class="header-container">
      <h1 class="project-title">
        Automated Furniture Mesh Generation Platform based on MeshGPT
      </h1>
      <p class="project-description">
        This platform leverages advanced AI models to automate the generation of 3D furniture meshes from minimal input. It allows users to upload 3D models in OBJ format, visualize them directly in the browser, and interact with the mesh using rotation, scaling, and translation tools.
      </p>
    </header>
  </template>
  
  <script>
  export default {
    name: 'HeaderTitle'
  }
  </script>
  
  <style scoped>
  .header-container {
    text-align: center;
    color: #2c3e50;
    padding: 60px 20px 40px;
    background-color: #ffffff;
  }
  
  .project-title {
    font-size: 2.2rem;
    font-weight: bold;
    margin-bottom: 30px;
    line-height: 1.4;
  }
  
  .project-description {
    font-size: 1.1rem;
    max-width: 800px;
    margin: 0 auto;
    color: #333;
    line-height: 1.6;
  }
  </style>
  