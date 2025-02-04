<script setup>
import { ref } from 'vue'
import FormInput from './FormInput.vue';
import FormSelect from './FormSelect.vue';
import ButtonInput from './ButtonInput.vue';
import FormRadioInput from './FormRadioInput.vue';
import FormDatalist from './FormDatalist.vue';

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
  gender: "",
  subscribe: false,
  comment: "",
  button: ""
});

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
    <form autocomplete="off" class="rounded-xl text-center bg-black/35 backdrop-blur-xl p-10 place-items-center">
      <div class="grid gap-6 mb-6 md:grid-cols-2">
        <label for="name">
          <div class="font-bold">NOMBRE</div>
          <FormInput v-model="form.name" type="text" id="name" name="name"></FormInput>
        </label>

        <label for="surname">
          <div class="font-bold">APELLIDOS</div>
          <FormInput v-model="form.surname" type="text" id="surname" name="surname"></FormInput>
        </label>

        <label for="user">
          <div class="font-bold">USER</div>
          <FormInput v-model="form.user" type="text" id="user" name="user"></FormInput>
        </label>

        <label for="mail">
          <div class="font-bold">EMAIL</div>
          <FormInput v-model="form.email" type="text" id="mail" name="mail"></FormInput>
        </label>

        <label for="password">
          <div class="font-bold">CONTRASEÑA</div>
          <FormInput v-model="form.password" type="text" id="password" name="password"></FormInput>
        </label>

        <label for="birthday">
          <div class="font-bold">FECHA DE NACIMIENTO</div>
          <FormInput v-model="form.birthday" type="date" id="birthday" name="birthday" class="w-full text-center"></FormInput>
        </label>
      </div>

      <div class="grid gap-6 mb-6 md:grid-cols-2">
        <label for="street">
          <div class="font-bold">CALLE</div>
          <FormInput v-model="form.street" type="text" id="street" name="street"></FormInput>
        </label>

        <label for="building type">
          <div class="font-bold">TIPO DE EDIFICIO</div>
          <FormDatalist :options="buildingType" id="types"/>
          <FormInput list="types" id="building-type" name="building-type" required />
        </label>

        <label for="door-number">
          <div class="font-bold">Nº PUERTA</div>
          <FormInput v-model="form.doorNumber" type="text" id="door-number" name="door-number"></FormInput>
        </label>

        <label for="postalcode">
          <div class="font-bold">CÓDIGO POSTAL</div>
          <FormInput v-model="form.postalCode" type="text" id="postalcode" name="postalcode"></FormInput>
        </label>

        <label for="province">
          <div class="font-bold">PROVINCIA</div>
          <FormInput v-model="form.province" type="text" id="province" name="province"></FormInput>
        </label>

        <label for="country">
          <div class="font-bold">PAÍS</div>
          <FormInput v-model="form.country" type="text" id="country" name="country"></FormInput>
        </label>
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

      <br>

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

      <div class="inline-flex rounded-md shadow-xs" role="group:b">
        <ButtonInput type="submit" class="rounded-s-lg hover:bg-blue-900">ENVIAR</ButtonInput>
        <ButtonInput type="reset" class="rounded-e-lg hover:bg-red-900">LIMPIAR</ButtonInput>
      </div>
    </form>
  </div>
</template>