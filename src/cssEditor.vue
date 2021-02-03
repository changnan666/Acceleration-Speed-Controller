<template>
  <div class="container" ref="container" />
</template>

<script>
import { onMounted, ref } from "vue";
import { editor } from "monaco-editor";

export default {
  setup() {
    const container = ref(null);

    onMounted(() => {
      editor.create(container.value, {
        value: "",
        language: "json",
        theme: "vs-dark",
        tabSize: 2,
        lineNumbers: false,
        suggest: true,
      });
    });

    return {
      container,
    };
  },
};
</script>

<style scoped>
.container {
  width: 100%;
  height: 300px;
}
</style>