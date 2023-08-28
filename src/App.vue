<template>
  <div>
    <CheckBoxBlock @input="onUpdateCurrentItems" :items="array" />
    <div>
      <h2>Список выбранных элементов:</h2>
      <div v-for="item in selectedItems" :key="item.id">{{ item.title }}</div>
    </div>
  </div>
</template>
<script>
import CheckBoxBlock from "./components/CheckBoxBlock.vue";
export default {
  components: {
    CheckBoxBlock,
  },
  computed: {
    selectedItems() {
      return this.array.filter((item) => item.checked);
    },
  },
  data() {
    return {
      array: [
        { id: 1, title: "Apple", visible: true, disable: true, checked: false },
        { id: 2, title: "Melon", visible: false, checked: false },
        { id: 3, title: "Pineapple", visible: true, checked: false },
        { id: 4, title: "Berry", visible: true, checked: false },
      ],
      currentSelectionsArray: [],
    };
  },
  methods: {},
};
</script>
<style></style>
