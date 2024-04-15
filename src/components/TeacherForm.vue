<template>
    <section>
        <h3>Añadir Profesor</h3>
        <div>
            <label>Nombre: <input type="text" placeholder="ingrese nombre" v-model="teacher.teacherName"></label>
        </div>
        <div>
            <label>Apellidos: <input type="text" placeholder="ingrese apellidos" v-model="teacher.teacherSurName"></label>
        </div>
        <div>
            <label >RUT/DNI: <input type="text" placeholder="ingrese DNI/Rut" v-model="teacher.rut"></label>
        </div>
        <div>
            <label >Materias: <input type="text" placeholder="ingrese materias" v-model="subject" @keyup.enter="handleSubject"></label>
            <button v-on:click="handleSubject()">Agregar</button>
        </div>
        <div><ul>
            <li v-for="(elemento, index) in teacher.subjects" v-bind:key="index">{{ elemento }}</li>
        </ul></div>
        <input type="checkbox" v-model="teacher.doc"> Documentacion entregada 
        <button v-on:click="handleAddTeacher()">Agregar </button>
    </section>

    <section>
        <h3>Listado de profesores</h3>
        <table>
            <tr>
                <th>Nombre</th>
                <th>Apellidos</th>
                <th>RUT</th>
                <th>Materias</th>
                <th>Documentacion entregada</th>
            </tr>
            <tr v-for="elemento in teachers" :key="elemento.rut">
                <th>{{ elemento.teacherName }}</th>
                <th>{{ elemento.teacherSurName }}</th>
                <th>{{elemento.rut  }}</th>
                <th>
                    <ul>
                        <li v-for="(item, index) in elemento.subjects" :key="index">{{ item }}</li>
                    </ul>
                </th>
                <th v-if="elemento.doc">Entregado</th>
                <th v-else>No entregado</th>
            </tr>
        </table>
    </section>
</template>

<script setup>
import { ref } from 'vue';
let teacher = ref({
    teacherName: '',
    teacherSurName: '',
    rut: '',
    subjects: [],
    doc: false
})
console.log(teacher)

let teachers = ref([])

let subject = ref('')

const handleSubject = () =>{
    teacher.value.subjects.push(subject.value)
    subject.value = ''
}

const handleAddTeacher = () =>{
   teachers.value.push(teacher.value)
   teacher.value.teacherName= ""
   teacher.value.teacherSurName= ""
   teacher.value.rut= ""
   teacher.value.subjects= []
   teacher.value.doc= false
}

</script>

<style scoped>
</style>