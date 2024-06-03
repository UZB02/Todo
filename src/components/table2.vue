<template>
    <header class="pl-14 pt-14">
        <button @click="addModal = !addModal" class="btn btn-primary">Add Student</button>
    </header>
    <div :class="addModal ? 'p-14 flex items-center absolute justify-center w-full z-50' : 'hidden'">
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
    <div class="pt-5 p-1">
        <!-- component -->
<table class="min-w-full border-collapse block md:table">
		<thead class="block md:table-header-group">
			<tr class="border border-grey-500 md:border-none block md:table-row absolute -top-full md:top-auto -left-full md:left-auto  md:relative ">
				<th class="bg-gray-600 p-2 text-white font-bold md:border md:border-grey-500 text-left block md:table-cell">ID</th>
				<th class="bg-gray-600 p-2 text-white font-bold md:border md:border-grey-500 text-left block md:table-cell">Name</th>
				<th class="bg-gray-600 p-2 text-white font-bold md:border md:border-grey-500 text-left block md:table-cell">Second Name</th>
				<th class="bg-gray-600 p-2 text-white font-bold md:border md:border-grey-500 text-left block md:table-cell">Actions</th>
			</tr>
		</thead>
		<tbody v-for="(item,index) in data" :key="index" class="block md:table-row-group">
			<tr class="bg-gray-300 border border-grey-500 md:border-none block md:table-row">
				<td class="p-2 w-[20px] md:border md:border-grey-500 text-left block md:table-cell"><span class="inline-block w-1/3 md:hidden font-bold">ID</span>{{ index +1  }}</td>
				<td class="p-2 md:border md:border-grey-500 text-left block md:table-cell"><span class="inline-block w-1/3 md:hidden font-bold">Name</span>{{ item.name }}</td>
				<td class="p-2 md:border md:border-grey-500 text-left block md:table-cell"><span class="inline-block w-1/3 md:hidden font-bold">Second Name</span>{{ item.secondName }}</td>
				<td class="p-2 md:border md:border-grey-500 text-left block md:table-cell">
					<span class="inline-block w-1/3 md:hidden font-bold">Actions</span>
					<button @click="EditModal(item.id)" class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-1 px-2 border border-blue-500 rounded">Edit</button>
					<button @click="Delete(item.id)" class="bg-red-500 hover:bg-red-700 text-white font-bold py-1 px-2 border border-red-500 rounded">Delete</button>
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