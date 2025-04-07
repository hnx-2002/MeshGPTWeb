<template>
    <div class="viewer-container">
      <h2>Upload and View OBJ File</h2>
      <UploadButton @file-selected="onFileSelected" />
      <span v-if="selectedFileName" class="file-name">Selected: {{ selectedFileName }}</span>
      <div ref="threeCanvas" class="three-canvas"></div>
    </div>
  </template>
  
  <script>
  import * as THREE from 'three'
  import { OBJLoader } from 'three/examples/jsm/loaders/OBJLoader.js'
  import { OrbitControls } from 'three/examples/jsm/controls/OrbitControls.js'
  import UploadButton from './UploadButton.vue'
  
  export default {
    name: 'MeshViewer',
    components: {
      UploadButton
    },

    data() {
      return {
        selectedFileName: ''
      }
    },
    created() {
      this.scene = null
      this.camera = null
      this.renderer = null
      this.controls = null
      this.meshObject = null
    },
    methods: {
      onFileSelected(file) {
        if (file && file.name.endsWith('.obj')) {
          this.selectedFileName = file.name;

          const reader = new FileReader()
          reader.onload = (e) => {
            const contents = e.target.result
            const loader = new OBJLoader()
            const object = loader.parse(contents)

            const box = new THREE.Box3().setFromObject(object)
            const center = new THREE.Vector3()
            box.getCenter(center)
            object.position.sub(center)  // 将模型中心移到 (0, 0, 0)
            object.scale.set(100, 100, 100)

            // 清除旧模型
            if (this.meshObject) {
              this.scene.remove(this.meshObject)
            }

            this.meshObject = object
            this.scene.add(object)
          }
          reader.readAsText(file)
        } else {
          alert('Please upload a valid .obj file')
          this.selectedFileName = ''
        }
      },
      initThreeJS() {
        // 创建场景
        this.scene = new THREE.Scene()
        this.scene.background = new THREE.Color(0xf5f5f5)
  
        // 相机
        const width = this.$refs.threeCanvas.clientWidth
        const height = 500
        this.camera = new THREE.PerspectiveCamera(45, width / height, 0.1, 1000)
        this.camera.position.set(0, 0, 150)
  
        // 渲染器
        this.renderer = new THREE.WebGLRenderer({ antialias: true })
        this.renderer.setSize(width, height)
        this.$refs.threeCanvas.appendChild(this.renderer.domElement)
  
        // 轨道控制器
        this.controls = new OrbitControls(this.camera, this.renderer.domElement)

        // 主方向光，模拟太阳从前方照射
        const directionalLight = new THREE.DirectionalLight(0xffffff, 1)
        directionalLight.position.set(0, 0, 50).normalize()
        this.scene.add(directionalLight)

        // ✅ 环境光（解决背面漆黑问题）
        const ambientLight = new THREE.AmbientLight(0xffffff, 0.8) // 第二个参数是强度（0~1）
        this.scene.add(ambientLight)

        // （可选）后侧补光
        const backLight = new THREE.DirectionalLight(0xffffff, 0.7)
        backLight.position.set(0, 0, -50).normalize()
        this.scene.add(backLight)
  
        // 开始动画循环
        this.animate()
      },
      animate() {
        requestAnimationFrame(this.animate)
        if (this.controls) this.controls.update()
        this.renderer.render(this.scene, this.camera)
      }
    },
    mounted() {
      this.initThreeJS()
    }
  }
  </script>
  
<style scoped>

.viewer-container {
    width: 100%;        /* 跟着 page-container 走 */
    padding: 20px 0;
    text-align: center;
}

.three-canvas {
  width: 100%;        /* 占满父容器（即 page-container） */
  height: 500px;      /* 固定高度，不随窗口变化 */
  border: 1px solid #ccc;
  margin: 20px auto;
}





  /* .viewer-container {
    text-align: center;
    width: 90%;
    padding: 30px;
  }
  input[type="file"] {
    margin-bottom: 20px;
  }
  .three-canvas {
    width: 100%;
    height: 500px;
    border: 1px solid #ccc;
    margin: 0 auto;
  } */
</style>
  