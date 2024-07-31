<script setup>
import { onMounted, ref, watch } from 'vue'
let names = ref()
let filterd = ref()

onMounted(() => {
    const storedNames = localStorage.getItem('Names')
    names.value = JSON.parse(storedNames)
    filterd.value = JSON.parse(storedNames)

})
let search = ref("")

watch(search, (newSearch, oldSearch) => {
    if (newSearch) {
        newSearch = newSearch.trim()
        filterd.value = names.value.filter(item => item.name.toLowerCase().search(newSearch.toLowerCase()) !== -1)
    } else {
        filterd.value = names.value;
    }
})

const filterdName = (name) => {
    let  fundedIndex= name.toLowerCase().search(search.value.toLowerCase());
    if(fundedIndex !== -1) {
        let first = name.slice(0,fundedIndex);
        let second = name.slice(fundedIndex, fundedIndex + search.value.length);
        let third = name.slice(fundedIndex + search.value.length , name.length);

        return first +'<b>' + second + '</b>' + third;
    }else {
        return name;
    }
}
const DeleteName = (id) => {
    names.value = names.value.filter(item => item.id !== id)
}

</script>

<template>
    <section>
        <h1>Names</h1>
        <div>
            <label>Search</label>
            <input type="text" v-model="search">
        </div>
        <div class="tbl-header">
            <table>
                <thead>
                <tr>
                    <th>Id</th>
                    <th>Name</th>
                    <th>Delete</th>
                </tr>
                </thead>
            </table>
        </div>
        <div class="tbl-content">
            <table>
                <tbody>
                <tr v-for="name in filterd">
                    <td>{{ name.id }}</td>
                    <td v-html="filterdName(name.name)"></td>
                    <td>
                        <button @click="DeleteName(name.id)" class="delete">Delete</button>
                    </td>
                </tr>
                </tbody>
            </table>
        </div>
    </section>
</template>

<style>
b{
    color: #F50057 !important;
}
h1 {
    font-size: 30px;
    color: #fff;
    text-transform: uppercase;
    font-weight: 300;
    text-align: center;
    margin-bottom: 15px;
}

table {
    width: 100%;
    table-layout: fixed;
}

.tbl-header {
    background-color: #a3a3a3;
}

.tbl-content {
    height: 300px;
    overflow-x: auto;
    margin-top: 0px;
    background-color: rgba(65, 65, 66, 0.51);
}

th {
    padding: 20px 15px;
    text-align: left;
    font-weight: 500;
    font-size: 12px;
    color: #fff;
    text-transform: uppercase;
}

td {
    padding: 15px;
    text-align: left;
    vertical-align: middle;
    font-weight: 300;
    font-size: 12px;
    color: #fff;
    border-bottom: solid 1px rgba(255, 255, 255, 0.1);
}

.made-with-love {
    margin-top: 40px;
    padding: 10px;
    clear: left;
    text-align: center;
    font-size: 10px;
    font-family: arial;
    color: #fff;
}

.made-with-love i {
    font-style: normal;
    color: #F50057;
    font-size: 14px;
    position: relative;
    top: 2px;
}

.made-with-love a {
    color: #fff;
    text-decoration: none;
}

.made-with-love a:hover {
    text-decoration: underline;
}

.delete {
    background-color: #F50057;
    padding: 16px;
    border-radius: 5px;
    border: none;
    color: white;
}

.delete:hover {
    cursor: pointer;
}
</style>