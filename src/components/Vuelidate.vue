<template>
<div class="root">
    <h2>Create Account</h2>
    <p>
        <input type="text" 
        placeholder="Email"
        v-model="state.email">
        <span v-if="v$.email.$error">
            {{v$.email.$errors[0].$message}}
        </span>
    </p>
    <p>
        <input type="text" 
        placeholder="Phone Number"
        v-model="state.phone">
        <span v-if="v$.phone.$error">
            {{v$.phone.$errors[0].$message}}
        </span>
    </p>
    <p>
        <input 
        type="password" 
        placeholder="Password"
        v-model="state.password.password">
        <span v-if="v$.password.password.$error">
            {{v$.password.password.$errors[0].$message}}
        </span>
    </p>
    <p>
        <input type="password" 
        placeholder="Confirm Password"
        v-model="state.password.confirm">
        <span v-if="v$.password.confirm.$error">
            {{v$.password.confirm.$errors[0].$message}}
        </span>
    </p>
    <button @click="submitForm">Submit</button>
</div>
</template>

<script>
import useValidate from "@vuelidate/core";
import { 
    required,
    email, 
    minLength, 
    sameAs,
    helpers } from "@vuelidate/validators";
import {reactive, computed} from 'vue';
export default{
    setup(){
        const state =reactive({
            email: '',
            phone: '',
            password: {
                password: '',
                confirm: '',
            },
        })
        const phoneNumber = (value) => 
            /^(\+)?(88)?01[0-9]{9}$/.test(value)
            // value.includes('cool')
            // console.log(value.includes('cool'))

        // const phoneNumber = (value) => {
        //     // if (value !='1932'){
        //     //     return True
        //     // }
        //     console.log(value.include('phone'));
        //     value.include('phone')
        //     console.log(value.include('phone'));
        // }
        
        const rules = computed(() => {
  		return {
  			email: { 
                  required, 
                  email
                },
            phone: {
                required,
                phoneNumber: helpers.withMessage('Must be a valid phone number',phoneNumber),
            },
  			password: {
  				password: { 
                      required, 
                      minLength: minLength(6) },
  				confirm: { 
                      required, 
                    //   sameAs: sameAs(state.password.password) 
                    sameAs: helpers.withMessage('Both password must be same', sameAs(state.password.password)) 
                    },
  			}
  		}
        }) 
        const v$ = useValidate(rules, state)
        return{
            state,
            v$
        }
    },
    // data(){
    //     return{
    //         v$: useValidate(),
    //         email: '',
    //         password: {
    //             password: '',
    //             confirm: '',
    //         },
    //     }
    // },
  	// validations() {
  	// 	return {
  	// 		email: { required },
  	// 		password: {
  	// 			password: { required },
  	// 			confirm: { required },
  	// 		}
  	// 	}
    // },
    methods:{
        submitForm(){
            console.log(this.v$);
            this.v$.$validate();
            if(!this.v$.$error){
                alert('Form successfully submitted')
            }else{
                alert('Form failed validation')
            }
            
        }
    }
}
</script>

<style scoped>
.root{
    width: 400px;
    margin: 0 auto;
    background-color: #fff;
    padding: 30px;
    margin-top: 100px;
    border-radius: 20px;
}
input{
    border: none;
    outline: none;
    border-bottom: 1px solid #ddd;
    font-size: 1em;
    padding: 5px 0;
    margin: 10px 0 5px 0;
    width: 100%;
}
button {
    background-color: #3498db;
    padding: 10px 20px;
    margin-top: 10px;
    border: none;
    color: white;
}
</style>