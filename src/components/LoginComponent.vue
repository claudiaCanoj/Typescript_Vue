<template>
  <h1>Acceso a la tienda</h1>
  <form @submit="login">
    <div>{{ error }}</div>
    <div>
      <input type = "email" id = "user" name = "user" placeholder="Usuario" v-model = "user" required/>
    </div>  
    <div>
      <input type = "password" id = "password" name = "password" placeholder="Contraseña" v-model = "password" required/>
    </div>
    <div>
      <input type = "submit" id = "login" value = "Acceder"/>
    </div>
  </form> 
</template>

<script>
export default {
  name: 'LoginComponent',
  data() { 
    return {
      user: "",
      password: "",
      error: ""
    }
  }, 
  methods: {    
    login(e) {
      const data = { 
        "email" : this.user, 
        "password": this.password
      };
      fetch("https://api.escuelajs.co/api/v1/auth/login", 
            { 
              method: 'POST', 
              body: JSON.stringify(data)
            })
        .then((response) => {
          e.preventDefault();
          if (response.statusCode != "201") {
            this.error = response;
            e.preventDefault();
          }         
        })  
        .then((error) => this.error = error);
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
