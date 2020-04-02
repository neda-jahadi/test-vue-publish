<template>
  <div>
      <h2>Register snipp</h2>
      <div class="form-snippers">
          <label>Title</label><br>
          <input type="text" placeholder="Write Title..." v-model="snipinfo.title" :class="titleClass" 
          @blur.once="titleIsTouched=true" />
           <span v-if="titleIsTouched && !titleIsValid" class="error">{{titleErrorMessage}}</span>
      </div>

      <div class="form-snippers">
          <label>Content</label><br>
          <input type="text" placeholder="Write Content..." v-model="snipinfo.content" :class="contentClass" 
          @blur.once="contentIsTouched=true" />
           <span v-if="contentIsTouched && !contentIsValid" class="contentError">{{contentErrorMessage}}</span>
      </div>
      <button @click="submitSnipp" :disabled="!contentIsValid || !titleIsValid">Submit!</button>
      <button @click="check">Check!</button>
      
      <!--{{snipinfo}}-->
      
  </div>
</template>

<script>
const url = 'https://www.forverkliga.se/JavaScript/api/api-snippets.php?';
export default {
 data: ()=>({
     snipinfo :{
         title: '',
         content:''
     },
     titleIsTouched: false,
     contentIsTouched: false
     

 }),
 methods: {
     check() {
         console.log('snipinfo.title is:',this.snipinfo.title);
     },
        async submitSnipp() {
            try {
                let response = await this.$http.post(url, {
					params: { 
                        add: '',
                        title: this.snipinfo.title,
                        content: this.snipinfo.content
                         }
                });
                console.log(response);
            }
            catch(error) {
				console.log('Something went wrong', error);
			}
        }
    },
 
 computed: {
     titleIsValid() {
         return this.snipinfo.title.length >=3 ;
     },
     titleClass() {
         if (!this.titleIsTouched) return '';
         return this.titleIsValid ? 'valid' : 'invalid';
     },
     titleErrorMessage() {
         return 'Enter at least 3 characters.';
     },
     contentIsValid() {
         return this.snipinfo.content.length >=5;
     },
     contentClass() {
         if (!this.contentIsTouched) return '';
         return this.contentIsValid ? 'valid' : 'invalid';
     },
     contentErrorMessage() {
         return 'Enter at least 5 characters';
     }
 }
 

}
</script>

<style>
  input.valid {border: solid 1px green;}
  input.invalid {border: solid 1px red;}
  .form-snippers {
      border: 1px solid gray;
      border-radius: 5px;
      padding: 0.5em;
      margin: 0.2em;
  }
  input {
      width: 30%;
      padding: 0.5em;
      margin: 0.2em;
      border-radius: 5px;
  }
  .error, .contentError {
      color: red;
      
  }
  button {
      border: 1px soild green;
      border-radius: 5px;
      padding: 1em;
      
  }
button[disabled] { background-color: #ddd; border-color: #ccc; }
button[disabled]:hover { cursor: not-allowed; }


</style>