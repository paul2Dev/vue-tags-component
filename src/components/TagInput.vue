<template>
  <div class="tag-input">
    <div
      v-for="(tag, index) in tags"
      :key="tag"
      class="tag-input__tag"
    >
      <span @click="removeTag(index)">x</span>
      {{ tag }}
    </div>
    <input 
      type="text"
      placeholder="enter tag name"
      class="tag-input__text"
      @keydown="addTag"
      @keydown.delete="removeLastTag"
    />
  </div>
</template>

<script setup>
import { ref } from 'vue'

const tags = ref(['tag1', 'tag2'])

function addTag(event) {
  if(event.code == 'Comma' || event.code == 'Enter') {
    event.preventDefault()
    let val = event.target.value.trim()
    if (val.length > 0) {
      tags.value.push(val)
      event.target.value = ''
    } 
  }
}

function removeTag(index) {
  tags.value.splice(index, 1)
}

function removeLastTag(event) {
  if(event.target.value.length === 0){
    removeTag(tags.value.length - 1)
  }
}

</script>



<style scoped>
.tag-input {
  width: 100%;
  border: 1px solid #34495E;
  font-size: 0.9em;
  height: 50px;
  box-sizing: border-box;
  padding: 0 10px;
}

.tag-input__tag {
  height: 30px;
  float: left;
  margin-right: 10px;
  background-color: #41B883;
  margin-top: 10px;
  line-height: 30px;
  padding: 0 5px;
  border-radius: 5px;
  color: #34495E;
}

.tag-input__tag > span {
  cursor: pointer;
  opacity: 0.75;
}

.tag-input__text {
  border: none;
  outline: none;
  font-size: 0.9em;
  line-height: 50px;
  background: none;
}
</style>
