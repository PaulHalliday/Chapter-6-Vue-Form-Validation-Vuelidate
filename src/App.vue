<template>
  <div>
    <form class="form" @submit.prevent="onSubmit">
      <div class="input">
        <label for="email">Email</label>
        <input 
        :class="{ error: $v.email.$error }"
        type="email" 
        id="email" 
        @input="$v.email.$touch()"
        v-model.trim="email">
        <p class="error-message"  v-if="!$v.email.email">Please enter a valid email address.</p>
        <error-field-required :isRequired="!$v.email.required" name="Email" />
      </div>
      <div class="input"> 
        <label for="firstName">First Name</label>
        <input 
        :class="{ error: $v.firstName.$error }"
        type="text"
        id="firstName" 
        v-model.trim="firstName"
        @input="$v.firstName.$touch()">
        <error-field-required :isRequired="!$v.firstName.required" name="First Name" />
      </div>
      <div class="input">
        <label for="lastName">Last Name</label>
        <input 
        :class="{ error: $v.lastName.$error}"
        type="text" 
        id="lastName" 
        v-model.trim="lastName"
        @input="$v.lastName.$touch()">
        <error-field-required :isRequired="!$v.lastName.required" name="Last Name" />
      </div>
      <div class="input">
        <label for="password">Password</label>
        <input 
        :class="{ error: $v.password.$error }"
        type="password" 
        id="password" 
        v-model.trim="password"
        @input="$v.password.$touch()">
        <error-field-required :isRequired="!$v.password.required" name="Password" />
      </div>
      <div class="input">
        <label for="password">Repeat Password</label>
        <input 
        :class="{ error: $v.repeatPassword.$error }"
        type="password" 
        id="password" 
        v-model.trim="repeatPassword"
        @input="$v.repeatPassword.$touch()">

        <p class="error-message"  v-if="!$v.repeatPassword.sameAsPassword">Passwords must be identical.</p>
        <error-field-required :isRequired="!$v.repeatPassword.required" name="Password" />
      </div>
      <button type="submit">Submit</button>
    </form>
    <div class="validators">
      <pre>{{$v}}</pre>
    </div>
  </div>

</template>

<script>
import { required, email, minLength, sameAs } from 'vuelidate/lib/validators';

import Required from './components/Required';

export default {
  components: {
    errorFieldRequired: Required,
  },
  data() {
    return {
      email: '',
      password: '',
      repeatPassword: '',
      firstName: '',
      lastName: '',
    };
  },
  validations: {
    email: {
      required,
      email,
    },
    firstName: {
      required,
    },
    lastName: {
      required,
    },
    password: {
      required,
      minLength: minLength(6),
    },
    repeatPassword: {
      sameAsPassword: sameAs('password'),
    },
  },
  methods: {
    onSubmit() {},
  },
};
</script>

<style>
.form {
  display: inline-block;
  text-align: center;
  width: 49%;
}
.validators {
  display: inline-block;
  width: 49%;
  text-align: center;
  vertical-align: top;
}
.input {
  padding: 5px;
}
input:focus {
  outline: none;
}
.error {
  border: 1px solid red;
}
.error-message {
  color: red;
}
</style>
