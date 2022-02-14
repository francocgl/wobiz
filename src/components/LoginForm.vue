<template>
    <div class="col-12 col-md-6 col-lg-4 p-0 ml-0 col">
        <div class="box vh-100">
            <div>
                <figure class="img-box logo mb-5">
                    <img src="@/assets/logo.svg" alt="Logo de Wobiz"> 
                </figure>
            </div>
            <h2 class="title mb-3">Ingresa a tu cuenta</h2>
             <div v-if="msg.login && isSubmitted" class="inline-alert  mb-3" >
                <p>{{ msg.login }} </p>
            </div>
            <form @submit.prevent="handleLogin">
                <fieldset class="form-group mb-3">
                    <label for="user">Email</label>
                    <input  
                        autocomplete="off"
                        v-model="user"
                        id="user"
                        name="user"
                        type="text"
                        placeholder="Ej: usuario@mail.com"
                        class="form-control"
                    />
                    <div v-if="msg.user && isSubmitted" class="inline-alert mt-3" >
                        <p>{{ msg.user }}</p>
                    </div>
                </fieldset>
                <fieldset class="form-group mb-3">
                    <label for="password">Contraseña</label>
                    <input 
                        autocomplete="off"
                        v-model="password"
                        id="password" 
                        name="password" 
                        type="password" 
                        placeholder="Escribe tu contraseña" 
                        class="form-control"
                    /> 
                    <div v-if="msg.password && isSubmitted" class="inline-alert mt-3" >
                        <p>{{ msg.password }} </p>
                    </div>
                </fieldset>
                <fieldset class="form-group mb-1 mt-1">
                    <a href="#" class="link">¿Olvidaste tu contraseña?</a>
                </fieldset>
                <fieldset class="form-group">
                    <button type="submit" class="btn btn-submit mt-3"  >Ingresar a mi cuenta </button>
                </fieldset>
            </form>
        </div>
    </div>
</template>

<script>
import axios from 'axios';

export default {
    name : 'LoginForm',
    data(){
        return{
            user: '',
            password: '',
            emailRegex : RegExp(/^[a-z0-9]+@[a-z]+\.[a-z]{2,3}$/),
            isSubmitted: false,
            msg: [] 
        }
    },
    watch : {
        password(value){
            if(!value){
                this.msg['password'] = 'Necesitamos tu contraseña.';
            }else{
                if(value.length < 6) {
                    this.msg['password'] = 'La contraseña no tiene un formato válido.';
                } else {
                    this.msg['password'] = '';
                }
            }
        },
        user(value){
            if(!value){
                this.msg['user'] = 'Necesitamos tu email.';
            }else{
                if (!this.emailRegex.test(value)) {
                    this.msg['user'] = 'El email ingresado no es correcto.';
                } else {
                    this.msg['user'] = '';
                }
            }
        }
    },
    methods : {
        async handleLogin() {
            const { user, password, msg } = this;
            this.isSubmitted = true;
            this.msg = []

            // Validate email
            if(!user){
                this.msg['user'] = 'Necesitamos tu email.';
            }else{
                if (!this.emailRegex.test(user)) {
                    this.msg['user'] = 'El email ingresado no es correcto.';
                } else {
                    this.msg['user'] = '';
                }
            }
            // Validate password
            if(!password){
                this.msg['password'] = 'Necesitamos tu contraseña.';
            }else{
                if(password.length < 6) {
                    this.msg['password'] = 'La contraseña no tiene un formato válido.';
                } else {
                    this.msg['password'] = '';
                }
            }
            // Endpoint call
            if(msg['password'] === '' && msg['user'] === ''){
                let auth = {
                    user : user,
                    password : password 
                }
                const baseURL = 'https://admin.localwobiz.com';

                await axios.post( `${baseURL}/login`, auth )
                .then( res => {
                    console.log(res) 
                    if(res.status === 401){
                        this.msg['login'] = 'Tu email o contraseña son incorrectos. Revísalos y vuelve a intentar.'
                    }
                    if(res.status === 200){
                        // const apiToken = res.status.token;
                        // this.$router.push({ path: '/', params: { apiToken, user } }) 
                    }
                })
                .catch( error =>{
                    console.log(`Error: ${error.message}`) 
                })
            }
        }
    }
}
</script>

<style>
.login .box{
    padding: 30px 50px;
}
.login .box .logo{
    width: 180px;
}
.login form input { 
    height: 50px;
    border-radius: 0.25rem;
}
.title { 
    color: #163a49;
    font-size: 25px;
    font-weight: 700;
}
label{
    font-size: .8em!important;
    line-height: 1.5;
    padding-bottom: calc(0.375rem + 1px);
    margin-bottom: 0;
    font-weight: 500;
    display: block;
    opacity: .9;
}
.link{
    font-size: 14px;
    color: #969696;
}
/* // Errors  */
.inline-alert{
    background-color: #e85837;
    padding: 10px 25px;
    border-radius: .25rem;
}
.inline-alert p{
   color: #fff;
   margin: 0;
   font-size: .8em;
   font-weight: 600;
}

@media only screen
and (min-width : 961px) {
    @media(hover: hover) {
        .link:hover{ color: #363636; }
        .login label:hover{ opacity: 1; }
    }
}
</style>