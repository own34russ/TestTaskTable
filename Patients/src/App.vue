
<script setup>

import axios from 'axios';
import {ref,computed, onMounted} from 'vue'
import BaseTable from './components/Table/BaseTable.vue'
import TableRow from './components/Table/TableRow.vue';
import TableColumn from './components/Table/TableColumn.vue';
const tableHeads = ['Id', 'name', 'surname', 'patronymic', 'ДАТА РОЖДЕНИЯ','marital_status', 'ПОЛ', 'СНИЛС', 'reason_no_snils', 'ПОЛИС','author_id', 'date_first_reception','редактирование']
const tableSizeColumns = '1fr 1fr 1fr  1fr  1fr  1fr  1fr  1fr  1fr  1fr  1fr  1fr 1fr'
const sortField =ref('id')
const typeSort=ref('desc')
const APIurl ='http://localhost:3000/patients'
onMounted(async()=>{
    try{
const {data}= await axios.get(APIurl)
patients.value=data
    }
    catch (err) {
console.log(err)
    }
  })
  
const patients = ref([
  {
        id: "",
        name: "",
        surname: "",
        patronymic: null,
        patronymic: "",
        marital_status: null,
        gender: "",
        snils: null,
        reason_no_snils: "",
        series_number_policy: "",
        author_id: "",
        date_first_reception: ""
  },

])
// const addPatient(id,name,surname,patronymic patronymic marital_status gender snils reason_no_snils series_number_policy author_id )=>{

// }
const setSort=(name)=>{
  if (sortField.value === name){
    if(typeSort.value ==='asc'){
      typeSort.value ='desc'
    }else{
      typeSort.value ='asc'
    }
  }else{
    sortField.value = name
  }
}
const patientsSorting=computed(()=>{
  return patients.value.sort((a,b)=>{
    let modifier=1;
if(typeSort.value==='desc') modifier=-1
if(a[sortField.value]<b[sortField.value])return -1*modifier
if(a[sortField.value]<b[sortField.value])return 1*modifier
return 0

  })
})

</script>
<template>
  <h1 class="heading-1">
    Пациенты
  </h1>
  
  <base-table 
  :head="tableHeads"
  :columnTemplates="tableSizeColumns"
  @sorting="setSort">
  <table-row
  v-for="patient in patientsSorting" :key="patient.id " 

  :columnTemplates="tableSizeColumns"
  :bgRow="patient.bg">
  <table-column>
  {{ patient.id }}
</table-column><table-column>
  {{ patient.name }}
</table-column><table-column>
  {{ patient.surname }}
</table-column><table-column>
  {{ patient.patronymic }}
</table-column><table-column>
  {{ patient.birthday }}
</table-column><table-column>
  {{ patient.marital_status }}
</table-column><table-column>
  {{ patient.gender }}
</table-column><table-column>
  {{ patient.snils }}
</table-column><table-column>
  {{ patient.reason_no_snils }}
</table-column><table-column>
  {{ patient.series_number_policy }}
</table-column><table-column>
  {{ patient.author_id }}
</table-column><table-column>
  {{ patient.date_first_reception }}
</table-column>
<table-column>
  <button class="delete-patient">удалить</button>
  <button class="edit-patient" >редактировать</button></table-column>
</table-row>
    
  </base-table>
</template>
<style lang="scss">


#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

.content {
  max-width: 1400px;
  margin-left: 250px;
  padding: 30px;
  transition: 0.2s;
  &_full {
    margin-left: 0;
  }

}

.sidebar-toggle {
  position: fixed;
  left: 0;
  width: 15px;
  background: var(--primary);
  height: 100%;
  top: 62px;
  z-index: 1;
  cursor: pointer;
  color: #fff;
  display: flex;
  align-items: center;
  justify-content: center;
}

@media screen and (max-width: 1023px) {
  .content {
    margin-left: 0;
  }
}
</style>