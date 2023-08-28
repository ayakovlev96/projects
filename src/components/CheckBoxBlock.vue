<template>
  <div>
    <h1>Блок выбора:</h1>
    <div style="margin-bottom: 12px; display: flex; align-items: center">
      Отображать в виде RadioButtons
      <input type="checkbox" :id="visionType" v-model="visionType" />
    </div>
    <div v-show="!visionType" class="checkBoxBlock">
      <ul class="list">
        <li v-for="item in currentItems" :key="item.id" class="list-item">
          <input
            v-model="item.checked"
            class="custom-checkbox"
            type="checkbox"
            :id="item.id"
            :disabled="item.disable"
          />
          <label :for="item.id"> </label>
          <label class="custom-lable">{{ item.title }}</label>
        </li>
      </ul>
    </div>

    <div v-show="visionType" class="checkBoxBlock">
      <ul class="list">
        <li v-for="item in currentItems" :key="item.id" class="list-item">
          <label class="switch">
            <input
              v-model="item.checked"
              :disabled="item.disable"
              :name="`slider_${item.id}`"
              class="custom-slider"
              :id="`slider_${item.id}`"
              type="checkbox"
            />
            <label class="slider" :for="`slider_${item.id}`"> </label>
          </label>
          <label :class="['custom-lable', { checked: item.checked }]">{{
            item.title
          }}</label>
        </li>
      </ul>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    items: {
      type: Array,
      default: () => [],
    },
  },
  data() {
    return {
      currentItems: this.items,
      visionType: false,
    };
  },
  //   watch: {
  //     currentItems() {
  //       this.content = this.value;
  //     },
  //   },
  methods: {
  },
};
</script>
<style>
.checkBoxBlock {
  padding: 20px;
  border-width: thick;
  border: 1px dashed #4ab4ff;
  border-radius: 10%;
  display: inline-block;
  background-color: rgb(0 0 0 / 75%);
}
.list {
  margin: 0px;
  padding: 0px;
  list-style: none;
  display: grid;
  grid-template-rows: repeat(4, 24px);
  gap: 6px;
  grid-auto-flow: column;
}
.list-item {
  display: inline-flex;
  align-items: center;
  gap: 6px;
}
.custom-checkbox {
  position: absolute;
  z-index: -1;
  opacity: 0;
}
.custom-checkbox + label {
  display: inline-flex;
  align-items: center;
  user-select: none;
}
.custom-checkbox + label::before {
  content: "";
  display: inline-block;
  width: 20px;
  height: 20px;
  border-radius: 4px;
  border: 1px solid var(--primary-primary-400, #303f5f);
  background: var(--primary-primary-900, #0e121b);
  background-color: #151b29;
  background-repeat: no-repeat;
  background-position: center center;
  background-size: 50% 50%;
}
.custom-checkbox:checked + label::before {
  background-image: url("~@/assets/images/svg/checked.svg");
}
.custom-checkbox[disabled] + label::before {
  background-image: url("~@/assets/images/svg/disabled_check.svg");
}
.custom-checkbox:not(:disabled) + label:hover::before {
  border-color: #4ab4ff;
}

.custom-lable {
  font-family: Gotham Pro;
  font-size: 12px;
  font-style: normal;
  font-weight: 400;
  line-height: 16px;
  letter-spacing: 0.396px;
  color: #92a4c8;
  &.checked {
    color: #ffffff;
  }
}
.custom-checkbox:checked ~ .custom-lable {
  color: #ffffff;
}

.switch {
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 48px;
  height: 24px;
}

.custom-slider {
  display: none;
}

.slider {
  position: absolute;
  cursor: pointer;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: #151b29;
  border: 1px solid #303f5f;
  border-radius: 4px;
  -webkit-transition: 0.4s;
  transition: 0.4s;
}
.slider:before {
  position: absolute;
  content: "";
  bottom: 1px;
  left: 1px;
  height: 20px;
  width: 20px;
  background-color: #92a4c8;
  border-radius: 10%;
  -webkit-transition: 0.4s;
  transition: 0.4s;
}

.custom-slider:checked + .slider:before {
      background-color: #4AB4FF;
}
.custom-slider:checked + .slider:before {
  -webkit-transform: translateX(24px);
  -ms-transform: translateX(24px);
  transform: translateX(24px);
}
.custom-slider-disable {
  background-color: #212b41;
}
.custom-slider:disabled + .slider {
  background-color: #212b41;
}
.custom-slider:disabled + .slider:before {
  background-color: #3e517a;
}
.custom-slider:hover + .slider {
  border-color: #4AB4FF;
}
</style>
