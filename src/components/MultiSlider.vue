<template>
  <div class="slider-container">
    <input
      type="range"
      :min="min"
      :max="max"
      :step="step"
      v-model="value"
      @input="emitChange"
    />
    <span>{{ value }}</span>
  </div>
</template>

<script>
export default {
  name: 'Slider',
  props: {
    min: {
      type: Number,
      default: 0,
    },
    max: {
      type: Number,
      default: 100,
    },
    step: {
      type: Number,
      default: 1,
    },
    value: {
      type: Number,
      default: 0,
    },
  },
  methods: {
    emitChange() {
      this.$emit('input', Number(this.value));
    },
  },
};
</script>

<style>
.slider-container {
  display: flex;
  align-items: center;
}

input[type='range'] {
  width: 100%;
  margin-right: 10px;
}

span {
  font-size: 14px;
}
</style>