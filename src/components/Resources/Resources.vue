<template>
 <div class="wrapper">
    <button class="btn__submit" @click="changeTab('TabStore')" :class="{active: isActiveStore}"> Stored Resources</button>
    <button class="btn__submit" @click="changeTab('TabAdd')" :class="{active: isActiveAdd}"> Add Resources</button>
    <button class="btn__submit" @click="clearCourse()"> Delete All Resources</button>
 </div>
   <keep-alive>
    <component :is="currentTab" :resources="resources"></component>
  </keep-alive>
</template>

<script>
import TabAdd from './TabAdd.vue'
import TabStore from './TabStore.vue'


export default {
  name: 'resources',
  components: {
    TabAdd,
    TabStore
  },
  provide() {
      return {
          addCourse: this.addCourse,
          deleteCourse: this.handleDelete,
      }
  },
  data() {
      return {
          currentTab: 'TabStore',
          resources: [],
          isActive:  false,
      }
  },
  methods: {
      getLocalStorage(name) {
        return JSON.parse(localStorage.getItem(name))
    },
    setLocalStorage(name, data) {
      localStorage.setItem(name, JSON.stringify(data));
    },
    changeTab(tab) {
          this.currentTab = tab;
      },
    addCourse(title, description, link) {
        const newCourse = {title: title, description: description, link: link};
        this.resources.push(newCourse);
        this.setLocalStorage('resources', this.resources);
        this.resources = this.getLocalStorage('resources');
        this.currentTab = 'TabStore'
    },
    clearCourse() {
       if(this.resources.length) {
            this.resources = JSON.parse(localStorage.resources);
            this.resources.splice(0, this.resources.length);
       }
       else {
           alert('Please add course first!')
       }
    },
    handleDelete(index) {
        this.resources = JSON.parse(localStorage.resources);
        this.resources.splice(index, 1);
    }
  },
  computed: {
      isActiveStore() {
          if(this.currentTab == "TabStore") {
              return true;
          }
          else {
              return false;
          }
      },
      isActiveAdd() {
          if(this.currentTab == "TabAdd") {
              return true;
          }
          else {
              return false;
          }
      }
  },
   watch: {
      resources: {
          handler(newCourses) {
              localStorage.resources = JSON.stringify(newCourses);
          },
          deep: true
      }
  },
  mounted() {
       const resources = this.getLocalStorage('resources');
        if (resources.length) {
            this.resources = resources;
        } else {
             this.setLocalStorage('resources', []);
        } 
     }
}
</script>

<style scoped>
.wrapper {
    width: 40%;
    height: 80px;
    background-color: #FFF;
    margin: 30px auto;
    font-family: 'Roboto', sans-serif;
    border-radius: 10px;
    box-shadow: 0 2px 8px rgba(0, 0 ,0 , 0.3);
    display: flex;
    justify-content: space-between;
    align-items: center;
}
.btn__submit {
    font-size: 1rem;
    padding: 0.75rem;
    font-family: inherit;
    color: #3a0061;
    margin: 0 15px;
    border: none;
    outline: none;
    cursor: pointer;
    border: 1px solid transparent;
    transition: all 0.5s;
    border-radius: 10px;
    background-color: #FFF;
}
.btn__submit:hover {
    background-color: rgba(39, 0, 65, 0.5);
    border-color: #FFF;
}
.btn__submit:focus:not(:last-child) {
    background-color: #3a0061;
    color: #FFF;
    border-color: #270041;
}
.active {
    background-color: rgba(39, 0, 65, 1);
    color: #FFF;
    border-color: #FFF;
}
</style>
