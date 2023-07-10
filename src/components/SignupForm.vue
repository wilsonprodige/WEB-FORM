<template>
    <form @submit.prevent="handleSubmit">
        <label>Email:</label>
        <input   type="email" required v-model="email">

        <label>Password:</label>
        <input   type="password" required v-model="pwd">
        <div v-if="passwordError" class="error">{{ passwordError }}</div>



        <label>Role</label>
        <select v-model="role">
            <option value="developer">Web developer</option>
            <option value="designer">Web designer</option>

        </select>

        <label>skills</label>
        <input type="text" v-model="tempskill" @keyup.ctrl="addskill">


        <div v-for="skill in skills" :key="skill" class="pill">
            <span @click="deleteSkill(skill)">{{ skill }}</span>


        </div>
        <div class="terms">
            <input type="checkbox" required v-model="terms"/>
            <label>Accept terms and conditions</label>
        </div>

        <div class="submit">
            <button>Create  Account</button>
        </div>

       
    </form>
    

  
</template>

<script>
export default {
    data(){
        return {
            email:'',
            pwd:'',
            role:'designer',
            terms:false,
            tempskill:'',
            skills:[],
            passwordError:''
            
        
        }
    },
    methods:{
        //fired when a user presses a key and lifts it up
        addskill(e){
            if(e.key===',' && this.tempskill){
                if(!this.skills.includes(this.tempskill)){
                    this.skills.push(this.tempskill);
                }
                
                this.tempskill='';
            }

        },
        deleteSkill(skill){
            this.skills=this.skills.filter((item)=> {
                return skill !== item
            })


        },
        handleSubmit(){
            //validation
            this.passwordError=this.pwd.length > 8 ? 
            '' : 'password must be atleast 6 characters long';

            if(!this.passwordError){
                console.log('email: ',this.email)
                console.log('password: ',this.pwd)  
                console.log('role: ',this.role)
                console.log('skills: ',this.skills)
                console.log('terms accepted: ',this.terms)
            }


        }

    }

}
</script>

<style>
form{
    min-width: 420px;
    display: inline-block;
    background: white;
    text-align: left;
    padding: 40px;
    border-radius: 10px;
}
label{
    color: #aaa;
    display: inline-block;
    margin: 25px 0 15px;
    font-size:0.6em;
    text-transform: uppercase;
    letter-spacing: 1px;
    font-weight: bold;

}
input,select{
    border: none;
    color: #555;
    border-bottom: 1px solid #555;
    box-sizing: border-box;
    width: 100%;
    display: block;
    padding: 10px 6px;
}
input[type="checkbox"]
{
    display: inline-block;
    width: 16px;
    margin: 0 10px 0 0;
    position: relative;
    top: 2px;
    

}
.pill{
    display: inline-block;
    margin: 20px 10px 0 0;
    padding: 6px 12px;
    background: #eee;
    border-radius: 20px;
    font-size: 12px;
    letter-spacing: 1px;
    font-weight: bold;
    color: #777;
    cursor: pointer;

}
button{
    background: #0b6dff;
    border: 0;
    padding: 10px 20px;
    margin-top: 20px;
    color: white;
    border-radius: 20px;
    cursor: pointer;
}
.submit{
    text-align: center;

}
.error{
    color: #ff0062;
    margin-top: 10px;
    font-size: 0.8em;
    font-weight: bold;


}
</style>