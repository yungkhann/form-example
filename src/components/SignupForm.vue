<template>
    <form @submit.prevent="handleSubmit">
        <label>Email:</label>
        <input  v-model="email" type="email" placeholder="Email address..." required>
        <label>Password:</label>
        <input v-model="password" placeholder="Your password..." type="password" required>
        <div v-if="passwordErr" class="error"> {{passwordErr}} </div>
        <label>Role:</label>
        <select v-model="role">
            <option value="WebDeveloper">Web Developer</option>
            <option value="PythonDeveloper">Python Developer</option>
            <option value="RubyDeveloper">Ruby Developer</option>
            <option value="PHPDeveloper">PHP Developer</option>
            <option value="musician">Күйші</option>
        </select>

        <label>Skills:</label>
        <input @keyup="addSkill" type="text" v-model="tempSkill">

       <div class="user-skills">
           User Skills:
            <span @click="deleteSkill(skill)" v-for="skill in skills" :key="skill" class="pill">
                {{skill}} <abbr/>
            </span>
       </div>

        <div class="terms">
            <input v-model="terms"  type="checkbox" required>
            <label>Accept terms and conditions</label>
        </div>
        <div class="submit">
            <button>Create an Account</button>
        </div>
        
    </form>
    <p>Email is {{email}} </p>
    <p>Password is {{password}} </p>
    <p>Role is {{role}} </p>
    <p>Is terms accepted? {{terms}} </p>
 
</template>
<script>
export default {
    data() {
        return {
            email:'',
            password:'',
            role:'',
            terms:false,
            tempSkill:'',
            skills:[],
            passwordErr:''
        }
    },
    methods: {
        addSkill(e){
           if (e.key === ',' && this.tempSkill) {
               if(!this.skills.includes(this.tempSkill)){
                   this.skills.push(this.tempSkill)
               }
               this.tempSkill = ''
           }
        },
        deleteSkill(skill){
            this.skills = this.skills.filter((item) => {
                return skill !== item
            })
        },
        handleSubmit(){
            this.passwordErr = this.password.length > 5 ? '' : 'Password is to short'
            
        }
    },
}
</script>
<style>
    form{
        max-width: 420px;
        margin:30px auto;
        background: white;
        text-align: left;
        padding: 40px;
        border-radius: 10px;
        
    }
    label{
        color:#aaa;
        display: inline-block;
        margin:25px 0 15px;
        font-size:0.6em;
        text-transform: uppercase;
        letter-spacing: 1px;
        font-weight: bold;
        font-family: Avenir, Helvetica, Arial, sans-serif;
    }
    input,select{
        display: block;
        padding: 10px 6px;
        width: 100%;
        box-sizing: border-box;
        border: none;
        border-bottom: 1px solid #ccc;
        color: #555;
        outline: none;
    }
    input::placeholder{
        color: #999;
    }
    input[type="checkbox"]{
        display: inline-block;
        width: 16px;
        margin:0 10px 0 0;
        position: relative;
        top: 2px;
    }
    .pill{
        display:inline-block;
        margin:10px 10px 0 0;
        padding:6px 12px;
        background: #eee;
        border-radius: 20px;
        font-size: 12px;
        letter-spacing: 1px;
        font-weight: bold;
        color: #777;
        cursor: pointer;
    }
    .user-skills{
        margin-top: 10px;
    }
    .submit{
        text-align: center;
    }
    button{
        background:#0b6dff;
        border: 0;
        padding: 10px 20px;
        margin-top:20px;
        color:white;
        border-radius:20px
    }
    .error{
        color:#ff0062;
        margin-top: 10px;
        font-size:0.8em;
        font-weight: bold;
    }
</style>