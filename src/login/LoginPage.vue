<style scoped>
.background{
    width: 430px;
    height: 520px;
    position: absolute;
    transform: translate(-50%,-50%);
    left: 50%;
    top: 50%;
}
.background .shape{
    height: 200px;
    width: 200px;
    position: absolute;
    border-radius: 50%;
}
.shape:first-child{
    background: linear-gradient( to right, #2ffff7, #9319f0 );
    left: -50px;
    top: -103px;
}
.shape:last-child{
    background:linear-gradient( to right, #2ffff7, #9319f0 );
    right: -30px;
    bottom: -80px;
}
form{
    height: 580px;
    width: 400px;
   background-color: rgb(0 0 0 / 6%);
    /* background-color: rgba(255,255,255,0.13); */
    position: absolute;
    transform: translate(-50%,-50%);
    top: 50%;
    left: 50%;
    border-radius: 10px;
    backdrop-filter: blur(10px);
    border: 2px solid rgba(255,255,255,0.1);
    box-shadow: 0 0 40px rgba(8,7,16,0.6);
    padding: 50px 35px;
}
form *{
    letter-spacing: 0.5px;
    outline: none;
    border: none;
}
form h3{
    font-size: 35px;
    font-weight: 600;
    line-height: 42px;
    text-align: center;
    font-style: bold;
}

.inputclass{
   background-color: rgba(255,255,255,0.07);
    border-radius: 3px;
    font-size: 18px;
    font-weight: 300;
}
.inclass{
    background-color: transparent!important;
    border-radius: 3px !important;
    font-size: 14px;
    border: 1px solid #ffe2e233;
    font-weight: 300;
    color: white !important;

}
::placeholder{
    color: #e5e5e5;
}
.buttonclass{
    width: 100%;
    border: 1px solid #ffe2e233;
     background-color: transparent;
   color: #e8f4ff; 
    font-size: 18px;
    font-weight: 600;
    border-radius: 3px;
    cursor: pointer;
}
.buttonclass:hover{
    background-color:#9319f0 ;
   color: #e8f4ff; 

}

.go{
     padding: 5px 10px 10px 5px;
    border-radius: 3px;
  background-color: rgba(255,255,255,0.27);
  color: #eaf0fb;
  text-align: center;
}
.go:hover{
     background-color: rgba(255,255,255,0.47);
}
.fb:hover{
     background-color: rgba(255,255,255,0.47);
}
.fb{
     padding: 5px 10px 10px 5px;
    border-radius: 3px;
  background-color: rgba(255,255,255,0.27);
  color: #eaf0fb;
  text-align: center;
}
.invalid-feedback{
    color: red !important;
}
.textmutednew{
    color: #e8f4ff;
}
</style>
<template>
    <div>
          <div class="background">
        <div class="shape"></div>
        <div class="shape"></div>
    </div>
    <form  class="textmutednew" @submit.prevent="handleSubmit">
        <h3 >Login Here</h3>
   
            <div class="form-group"><i class='fas fa-user'></i>
               <label class="" for="username">
                   Username</label>
                <input type="text" v-model="username" name="username" placeholder="Type here" class="inclass p-2 col-12 form-control" :class="{ 'is-invalid': submitted && !username }" />
                <div v-show="submitted && !username" class="invalid-feedback">Username is required</div></div>
          
            <div class="form-group"><i class="fas fa-key"></i>
                <label htmlFor="password">Password</label>
                <input type="password" v-model="password" name="password" placeholder="Type here" class="inclass p-2  col-12 form-control" :class="{ 'is-invalid': submitted && !password }" />
                <div v-show="submitted && !password" class="invalid-feedback">Password is required</div>
            </div>
            <div class="form-group">
             <div class="row"> <div class="col-12">  <button class=" buttonclass p-2" :disabled="status.loggingIn">Log In
                <img v-show="status.loggingIn" src="data:image/gif;base64,R0lGODlhEAAQAPIAAP///wAAAMLCwkJCQgAAAGJiYoKCgpKSkiH/C05FVFNDQVBFMi4wAwEAAAAh/hpDcmVhdGVkIHdpdGggYWpheGxvYWQuaW5mbwAh+QQJCgAAACwAAAAAEAAQAAADMwi63P4wyklrE2MIOggZnAdOmGYJRbExwroUmcG2LmDEwnHQLVsYOd2mBzkYDAdKa+dIAAAh+QQJCgAAACwAAAAAEAAQAAADNAi63P5OjCEgG4QMu7DmikRxQlFUYDEZIGBMRVsaqHwctXXf7WEYB4Ag1xjihkMZsiUkKhIAIfkECQoAAAAsAAAAABAAEAAAAzYIujIjK8pByJDMlFYvBoVjHA70GU7xSUJhmKtwHPAKzLO9HMaoKwJZ7Rf8AYPDDzKpZBqfvwQAIfkECQoAAAAsAAAAABAAEAAAAzMIumIlK8oyhpHsnFZfhYumCYUhDAQxRIdhHBGqRoKw0R8DYlJd8z0fMDgsGo/IpHI5TAAAIfkECQoAAAAsAAAAABAAEAAAAzIIunInK0rnZBTwGPNMgQwmdsNgXGJUlIWEuR5oWUIpz8pAEAMe6TwfwyYsGo/IpFKSAAAh+QQJCgAAACwAAAAAEAAQAAADMwi6IMKQORfjdOe82p4wGccc4CEuQradylesojEMBgsUc2G7sDX3lQGBMLAJibufbSlKAAAh+QQJCgAAACwAAAAAEAAQAAADMgi63P7wCRHZnFVdmgHu2nFwlWCI3WGc3TSWhUFGxTAUkGCbtgENBMJAEJsxgMLWzpEAACH5BAkKAAAALAAAAAAQABAAAAMyCLrc/jDKSatlQtScKdceCAjDII7HcQ4EMTCpyrCuUBjCYRgHVtqlAiB1YhiCnlsRkAAAOwAAAAAAAAAAAA==" />
                 
                 </button></div>
            </div>
            <div class="row pt-3"> <div class="col-12 "> <router-link to="/register"> <button class="buttonclass p-2">Register</button></router-link></div></div>
        <div class="row pt-3">
          <div class="col-6"><div class="go pointer" ><i class="fab fa-google"></i>  Google</div></div>
          <div class="col-6 text-right "><div class="fb"><i class="fab fa-facebook"></i>  Facebook</div></div>
        </div>
                <!-- <router-link to="/register" class="btn btn-link">Register</router-link> -->
            </div>
        </form>
    </div>
</template>

<script>
import { mapState, mapActions } from 'vuex'

export default {
    data () {
        return {
            username: '',
            password: '',
            submitted: false
        }
    },
    computed: {
        ...mapState('account', ['status'])
    },
    created () {
        // reset login status
        this.logout();
    },
    methods: {
        ...mapActions('account', ['login', 'logout']),
        handleSubmit (e) {
            this.submitted = true;
            const { username, password } = this;
            if (username && password) {
                this.login({ username, password })
            }
        }
    }
};
</script>