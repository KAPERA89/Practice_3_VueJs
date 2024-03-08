<template>
    <form @submit.prevent="handleSubmit">
        <lable>Email : </lable>
        <input type="email" required v-model="email"/>

        <lable>Password : </lable>
        <input type="password" required v-model="password"/>
        <div v-if="passwordError" class="error">
            {{passwordError}}
        </div>


        <lable>Role : </lable>
        <select v-model="role">
            <option value="developer">Web Developer</option>
            <option value="designer">Web Designer</option>
        </select>


        <lable>Skills : </lable>
        <input type="text" v-model="tempSkill" @keyup="addSkill"/>
        <div v-for="skill in skills" :key="skill" class="pill" >
         <span @click="deleteSkill(skill)">{{skill}}</span>
        </div>


        <div class="terms">
            <input type="checkbox" v-model="terms" required>
            <label>Accept terms and conditions </label>
        </div>


        <!-- <div>
            <input type="checkbox" value="Shaun" v-model="names">
            <label>Shaun</label>
        </div>
        <div>
            <input type="checkbox" value="yoshi" v-model="names">
            <label>yoshi</label>
        </div>
        <div>
            <input type="checkbox" value="mario" v-model="names">
            <label>mario</label>
        </div> -->


        <div class="submit">
            <button>Create an account</button>
        </div>

    </form>

    <p>email : {{email}}</p>
    <p>password : {{password}}</p>
    <p>Role : {{role}}</p>
    <p>Terms : {{terms}}</p>
    
    <!-- <p>Names : {{names}} </p> -->
</template>
    


<script>
export default {
    data() {
        return {
            email: '',
            password: '',
            role: '',
            terms : false,
            tempSkill: '',
            skills : [],
            passwordError: '',
            // names: []
        }
    },
    methods: {
        addSkill(e){
            if(e.key === ',' && this.tempSkill){
                if(!this.skills.includes(this.tempSkill.split(",")[0])){
                    this.skills.push(this.tempSkill.split(",")[0]);
                }
                this.tempSkill = ''
            }
        },
        deleteSkill(skill){
           this.skills = this.skills.filter(s => s!=skill);
        },
        handleSubmit(){
            //validate password   
            this.passwordError = this.password.length>5 ? '' : 'password must be at least 6 chars long'

            if(!this.passwordError){
                console.log('email : ', this.email)
                console.log('password : ', this.password)
                console.log('role : ', this.role)
                console.log('skills : ', this.skills)
                console.log('terms accepted : ', this.terms)
            }
        }
    },
}
</script>



<style>
    form{
        max-width: 420px;
        margin: 30px auto;
        background: white;
        text-align: left;
        padding: 40px;
        border-radius: 10px;
    }
    lable{
        color: #aaa;
        display: inline-block;
        margin: 25px 0 15px;
        font-size: 0.6em;
        text-transform: uppercase;
        letter-spacing: 1px;
        font-weight: bold;
    }   
    input, select{
        display: block;
        padding: 10px 6px;
        width: 100%;
        box-sizing: border-box;
        border: none;
        border-bottom: 1px solid #ddd;
        color: #555;
    }
    input[type="checkbox"]{
        display: inline-block;
        width: 16px;
        margin: 0 10px 0 0;
        position: relative;
        top: 2px;
    }
    .terms{
        margin-top: 30px;
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
    button {
        background: #0b6dff;
        border: 0;
        padding: 10px 20px;
        margin-top: 20px;
        color: white;
        border-radius: 20px;
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