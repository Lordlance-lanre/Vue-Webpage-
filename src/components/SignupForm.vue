<template>
    <form @submit.prevent="handleSubmit">
        <label>Email: </label>
        <input type="email" required v-model="email">

        <label>Password: </label>
        <input type="password" required v-model="password">
        <div v-if="passwordError" class="error">{{ passwordError }}</div>
        <label>Role: </label>

    <select v-model="role">
        <option value="developer">Web developer</option>
        <option value="designer">Web designer</option>
    </select>

    <label>Skills: </label>
    <input type="text" v-model="tempSkills" @keyup.alt="addSkills">
    <div v-for="skill in skills" :key="skills" class="pill">
     <span @click="deleteSkill(skill)">{{skill}}</span>
    </div>

    <div class="terms"></div>
    <input type="checkbox" required v-model="terms">
    <label>Accept terms and conditions</label>

    <div class="submit">
        <button>Create an account</button>
    </div>
</form>


    <p>Email: {{email}}</p>
    <p>Password: {{password}}</p>
    <p>Role: {{role}}</p>
    <p>Accept terms: {{ terms }}</p>
</template>

<script>
export default{
    data(){
        return {
            email: ' ',
            password: ' ',
            role: ' ',
            terms: false,
            tempSkills: ' ',
            skills: [],
            passwordError: ' '
        }
    },
    methods: {
        addSkills(e){
            if(e.key === ',' && this.tempSkills){
                if(!this.skills.includes(this.tempSkills)){
                    this.skills.push(this.tempSkills)
                }
                this.tempSkills = " "
            }
        },
        deleteSkill(skill){
            this.skills = this.skills.filter((item) => {
                return skill !== item
            })
        },
        handleSubmit(){
            this.passwordError = this.password.length > 5 ? 
            '': 'password must be at least 6 chars long'
            if(!this.passwordError){
                console.log('email', this.email)
                console.log('password', this.password)
                console.log('role', this.role)
                console.log('skills', this.skills)
                console.log('terms accepted', this.terms)
            }
        }
    }

}
</script>

<style>
    form{
        max-width: 420px;
        margin: 40px auto;
        background: white;
        text-align: left;
        padding: 60px;
        border-radius: 10px;
        
    }
    label{
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
    }
    .submit{
        text-align: center;
    }
    button:hover{
        background-color: grey;
        color: rgba(235, 227, 227, 0.904);
        transition: 0.5s ease-in-out;
    }
    .error{
        color: #ff0062;
        margin-top: 10px;
        font-size: 0.8em;
        font-weight: bold;
    }
   
</style>