<style scoped>
.background{
    width: 556px;
    height: 562px;
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
    left: 6px;
    top: -83px;
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
    padding: 8px 35px;
}
form *{
    font-family: 'Montserrat' !important;
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
    /* background-color:  rgba(255,255,255,0.07); */
     background-color: transparent;
   color: #e8f4ff; 
    font-size: 18px;
    font-weight: 600;
    border-radius: 3px;
    cursor: pointer;
}
.buttonclass:hover{
    background-color:#9319f0 ;
    /* background-color:  rgba(255,255,255,0.07); */
     /* background-color: transparent!important; */
   color: #e8f4ff; 
    /* font-size: 18px;
    font-weight: 600;
    border-radius: 3px; */
    /* cursor: pointer; */
}

.go{
     padding: 5px 10px 10px 5px;
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
form:select{
    background: transparent !important;
}
</style>
<template>

    <div>
          <div class="background">
        <div class="shape"></div>
        <div class="shape"></div>
    </div>
         <div>
        
        <form  class="textmutednew" @submit.prevent="handleSubmit">
        <h2 class="textmutednew text-center">Register</h2>

            <div class="form-group">
                <label for="firstName">First Name</label>
                <input type="text" v-model="user.firstName" v-validate="'required'" name="firstName" class="inclass p-2 col-12 form-control" :class="{ 'is-invalid': submitted && errors.has('firstName') }" />
                <div v-if="submitted && errors.has('firstName')" class="invalid-feedback">{{ errors.first('firstName') }}</div>
            </div>
            <div class="form-group">
                <label for="lastName">Last Name</label>
                <input type="text" v-model="user.lastName" v-validate="'required'" name="lastName" class="inclass p-2 col-12 form-control" :class="{ 'is-invalid': submitted && errors.has('lastName') }" />
                <div v-if="submitted && errors.has('lastName')" class="invalid-feedback">{{ errors.first('lastName') }}</div>
            </div>
            <div class="form-group">
                <label for="username">Username</label>
                <input type="text" v-model="user.username" v-validate="'required'" name="username" class="inclass p-2 col-12 form-control" :class="{ 'is-invalid': submitted && errors.has('username') }" />
                <div v-if="submitted && errors.has('username')" class="invalid-feedback">{{ errors.first('username') }}</div>
            </div>
            <div class="form-group">
                <label htmlFor="password">Password</label>
                <input type="password" v-model="user.password" v-validate="{ required: true, min: 6 }" name="password" class="inclass p-2 col-12 form-control" :class="{ 'is-invalid': submitted && errors.has('password') }" />
                <div v-if="submitted && errors.has('password')" class="invalid-feedback">{{ errors.first('password') }}</div>
            </div>
            <div class="form-group">
                <div class="col-12 ">
                <div class="row pt-3">  
                    <div class="col-6 px-0">
                        <button class="buttonclass p-2" :disabled="status.registering">Register
                <img v-show="status.registering" src="data:image/gif;base64,R0lGODlhEAAQAPIAAP///wAAAMLCwkJCQgAAAGJiYoKCgpKSkiH/C05FVFNDQVBFMi4wAwEAAAAh/hpDcmVhdGVkIHdpdGggYWpheGxvYWQuaW5mbwAh+QQJCgAAACwAAAAAEAAQAAADMwi63P4wyklrE2MIOggZnAdOmGYJRbExwroUmcG2LmDEwnHQLVsYOd2mBzkYDAdKa+dIAAAh+QQJCgAAACwAAAAAEAAQAAADNAi63P5OjCEgG4QMu7DmikRxQlFUYDEZIGBMRVsaqHwctXXf7WEYB4Ag1xjihkMZsiUkKhIAIfkECQoAAAAsAAAAABAAEAAAAzYIujIjK8pByJDMlFYvBoVjHA70GU7xSUJhmKtwHPAKzLO9HMaoKwJZ7Rf8AYPDDzKpZBqfvwQAIfkECQoAAAAsAAAAABAAEAAAAzMIumIlK8oyhpHsnFZfhYumCYUhDAQxRIdhHBGqRoKw0R8DYlJd8z0fMDgsGo/IpHI5TAAAIfkECQoAAAAsAAAAABAAEAAAAzIIunInK0rnZBTwGPNMgQwmdsNgXGJUlIWEuR5oWUIpz8pAEAMe6TwfwyYsGo/IpFKSAAAh+QQJCgAAACwAAAAAEAAQAAADMwi6IMKQORfjdOe82p4wGccc4CEuQradylesojEMBgsUc2G7sDX3lQGBMLAJibufbSlKAAAh+QQJCgAAACwAAAAAEAAQAAADMgi63P7wCRHZnFVdmgHu2nFwlWCI3WGc3TSWhUFGxTAUkGCbtgENBMJAEJsxgMLWzpEAACH5BAkKAAAALAAAAAAQABAAAAMyCLrc/jDKSatlQtScKdceCAjDII7HcQ4EMTCpyrCuUBjCYRgHVtqlAiB1YhiCnlsRkAAAOwAAAAAAAAAAAA==" />

                </button>
                    </div>
                    <div class="col-6 pr-0">
                    <router-link to="/login" class=""> <button class="buttonclass p-2">
                Cancel
                </button></router-link></div></div></div>


            </div>
        </form>
    </div>
    </div>
</template>

<script>
import { mapState, mapActions } from 'vuex'

export default {
    data () {
        return {
            user: {
                firstName: '',
                lastName: '',
                username: '',
                password: ''
            },
            submitted: false
        }
    },
    computed: {
        ...mapState('account', ['status'])
    },
    methods: {
        ...mapActions('account', ['register']),
        handleSubmit(e) {
            this.submitted = true;
            this.$validator.validate().then(valid => {
                if (valid) {
                    this.register(this.user);
                }
            });
        }
    }
};
</script>