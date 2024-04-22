<template>

<div class="container-fluid ">
    <div class="row justify-content-center align-items-center">
        <div class=" col-md-12 ">
            <h5 class="modal-title text-center my-3 fs-6">Añade aquí los datos del profesor:</h5>
        </div>
      <div class="col-md-6">
            <div class="container border rounded d-flex justify-content-center align-items-center"> 
                <form >
                    <div class="row">

                        <div class="col-md-12">
                        
                            <div class="mb-1 ">
                                <label for="inputName" class="form-label mt-2 mb-0">Nombre:</label>
                                <input type="text" class="form-control form-control-sm" 
                                    :class="{ 
                                    'is-valid': validName && teacher.teacherName.trim() !== '',
                                    'is-invalid': !validName || (teacher.teacherName.trim() === '' && teacher.teacherName.length > 0)
                                    }" 
                                    id="inputName" 
                                    aria-describedby="nameHelp" 
                                    placeholder="Ingrese aqui su nombre." 
                                    v-model="teacher.teacherName" 
                                    @input="validateName" 
                                    @keydown.enter.prevent="focusNextInput('inputSurname')" 
                                    pattern="^[^\s]+$">
                                    
                                <div class="text-danger" v-if="!validName">
                                     El campo solo acepta letras
                                </div>
                                <div class="text-danger" v-else-if="!validNameLength">
                                    Sabemos que no es tan largo tu nombre deje el invento!
                                </div>
                                <div class="text-danger" v-if="teacher.teacherName.trim() === '' && !/^\s*$/.test(teacher.teacherName)">
                                    Por favor ingrese un texto.
                                </div>
                            </div>
                        </div>

                        <div class="col-md-12 ">
                            <div class="mb-1 ">
                                <label for="inputSurname" class="form-label mb-0" >Apellido:</label>
                                <input type="text" class="form-control form-control-sm" 
                                :class="{ 
                                    'is-valid': validSurName && teacher.teacherSurName.length > 0,
                                    'is-invalid': !validSurName || (teacher.teacherSurName.trim() === '' && teacher.teacherSurName.length > 0)
                                 }" 
                                 id="inputSurname" 
                                 placeholder="Ingrese aqui su apellido." 
                                 v-model="teacher.teacherSurName" @input="validateSurName" 
                                 @keydown.enter.prevent="focusNextInput('inputRut')"
                                 pattern="^[^\s]+$">
                                <div class="text-danger" v-if="!validSurName">
                                     El campo solo acepta letras
                                </div>
                                <div class="text-danger" v-else-if="!validSurNameLength">
                                    Sabemos que no es tan largo tu Apellido deje el invento!
                                </div>
                            </div>
                        </div>

                        <div class="col-md-12">
                            <div class="mb-1">
                                <label for="inputRut" class="form-label mb-0">RUT:</label>
                                <input type="text" class="form-control form-control-sm" 
                                :class="{ 
                                    'is-valid': validRut && teacher.rut.length > 7, 
                                    'is-invalid': !validRut || (teacher.rut.length === 0 && !validRut)  
                                }" id="inputRut" placeholder="Ingrese aqui su RUT." 
                                v-model="teacher.rut" @input="validateRut" @keydown.enter.prevent="submitRut">
                                <div id="passwordHelpBlock" class="form-text">
                                    Por favor ingrese su Rut sin puntos ni guion.
                                </div>
                                <div class="text-danger" v-if="!validRut">
                                    Rut invalido.
                                </div>
                            </div>
                        </div>

                    <div class="col-md-12">
                        <div class="mb-1 ">
                            <label for="inputsubjects" class="form-label mb-0">Tecnologias:</label>
                            <div>
                                <div class="d-flex flex-wrap border rounded p-2">
                                    <div class="form-check" v-for="(technology, index) in technologies" :key="index">
                                    <input class="form-check-input " type="checkbox" :value="technology" v-model="teacher.subjects">
                                    <label class="form-check-label truncate me-2">{{ technology }}</label>
                                </div>
                                </div>
                                
                            </div>
                        </div>
                    </div>
                    </div>

                    <div class="row">
                        <div class="col-md-12 ms-2">
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
    <h5 class="modal-title text-center my-3 fs-6">Listado de profesores:</h5>
    <div class="container-md mb-5">
        <div class="row justify-content-center">
            <div class="col-md-10">
                <div class="table-responsive border rounded ">
                    <table class="table">
                        <thead>
                            <tr>
                                <th scope="col" class="small text-center">Nombre</th>
                                <th scope="col" class="small text-center">Apellidos</th>
                                <th scope="col" class="small text-center">RUT</th>
                                <th scope="col" class="small text-center">Materias</th>
                                <th scope="col" class="small text-center">Documentacion entregada</th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr v-for="elemento in teachers" :key="elemento.rut">
                                <td class="small text-center align-middle">{{ elemento.teacherName }}</td>
                                <td class="small text-center align-middle">{{ elemento.teacherSurName }}</td>
                                <td class="small text-center align-middle">{{ elemento.rut }}</td>
                                <td class="small">
                                    <ul>
                                        <li v-for="(item, index) in elemento.subjects" :key="index">{{ item }}</li>
                                    </ul>
                                </td>
                                <td class="small text-center align-middle">
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

    // let subject = ref('')

    let teacher = ref({
        teacherName: '',
        teacherSurName: '',
        rut: '',
        subjects: [],
        doc: false
    })
    
    const technologies = ref(['JavaScript','Dart', 'TypeScript', "PHP",  "MessiScript", "Python", "Java", "C++",  "Otros.."]);
    
        const focusNextInput = (nextInputId) => {
            // Enfocar el siguiente input cuando se presiona "Enter"
            document.getElementById(nextInputId).focus();
        };

        const submitRut = () => {
            // Desenfocar el input para eliminar el foco después de ingresar el valor
            document.activeElement.blur();
        };
    
    // validaciones
    const regexOnlyLetters = /^[a-zA-ZáéíóúÁÉÍÓÚ\s]*$/; 
    const regexRut = /^[0-9]{7,8}[0-9kK]$/
    const regexNumbers = /^[0-9]+[kK]?$/;
    
    let validName = ref(true);
    let validNameLength = ref(true);
    const validateName = () => {
        const name = teacher.value.teacherName;
        validName.value = regexOnlyLetters.test(name);
        validNameLength.value = validName.value && teacher.value.teacherName.length <= 30;
    };

    let validSurName = ref(true);
    let validSurNameLength = ref(true);
    const validateSurName = () => {
        validSurName.value = regexOnlyLetters.test(teacher.value.teacherSurName);
        validSurNameLength = validSurName.value && teacher.value.teacherSurName.length <= 30;
    };

    

    let validRut = ref(true);
    const validateRut = () => {
        if (teacher.value.rut.length < 9) {
        validRut.value = teacher.value.rut.length === 0 || regexNumbers.test(teacher.value.rut);
    }else if (teacher.value.rut.length === 9 || teacher.value.rut.length === 10) {
        validRut.value = regexRut.test(teacher.value.rut);
    }else if (teacher.value.rut.length > 10) {
        validRut.value = false; 
    }else {
        validRut.value = true; 
    }
    };

    //variables end

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
.overflow-auto {
    max-height: 50px; /* Define la altura máxima del select */
}

.truncate {
        max-width: 90px; /* Ancho máximo deseado para cada elemento */
        overflow: hidden;
        text-overflow: ellipsis; /* Truncar texto con puntos suspensivos si es demasiado largo */
        white-space: nowrap; /* Evitar que el texto se divida en múltiples líneas */
    }
</style>