<style scoped>
::placeholder{
    color: #e5e5e5;
}
.buttonclass{
    border: 1px solid #ffe2e233;
     background-color: transparent;
   color: #e8f4ff; 
    font-size: 18px;
    font-weight: 600;
    border-radius: 3px;
    cursor: pointer;
}
.buttonclass:hover{
    background-color: #cb24eca3 ;
   color: #e8f4ff; 
}

.invalid-feedback{
    color: red !important;
}
.textmutednew{
    color: #e8f4ff;
}
.newcard{
    height: 620px;
    width: 800px;
   background: linear-gradient(45deg, #cb24eca3, #d7baed54);
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
.inclass{
    background-color: transparent!important;
    border-radius: 3px !important;
    font-size: 14px;
    border: 1px solid #ffe2e233;
    font-weight: 300;
    color: white !important;
}
</style>
<template>
    <div class="container newcard py-5 textmutednew">
        <div class="col-12 text-center  justify-content-center">
        <h1>Hi {{account.user.firstName}}!!! This is your Home Page</h1> 
       
        <p>You're currently Logged In </p>
        <h3>Here are the  List Of User in Your Platform</h3>
        <em v-if="users.loading">Loading users...</em>
        <span v-if="users.error" class="text-danger">ERROR: {{users.error}}</span>
        <ul v-if="users.items">
            <li class="inclass p-2 mt-2" v-for="user in users.items" :key="user.id">
            <div class="row">  <div class="col-6 text-left">  {{user.firstName + ' ' + user.lastName}}</div>
             <div class="col-6 text-right"> 
                    <span v-if="user.deleting"><em> - Deleting...</em></span>
                <span v-else-if="user.deleteError" class="text-danger"> - ERROR: {{user.deleteError}}</span>
               <span v-else> - 
                      <a @click="deleteUser(user.id)" class="text-danger"><i class="fas fa-trash btn btn-danger"></i></a></span>
            </div> </div>
            </li>
        </ul>
         <p>
            <router-link to="/login"> <button class="buttonclass p-3 w-25"><i class="fas fa-power-off fa-lg"></i></button></router-link>
        </p>
        
    </div></div>
</template>

<script>
import { mapState, mapActions } from 'vuex'

export default {
    computed: {
        ...mapState({
            account: state => state.account,
            users: state => state.users.all
        })
    },
    created () {
        this.getAllUsers();
    },
    methods: {
        ...mapActions('users', {
            getAllUsers: 'getAll',
            deleteUser: 'delete'
        })
    }
};
</script>