<template>
   <div 
   class="table-wrapper">
    <div 
    class="table">
       <div
       class="table-head"
        :style="{'grid-template-columns': columnTemplates}">
        <div 
        class="table-head__name" v-for="(element,i) of head" :key="i" @click="clickOnHead(element)" >
    {{ element }}
            </div>
            
       </div>
       <slot></slot>
     </div>
   </div>
   
</template>
<script setup>
const props=defineProps({
    head:{
        type:Array,
    required:false
},
columnTemplates:{
    type: String,
    required:false
}
},
)
const emit=defineEmits(['sorting'])
const clickOnHead=(name)=>{
emit('sorting',name.toLowerCase())
}
</script>
<style lang="scss" scoped>
.table {
  background-color: #aecbf1;
  width: 100%;
  margin-bottom: 40px;
  margin-top: 15px;
  &-wrapper {
    display: flex;
    justify-content: center;
  }
  &-head {
       padding: 5px 16px;
    display: grid;
    column-gap: 10px;
    align-items: center;
    border: 2px solid #01030f;
    background: #fff;
  
    &__name {
      display: flex;
      justify-content: flex-start;
      align-items: center;
      color: black;
      cursor: pointer;
   
  }}}
</style>