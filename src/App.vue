<template>
  <div id="visa">
    <h1>Create a New Vue Account</h1>
    <form>
 <div>
    <!-- Full name -->
  <div class="form-group" :class="{ 'form-group--error': $v.name.$error }">
    <label class="form__label">Full Name</label>
    <input class="form__input" v-model.trim="$v.name.$model"/>
  </div>
  <span class="error" v-if="!$v.name.required">Field is required</span>
  <span class="error" v-if="!$v.name.minLength">Name must have at least {{$v.name.$params.minLength.min}} letters.</span>
  <tree-view :data="$v.name" :options="{rootObjectKey: '$v.name', maxDepth: 2}"></tree-view>
      <!-- Email Address -->
  <label for="email">Email Address</label>
      <input type="text"> <br>
      <span></span>
      <!-- Password -->
  <div class="form-group" :class="{ 'form-group--error': $v.password.$error }">
    <label class="form__label">Password</label>
    <input class="form__input" v-model.trim="$v.password.$model"/>
  </div>
  <span class="error" v-if="!$v.password.required">Field is required</span>
  <span class="error" v-if="!$v.password.minLength">Name must have at least {{$v.password.$params.minLength.min}} letters.</span>
  <tree-view :data="$v.password" :options="{rootObjectKey: '$v.password', maxDepth: 2}"></tree-view>
      <!-- Age -->
  <div class="form-group" :class="{ 'form-group--error': $v.age.$error }">
    <label class="form__label">Age</label>
    <input class="form__input" v-model.trim="$v.age.$model"/>
  </div>
  <span class="error" v-if="!$v.age.between">Must be between {{$v.age.$params.between.min}} and {{$v.age.$params.between.max}}</span>
  <tree-view :data="$v.age" :options="{rootObjectKey: '$v.age', maxDepth: 2}"></tree-view>
</div>
      
    </form>

  </div>
</template>

<script>
import { required, minLength, between } from 'vuelidate/lib/validators'
export default {
  name: 'app',
  data() {
    return {
      name: '',
      password: '',
      age:''
    }
  },
  validations: {
    name: {
      required,
      minLength: minLength(4)
    },
    password: {
      required,
      minLength: minLength(4)
    }, 
    age: {
      required,
      between: between(18,45)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#visa {
  margin: 20px auto;
  max-width: 700px;
  margin-bottom: 28px;
}
label{
  display: block;
  margin: 20px 0 10px;
}
span {
  padding-top: 0px;
  margin-top: 0px;
  font-size: 12px;
  color: red;
}
input {
  font-size: 30px;
  border: 1px double rgb(102, 97, 96) ;
  border-radius: 4px;
}

</style>
