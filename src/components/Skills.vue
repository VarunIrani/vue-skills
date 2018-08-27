<template>
  <div class="hello">
    <div class="holder">
      <!-- Form validation using vee-validate -->
      <form @submit.prevent="addSkill">
        <input type="text" placeholder="Enter a skill that you have.." v-model="skill" v-validate="'min:5'" name="skill"/>
        <!-- Animation for error message: Using transition-->
        <transition name="alert-in" enter-active-class="animated flipInX" leave-active-class="animated flipOutX">
          <p class="alert" v-if="errors.has('skill')">{{errors.first('skill')}}</p>
        </transition>
      </form>
      
      <ul>
        <!-- Animating List Elements: Using transition-group -->
        <transition-group name="list" enter-active-class="animated bounceInUp" leave-active-class="animated bounceOutDown">
          <li v-for="(data, index) in skills" :key="index">
            {{data.skill}}
            <!-- Used to remove skill -->
            <i class="fa fa-minus-circle" @click="remove(index)"></i>
          </li>
        </transition-group>
      </ul>
      <!-- Vue Conditional Templating -->
      <p v-if="skills.length == 0">You currently do not have any skill</p>
      <p v-else>These are the skills that you possess.</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "Skills",
  data() {
    return {
      skill: "",
      skills: [{ skill: "Vue.js" }, { skill: "Frontend Developer" }]
    };
  },
  methods: {
    addSkill() {
      this.$validator.validateAll().then(result => {
        if (result) {
          // Submit only if valid
          this.skills.push({ skill: this.skill });
          this.skill = "";
        } else {
          // Otherwise Console Log Error
          console.error("Not Valid");
        }
      });
    },
    remove(id) {
      this.skills.splice(id, 1);
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@import url("https://cdnjs.cloudflare.com/ajax/libs/animate.css/3.7.0/animate.css");
@import url("https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.min.css");

.holder {
  background: white;
}
ul {
  margin: 0;
  list-style-type: none;
  padding: 0;
}

ul li {
  padding: 20px;
  font-size: 1.3em;
  background-color: #e0edf4;
  border-left: 5px solid #3eb3f6;
  margin-bottom: 3px;
}

p {
  text-align: center;
  padding: 30px 0;
  color: grey;
}

.container {
  box-shadow: 0 0 40px lightgray;
}

input {
  width: calc(100% - 40px);
  border: 0;
  padding: 20px;
  font-size: 1.3em;
  background-color: #323333;
  color: #687f7f;
}

.alert {
  background: #fdf2ce;
  font-weight: bold;
  display: inline-block;
  padding: 5px;
  margin-top: -20px;
}

/* .alert-in-enter-active {
  animation: bounce-in 0.5s;
}
.alert-in-leave-active {
  animation: bounce-in 0.5s reverse;
}

@keyframes bounce-in {
  0% {
    transform: scale(0);
  }
  50% {
    transform: scale(1.5);
  }
  100% {
    transform: scale(1);
  }
} */

i {
  float: right;
  cursor: pointer;
}
</style>
