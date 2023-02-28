<script>
// give each todo a unique id
let id = 0

export default {
  data() {
    return {
      newSelected: '',
      selects: [
        { id: id++, text: 'Height: 20, Width: 10' },
        { id: id++, text: 'Height: 5, Width: 5' },
      ]
    }
  },
  methods: {
    addSelected() {
      this.selects.push({ id: id++, text: this.newSelected })
      this.newSelected = ''
    },
    removeSelected(selected) {
      this.selects = this.selects.filter((t) => t !== select)
    }
  }
}
</script>

<template>
  <form @submit.prevent="addselected">
    <input v-model="newselected">
    <button>Add Selected</button>    
  </form>
  <ul>
    <li v-for="select in selected" :key="selected.id">
      {{ todo.text }}
      <button @click="removeSelected(select)">X</button>
    </li>
  </ul>
</template>