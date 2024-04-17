<template>
    <div class="container border rounded d-flex justify-content-center align-items-center">   
        <form>
            <div class="row">
                <div class="col-md-12">
                    <h5 class="modal-title text-center">Añade aqui los datos del profesor:</h5>
                </div>

                <div class="col-md-12">
                
                    <div class="mb-3 d-flex align-items-center">
                        <label for="inputName" class="form-label me-1">Nombre:</label>
                        <input type="text" class="form-control" id="inputName" aria-describedby="nameHelp" v-model="teacher.teacherName">
                    </div>
                
                    <div id="nameHelp" class="form-text">Aca podria agregar un texto informativo.</div> 
                </div>

                <div class="col-md-12">
                    <div class="mb-3 d-flex align-items-center">
                        <label for="inputSurname" class="form-label me-1" >Apellido:</label>
                        <input type="text" class="form-control" id="inputSurname" v-model="teacher.teacherSurName">
                    </div>
                </div>

                <div class="col-md-12">
                    <div class="mb-3 d-flex align-items-center">
                        <label for="inputRut" class="form-label me-1">RUT:</label>
                        <input type="number" class="form-control" id="inputRut" v-model="teacher.rut">
                    </div>
                </div>

                <div class="col-md-12">
                    <div class="mb-3 d-flex align-items-center">
                        <label for="inputsubjects" class="form-label me-1">tecnologias:</label>
                        <input type="text" class="form-control" id="inputsubjects" v-model="subject" @keyup.enter="handleSubject()">
                        <button type="button" class="btn btn-primary ms-1" v-on:click="handleSubject()">Agregar</button>
                    </div>
                </div>

                <div>
                    <ul>
                        <li v-for="(elemento, index) in teacher.subjects" v-bind:key="index">{{ elemento }}</li>
                    </ul>
                </div>

            </div>

            <div class="row">
                <div class="col-md-12">
                    <div class="mb-3 form-check d-flex align-items-center">
                        <input type="checkbox" class="form-check-input me-3" id="exampleCheck1" v-model="teacher.doc">
                        <label class="form-check-label" for="exampleCheck1">Documentacion entregada</label>
                    </div>
                </div>
                <div class="col-md-12">
                    <button type="button" class="btn btn-primary" v-on:click="handleAddTeacher()">Agregar</button>
                </div>
            </div>
        
        </form>
    </div>


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

    //Variables init
    let teachers = ref([])

    let subject = ref('')

    let teacher = ref({
        teacherName: '',
        teacherSurName: '',
        rut: '',
        subjects: [],
        doc: false
    })
    //variables end


    //Se cargan al listado las Materias.
    const handleSubject = () =>{
        teacher.value.subjects.push(subject.value)
        //Se limpia el input al pulsar el boton.
        subject.value = ''
    }

    //Se agregan los datos del profesor al listado.
    const handleAddTeacher = () =>{
    
        teachers.value.push({
            // IMPORTANTE agregamos un nuevo objeto (NO REACTIVO) y le asignamos los valores de nuestro elemento referenciado.
            teacherName: teacher.value.teacherName,
            teacherSurName:teacher.value.teacherSurName ,
            rut:teacher.value.rut ,
            subjects: teacher.value.subjects,
            doc: teacher.value.doc
        })
            //Se limpian los inputs del formulario al enviar la informacion
            teacher.value.teacherName= ""
            teacher.value.teacherSurName= ""
            teacher.value.rut= ""
            teacher.value.subjects= []
            teacher.value.doc= false
    }
</script>

<style scoped>
</style>