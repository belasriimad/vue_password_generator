<template>
   <div class="container">
      <div class="row my-5">
         <div class="col-md-8 mx-auto">
            <div class="card">
               <div class="card-body">
                  <div class="card-title text-center">
                     <h3>Password Generator</h3>
                  </div>
                  <hr>
                  <div class="row mt-4">
                     <div class="col-md-6 mx-auto">
                        <div class="form-group d-flex">
                           <input type="text" 
                              v-model="data.password"   
                              class="form-control rounded-0" placeholder="Password">
                           <button @click="copyPassword" class="btn btn-sm btn-dark rounded-0">
                              <i class="bi bi-files"></i>
                           </button>
                        </div>
                        <div class="form-group row mt-3 d-flex align-items-center">
                           <div class="col-md-8">
                              Password Length
                           </div>
                           <div class="col-md-4">
                              <input type="number" 
                                 v-model="data.passwordLength"     
                                 name="length" placeholder="Length" min="6" max="20" class="form-control">
                           </div>
                        </div>
                        <div class="form-check my-2">
                           <input class="form-check-input" 
                              v-model="data.uppercase"  
                              type="checkbox" id="uppercase">
                           <label class="form-check-label" for="uppercase">
                              Include Uppercase
                           </label>
                        </div>
                        <div class="form-check my-2">
                           <input class="form-check-input" 
                              v-model="data.lowercase"  
                              disabled type="checkbox" id="lowercase">
                           <label class="form-check-label" for="lowercase">
                                 Include Lowercase
                           </label>
                        </div>
                        <div class="form-check my-2">
                           <input class="form-check-input" 
                              v-model="data.numbers"  
                              disabled type="checkbox" id="numbers">
                           <label class="form-check-label" for="numbers">
                                 Include Numbers
                           </label>
                        </div>
                        <div class="form-check my-2">
                           <input class="form-check-input" 
                              v-model="data.symbols"  
                              type="checkbox" id="symbols">
                           <label class="form-check-label" for="symbols">
                                 Include Symbols
                           </label>
                        </div>
                        <hr>
                        <div class="d-flex justify-content-center my-2">
                           <button @click="generatePassword" class="btn btn-block btn-dark">
                              Generate Password
                           </button>
                        </div>
                     </div>
                  </div>
               </div>
            </div>
         </div>
      </div>
   </div>
</template>

<script setup>
   import { reactive } from "vue";
   import { upperCaseLetters, lowerCaseLettters, numbers, specialCharacters } from '../helper';

   const data = reactive({
      password: '',
      passwordLength: 20,
      uppercase: false,
      lowercase: true,
      numbers: true,
      symbols: false
   });

   const generatePassword = () => {
      data.password = '';
      let charsList = lowerCaseLettters;
      charsList += numbers;
      if(data.uppercase){
         charsList += upperCaseLetters;
      }
      if(data.symbols){
         charsList += specialCharacters;
      }
      //generate the password
      for(let i = 0; i < data.passwordLength; i++){
         const charIndex = Math.round(Math.random() * charsList.length);
         data.password = data.password + charsList.charAt(charIndex);
      }
   }

   const copyPassword = () => {
      // Copy the password inside the text field
      navigator.clipboard.writeText(data.password);

      // Alert the copied text
      alert("Copied the password: " + data.password);
   }
</script>

<style>

</style>