<template>
    <header class="pl-14 pt-14">
        <button @click="addModal = !addModal" class="btn btn-primary">Add Student</button>
    </header>
    <div :class="addModal ? 'p-14 flex items-center absolute justify-center w-full' : 'hidden'">
        <form @submit.prevent="addStudent()" class="bg-slate-300 flex flex-col gap-1 p-3 rounded-md">
            <span class="flex flex-col gap-1">
                <label for="name">Name</label>
                <input type="text" v-model="name" name="name" class="w-full p-2 rounded-lg" id="name">
            </span>
            <span>
                <label for="Second Name">Second Name</label>
                <input type="text" v-model="secondName" name="SecondName" class="w-full p-2 rounded-lg" id="Second Name">
            </span>
            <span class="flex gap-2">
                <button type="button" class="btn w-1/2 btn-primary" @click="addStudent()">Add</button>
                <button type="button" @click="Cancel()" class="btn w-1/2 btn-danger">Cancel</button>
            </span>
        </form>
    </div>
    <div>
        <table class="p-14 flex flex-col gap-3 items-center justify-center">
            <thead class="w-full shadow-lg rounded-md">
                <tr class=" p-1 rounded-sm w-full flex justify-between">
                    <th>ID</th>
                    <th>Name</th>
                    <th>Second Name</th>
                    <th>Actions</th>
                </tr>
            </thead>
            <tbody v-for="(item,index) in data" :key="index" :class="item==null ? 'hidden' : 'w-full shadow-lg rounded-md'">
                <tr class="p-1 rounded-sm w-full flex items-center justify-between gap-10">
                    <td>{{ index + 1 }}</td>
                    <td>{{ item.name }}</td>
                    <td>{{ item.secondName }}</td>
                    <td>
                        <span class="flex gap-2">
                            <button class="btn btn-primary" @click="EditModal(item.id)">Edit</button>
                            <button class="btn btn-danger" @click="Delete(item.id)">Delete</button>
                        </span>
                    </td>   
                </tr>
            </tbody>
        </table>
    </div>
       <div :class="editModal ? 'p-14 flex items-center absolute justify-center w-full' : 'hidden'">
        <form @submit.prevent="addStudent()" class="bg-slate-300 flex flex-col gap-1 p-3 rounded-md">
            <span class="flex flex-col gap-1">
                <label for="name">Name</label>
                <input type="text" v-model="editName" name="name" class="w-full p-2 rounded-lg" id="name">
            </span>
            <span>
                <label for="Second Name">Second Name</label>
                <input type="text" v-model="editSecondName" name="SecondName" class="w-full p-2 rounded-lg" id="Second Name">
            </span>
            <span class="flex gap-2">
                <button type="button" class="btn w-1/2 btn-primary" @click="Edit()">Add</button>
                <button type="button" @click="editModal=false" class="btn w-1/2 btn-danger">Cancel</button>
            </span>
        </form>
    </div>
</template>
<script setup>
import { ref,reactive } from 'vue';

const name=ref('')
const secondName=ref('')
const editModal=ref(false)
const studentId=ref()
const editName=ref('')
const editSecondName=ref('')

const data=localStorage.getItem('data') ? JSON.parse(localStorage.getItem('data')): []
const addStudent=()=>{
    if(name.value==='' || secondName.value===''){
        alert('Iltimos barcha maydonlarni to\'ldiring')
        return
    }else{
    data.push({
        id:data.length+1,
        name:name.value,
        secondName:secondName.value
    })
    localStorage.setItem('data',JSON.stringify(data))
    addModal.value=false
    console.log(name.value,secondName.value);
    }
}

// function fetchData(){
//     data.value=localStorage.getItem('data') ? JSON.parse(localStorage.getItem('data')): []
// }
// fetchData()

const Cancel=()=>{
    name.value=''
    secondName.value=''
    addModal.value=false
}

const Delete=(id)=>{
    console.log(id);
    data.splice(id-1,1)
    localStorage.setItem('data',JSON.stringify(data))
}
const EditModal=(id)=>{
    studentId.value=id
    editName.value=data[id-1].name
    editSecondName.value=data[id-1].secondName
    console.log(studentId.value);
    editModal.value=true
}

const Edit=()=>{
    console.log(studentId.value);
    editModal.value=true
    data[studentId.value-1].name=editName.value
    data[studentId.value-1].secondName=editSecondName.value
    console.log(name.value,secondName.value);
    localStorage.setItem('data',JSON.stringify(data))
}
const addModal=ref(false)
</script>
<style scoped>
    
</style>