<!-- UploadButton.vue -->
<template>
    <div class="upload-wrapper">
      <label class="custom-upload">
        📁 Upload OBJ File
        <input type="file" accept=".obj" @change="onFileChange" hidden />
      </label>
      <span v-if="fileName" class="file-name">Selected: {{ fileName }}</span>
    </div>
  </template>
  
  <script setup>
  import { defineEmits } from 'vue';
  
  const emit = defineEmits(['file-selected']);
  
  function onFileChange(event) {
    const file = event.target.files[0];
    if (!file) return;
    emit('file-selected', file);
  }
  </script>
  
  <style scoped>
  .upload-wrapper {
    text-align: center;
    margin: 16px 0;
  }
  .custom-upload {
    display: inline-block;
    background-color: #db91ee;
    color: white;
    padding: 10px 20px;
    font-weight: bold;
    border-radius: 8px;
    cursor: pointer;
    transition: 0.3s;
  }
  .custom-upload:hover {
    background-color: #c031e4;
  }
  .file-name {
    margin-left: 10px;
    font-style: italic;
    color: #555;
  }
  </style>
  