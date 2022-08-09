<template>
  <div class="home">
    <h1>DropZone</h1>
    <!-- drop和change事件都是冒泡的 -->
    <DropZone @drop.prevent="(e) => drop(e)" @change="(e) => selectedFile(e)" />
    <span class="file-info">File: {{ dropzoneFile.name }}</span>
  </div>
</template>

<script>
// @ is an alias to /src
import DropZone from "@/components/DropZone.vue";
import { ref } from "vue";

export default {
  name: "Home",
  components: {
    DropZone,
  },
  setup() {
    let dropzoneFile = ref("");

    const drop = (e) => {
      console.log(e.dataTransfer);
      dropzoneFile.value = e.dataTransfer.files[0];
      console.log(window.URL.createObjectURL(e.dataTransfer.files[0]));
    };

    const selectedFile = (e) => {
      console.log(e);
      dropzoneFile.value = document.querySelector(".dropzoneFile").files[0];
    };

    return { dropzoneFile, drop, selectedFile };
  },
};
</script>

<style scoped>
.home {
  height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  background-color: #f1f1f1;
}
h1 {
  font-size: 40px;
  margin-bottom: 32px;
}

.file-info {
  margin-top: 32px;
}
</style>
