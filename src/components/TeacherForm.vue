<template>

<div class="container-fluid ">
    <div class="row justify-content-center align-items-center">
        <div class=" col-md-12 ">
            <h5 class="modal-title text-center fs-6">Añade aquí los datos del profesor:</h5>
        </div>
      <div class="col-md-6">
            <div class="container border rounded d-flex justify-content-center align-items-center"> 
                <form >
                    <div class="row">

                        <div class="col-md-12">
                        
                            <div class="mb-1 ">
                                <label for="inputName" class="form-label ">Nombre:</label>
                                <input type="text" class="form-control form-control-sm" id="inputName" aria-describedby="nameHelp" v-model="teacher.teacherName">
                            </div>
                        </div>

                        <div class="col-md-12 ">
                            <div class="mb-1 ">
                                <label for="inputSurname" class="form-label" >Apellido:</label>
                                <input type="text" class="form-control form-control-sm" id="inputSurname" v-model="teacher.teacherSurName">
                            </div>
                        </div>

                        <div class="col-md-12">
                            <div class="mb-1">
                                <label for="inputRut" class="form-label ">RUT:</label>
                                <input type="number" class="form-control form-control-sm" id="inputRut" v-model="teacher.rut">
                            </div>
                        </div>

                        <div class="col-md-12 ">
                            <div class="mb-1 ">
                                <label for="inputsubjects" class="form-label">Tecnologias:</label>
                                <div class="d-flex align-items-center">
                                    <input type="text" class="form-control form-control-sm me-2" id="inputsubjects" v-model="subject" @keyup.enter="handleSubject()">
                                    <button type="button" class="btn btn-primary btn-sm" v-on:click="handleSubject()">Añadir</button>
                                </div>
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
                            <div class="mb-2 form-check d-flex align-items-center">
                                <input type="checkbox" class="form-check-input me-1" id="checkDoc" v-model="teacher.doc">
                                <label class="form-check-label" for="checkDoc">Documentacion entregada</label>
                            </div>
                        </div>
                        <div class="col-md-12 mb-2 ">
                            <button type="button" class="btn btn-primary btn-sm" v-on:click="handleAddTeacher()">Agregar</button>
                        </div>
                    </div>
                </form>
            </div>
        </div>
    </div>
</div>


<section>
    <h5 class="modal-title text-center mt-2 fs-6">Listado de profesores</h5>
    <div class="container-md">
        <div class="row justify-content-center">
            <div class="col-md-10">
                <div class="table-responsive border rounded ">
                    <table class="table">
                        <thead>
                            <tr>
                                <th scope="col" class="small">Nombre</th>
                                <th scope="col" class="small">Apellidos</th>
                                <th scope="col" class="small">RUT</th>
                                <th scope="col" class="small">Materias</th>
                                <th scope="col" class="small">Documentacion entregada</th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr v-for="elemento in teachers" :key="elemento.rut">
                                <td class="small">{{ elemento.teacherName }}</td>
                                <td class="small">{{ elemento.teacherSurName }}</td>
                                <td class="small">{{ elemento.rut }}</td>
                                <td class="small">
                                    <ul>
                                        <li v-for="(item, index) in elemento.subjects" :key="index">{{ item }}</li>
                                    </ul>
                                </td>
                                <td class="small">
                                    <span v-if="elemento.doc">✅</span>
                                    <span v-else>❌</span>
                                </td>
                            </tr>
                        </tbody>
                    </table>
                </div>
            </div>
        </div>
    </div>
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