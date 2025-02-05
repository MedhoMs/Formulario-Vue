<script setup>
import { computed, ref } from 'vue'
import FormInput from './FormInput.vue';
import FormSelect from './FormSelect.vue';
import ButtonInput from './ButtonInput.vue';
import FormRadioInput from './FormRadioInput.vue';
import FormDatalist from './FormDatalist.vue';
import { useMouse } from '@vueuse/core';
import { useStepper } from '@vueuse/core'

const form = ref({
  name: "",
  surname: "",
  user: "",
  email: "",
  password: "",
  birthday: "",
  street: "",
  buildingType: "",
  doorNumber: "",
  postalCode: "",
  province: "",
  country: "",
  studyLevel: "",
  gender: false,
  subscribe: false,
  captcha: false,
  comment: "",
  button: ""
});

const resetForm = () => {
  form.value= {
    name: "",
    surname: "",
    user: "",
    email: "",
    password: "",
    birthday: "",
    street: "",
    buildingType: "",
    doorNumber: "",
    postalCode: "",
    province: "",
    country: "",
    studyLevel: "",
    gender: false,
    subscribe: false,
    captcha: false,
    comment: "",
    button: ""
  };
};

const { x, y } = useMouse()

const activeCheckbox = ref (false)

const currentSection = ref("personalInfo")


const captchaValidation = () => {
  const captchaNumber1 = ref(5);
  const captchaNumber2 = ref(3);

  const userSum = parseInt(prompt(`Tengo mis sospechas... ¿Cuánto es ${captchaNumber1.value} + ${captchaNumber2.value}?`));

  if (userSum === captchaNumber1.value + captchaNumber2.value) {
    form.value.captcha = true
  } else {
    form.value.captcha = false;
    alert("Validación fallida, vuelva a intentar.")
  }
    
}

const submitValidation = (event) => {
  if (!form.value.captcha) { 
    event.preventDefault(); 
    alert("Debes validar que no eres un robot antes de enviar el formulario.");
  }
};


const totalSteps = 1;
const currentStep = ref(0); 

const progress = computed(() => {
  return (currentStep.value / totalSteps) * 100;
});

const nextStep = () => {
  if (currentStep.value < totalSteps) {
    currentStep.value += 1;
    if (currentStep.value === 1) {
      currentSection.value = 'address';
    }
  }
};

const studyLevel = [
  {
    value: "",
    text: "Elige",
  },
  {
    value: "Primaria",
    text: "Primaria",
  },
  {
    value: "Secundaria",
    text: "Secundaria",
  },
  {
    value: "Bachiller",
    text: "Bachiller",
  },
  {
    value: "FP",
    text: "FP",
  },
  {
    value: "Universidad",
    text: "Universidad",
  },
  {
    value: "Sin Estudios",
    text: "Sin Estudios",
  },
]

const buildingType = [

  {
    value: "Piso",
  },
  {
    value: "Apartamento",
  },
  {
    value: "Casa",
  },
  {
    value: "Oficina",
  },
]
</script>

<template>
  <div class="grid place-items-center dark:text-white bg-gradient-to-b from-black via-[#2f005e] to-black my-7">
    <h1>Poscion del cursor: {{ x }}, {{ y }}</h1>
    <form @submit="submitValidation" autocomplete="off" class="rounded-xl text-center bg-black/35 backdrop-blur-xl p-10 place-items-center">
      <div v-if="currentSection === 'personalInfo'">
        <div class="grid gap-6 mb-6 md:grid-cols-2">
        <label for="name">
          <div class="font-bold">NOMBRE</div>
          <FormInput v-model="form.name" type="text" id="name" name="name" required></FormInput>
        </label>

        <label for="surname">
          <div class="font-bold">APELLIDOS</div>
          <FormInput v-model="form.surname" type="text" id="surname" name="surname" required></FormInput>
        </label>

        <label for="user">
          <div class="font-bold">USER</div>
          <FormInput v-model="form.user" type="text" id="user" name="user" required></FormInput>
        </label>

        <label for="mail">
          <div class="font-bold">EMAIL</div>
          <FormInput v-model="form.email" type="email" id="mail" name="mail" required></FormInput>
        </label>

        <label for="password">
          <div class="font-bold">CONTRASEÑA</div>
          <FormInput v-model="form.password" type="password" id="password" name="password" required></FormInput>
        </label>

        <label for="birthday">
          <div class="font-bold">FECHA DE NACIMIENTO</div>
          <FormInput v-model="form.birthday" type="date" id="birthday" name="birthday" class="w-full text-center"></FormInput>
        </label>

        
      </div>
        <ButtonInput :disabled = "!(form.name && form.surname && form.user && form.email && form.password)" @click="nextStep" class="rounded-xl w-full">Siguiente</ButtonInput>
        <br><br>
      </div>

      <div class="grid gap-6 mb-6 md:grid-cols-2" v-if="currentSection === 'address'">
        <label for="street">
          <div class="font-bold">CALLE</div>
          <FormInput v-model="form.street" type="text" id="street" name="street" required></FormInput>
        </label>

        <label for="building type">
          <div class="font-bold">TIPO DE EDIFICIO</div>
          <FormDatalist :options="buildingType" id="types"/>
          <FormInput list="types" id="building-type" name="building-type" required />
        </label>

        <label for="door-number">
          <div class="font-bold">Nº PUERTA</div>
          <FormInput v-model="form.doorNumber" type="number" id="door-number" name="door-number" required></FormInput>
        </label>

        <label for="postalcode">
          <div class="font-bold">CÓDIGO POSTAL</div>
          <FormInput v-model="form.postalCode" type="text" id="postalcode" name="postalcode" required></FormInput>
        </label>

        <label for="province">
          <div class="font-bold">PROVINCIA</div>
          <FormInput v-model="form.province" type="text" id="province" name="province" required></FormInput>
        </label>

        <label for="country">
          <div class="font-bold">PAÍS</div>
          <FormInput v-model="form.country" type="text" id="country" name="country" required></FormInput>
        </label>
      </div>

      <div class="w-full bg-gray-200 rounded-full h-2.5 dark:bg-gray-700">
        <div class="bg-blue-600 h-2.5 rounded-full" :style="{ width: progress + '%' }"></div>
      </div>

      <br>

      <div>
        <label for="study-level">
          <div class="font-bold">NIVEL DE ESTUDIO</div>
          <FormSelect v-model="form.studyLevel" id="study-level" name="study-level" class="text-center" :options="studyLevel"/>
        </label>
      </div>

      <br>

      <label>
      <div class="font-bold">
          <p>¿Le ha sido útil nuestro formulario? Háganoslo saber...</p>
      </div>
      <br>
      <textarea v-model="form.comment" id="comment" name="comment" placeholder="Escriba aquí..." class="bg-white/30 backdrop-blur-lg rounded-lg text-center w-full"></textarea>
      </label>

      <br><br>

      <div>
        <p class="font-bold">GÉNERO</p>
        <label><FormRadioInput v-model="form.gender" id="man" name="gender" value="man"></FormRadioInput>&nbsp;&nbsp;Hombre&nbsp;&nbsp;</label>
        <label><FormRadioInput v-model="form.gender" id="woman" name="gender" value="woman"></FormRadioInput>&nbsp;&nbsp;Mujer&nbsp;&nbsp;</label>
        <label><FormRadioInput v-model="form.gender" id="no-specify" name="gender" value=""></FormRadioInput>&nbsp;&nbsp;Sin Especificar&nbsp;&nbsp;</label>
      </div>

      <br>

      <div>
        <p class="font-bold">¿Desea recibir información, cursos y ofertas mediante correo?</p>
        <input type="checkbox" v-model="form.subscribe" name="susbcribe"> De acuerdo
      </div>

      <br>

      <div>
        <p class="font-bold">¿Eres un robot?</p>
        <input type="checkbox" @change="captchaValidation" v-model="form.captcha" name="captcha"> Validar
      </div>

      <br>

      <div class="inline-flex rounded-md shadow-xs" role="group:b">
        <ButtonInput type="submit" class="rounded-s-lg hover:bg-blue-900">ENVIAR</ButtonInput>
        <ButtonInput @click="resetForm" type="reset" class="rounded-e-lg hover:bg-red-900">LIMPIAR</ButtonInput>
      </div>
    </form>
  </div>
</template>