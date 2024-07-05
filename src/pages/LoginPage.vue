<template>



  <div class="flex justify-center items-center w-full min-h-screen bg-gray-400">
  <div class="flex flex-col w-1/3 justify-center p-4 rounded-md text-black bg-white">
    
    <div class="text-2xl font-bold mb-2 text-[#1e0e4b] text-center">Bienvenido a <span
        class="text-[#7747ff]">Ecotech App</span></div>
    <div class="text-lg font-semibold mb-4 text-center text-[#1e0e4b]">Iniciar Sesion</div>
    
    <form class="flex flex-col gap-3 ">
      <div class="block relative">
        <label for="email" class="block text-gray-600 cursor-text text-sm leading-[140%] font-normal mb-2">Correo Electronico</label>
        <input type="text" id="email"
          class="rounded border border-gray-200 text-sm w-full font-normal leading-[18px] text-black tracking-[0px] appearance-none block h-11 m-0 p-[11px] focus:ring-2 ring-offset-2  ring-gray-900 outline-0">

      </div>
      <div class="block relative">
        <label for="password"
          class="block text-gray-600 cursor-text text-sm leading-[140%] font-normal mb-2">Contraseña</label>
        <input type="text" id="password"
          class="rounded border border-gray-200 text-sm w-full font-normal leading-[18px] text-black tracking-[0px] appearance-none block h-11 m-0 p-[11px] focus:ring-2 ring-offset-2 ring-gray-900 outline-0">

      </div>
  
      <button type="submit"
        class="bg-[#7747ff] hover:scale-110 hover:bg-violet-700 transition w-max m-auto px-6 py-3 rounded text-white text-sm font-normal">Enviar</button>

    </form>
    <div class="text-sm text-center mt-[1.6rem]">Aun no tienes una cuenta? <a class="text-sm text-[#7747ff]"
        href="#">¡Regístrate gratis!</a></div>
  </div>
</div>





  <!--contenedor login-->
  <div class="container-fluid">
    <div class="row justify-content-center align-items-center vh-100">
      <div class="col-md-8">
        <div class="card card-body" id="card">
          <div class="row align-items-center" id="row">
            <!--formulario credenciales-->
            <div class="col-md-6 mb-3 mb-md-0">
              <form @submit.prevent="login">
                <!--entrada username-->
                <div class="mb-3">
                  <label for="username" class="form-label text-sm text-white">Nombre de usuario</label>
                  <input type="text" id="username" v-model="username" required class="form-control"
                    placeholder="Ingrese el nombre de usuario" />
                </div>
                <!--entrada password-->
                <div class="mb-3">
                  <label for="password" class="form-label text-sm text-white">Contraseña</label>
                  <input type="password" id="password" v-model="password" required class="form-control"
                    placeholder="Ingrese la contraseña" />
                </div>
                <div v-if="error" class="text-danger mt-3">{{ error }}</div>
              </form>
            </div>
            <div class="col-md-6 mb-3 mb-md-0">
              <div class="text-center">
                <button @click="login" class="btn fw-bold btn-light rounded" id="btn">
                  Iniciar sesión
                </button>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { getUsers } from "@/services/service.js";

export default {
  data() {
    return {
      username: "",
      password: "",
      error: "",
    };
  },
  methods: {
    async login() {
      try {
        const users = await getUsers();
        const user = users.find(
          (user) => user.username === this.username && user.password === this.password
        );
        if (user) {
          sessionStorage.setItem("userId", user.id);
          this.$router.push("/notas");
        } else {
          this.error = "Nombre de usuario o contraseña incorrectos";
        }
      } catch (error) {
        this.error = "Error al cargar los datos de usuario";
      }
    },
  },
};
</script>

<style>
#card {
  background-color: rgb(22, 30, 31);
  border-radius: 25px;
  padding: 20px;
  width: 90%;
  max-width: 1200px;
  margin-left: auto;
  margin-right: auto;
}

#btn {
  margin-top: 1rem;
  position: relative;
  top: -30px;
}

#row {
  position: relative;
  left: 5%;
}
</style>
