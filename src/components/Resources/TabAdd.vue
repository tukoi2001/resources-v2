<template>
 <div class="tab__add">
   <form @submit.prevent="submitCourse()">
       <div class="form__control">
           <label for="title">Title</label>
           <input type="text" name="title" id="title" ref="titleCourses">
       </div>
       <div class="form__control">
           <label for="description">Description</label>
           <textarea type="text" name="description" id="description" ref="descriptionCourses"></textarea>
       </div>
       <div class="form__control">
           <label for="link">Link</label>
           <input type="url" name="link" id="link" ref="linkCourses">
       </div>
       <div class="form__control">
           <button type="submit">Add Resource</button>
       </div>
   </form>
 </div>
<PopupValid v-if="showPopup" @myEvent="hidePopup"></PopupValid>   
</template>

<script>
import PopupValid from './PopupValid.vue';

export default {
  name: 'tabAdd',
  components: {
    PopupValid
    
  },
  inject: ['addCourse'],
  data() {
    return {
      showPopup: false,
    }
  },
  methods: {
      hidePopup(data) {
          console.log(data)
          if(data == 'false') {
              this.showPopup = false;
          }
          else {
               this.showPopup = true;
          }
      },
      submitCourse() {
            const title = this.$refs.titleCourses.value;
            const description = this.$refs.descriptionCourses.value;
            const link = this.$refs.linkCourses.value;
            
            if (title === '' || description === '' || link === '') {
                this.showPopup = true;
                return;
            }

            this.addCourse(title.trim(), description.trim(), link.trim());
      }
  }
}
</script>

<style scoped>
.tab__add {
    max-width: 40%;
    background-color: #FFF;
    margin: 0 auto;
    font-family: 'Roboto', sans-serif;
    box-shadow: 0 2px 8px rgba(0, 0 ,0 , 0.3);
    border-radius: 10px;
}
.tab__add form {
    padding: 1rem;
}
.form__control {
    margin: 1rem 0;
}
.form__control label {
    display: block;
    margin-bottom: 0.5rem;
    font-size: 1rem;
    font-weight: bold;
    font-family: inherit;
    color: #3a0061;
}
.form__control input, .form__control textarea {
    display: block;
    min-width: 98%;
    font: inherit;
    padding: 0.3rem;
    border: 1px solid #ccc;
    font-size: 1rem;
    border-radius: 5px;
}
.form__control textarea {
    min-height: 65px;
}
.form__control button {
    font-size: 1rem;
    padding: 0.75rem;
    font-family: inherit;
    color: #FFF;
    border: none;
    outline: none;
    cursor: pointer;
    border: 1px solid transparent;
    transition: all 0.5s;
    border-radius: 10px;
    background-color: #3a0061;
}
.form__control button:hover {
    background-color: #270041;
}
.form__control textarea:focus, .form__control input:focus {
    outline: none;
    border-color: #3a0061;
    background-color: #f7ebff;
}
</style>
