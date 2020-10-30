<template>
    <div class="card">
        <h3 class="card-header text-center">Register Area</h3>
        <div class="card-body">
            <form @submit.prevent="submitForm">
                <div class="form-row">
                    <div class="form-group ">
                        <label>First name</label>
                        <input 
                            type="text" 
                            class="form-control" 
                            v-model.trim="$v.firstname.$model"
                            :class="{
                                'is-invalid': $v.firstname.$error, 'is-valid': !$v.firstname.$invalid
                            }"
                        >
                        <div class="valid-feedback">Your first name is valid!</div>
                        <div class="invalid-feedback">
                            <span v-if="!$v.firstname.required">First name is required</span>
                            <span v-if="!$v.firstname.minLength">First name must have at least 
                                {{$v.firstname.$params.minLength.min}} letters
                            </span>
                            <span v-if="!$v.firstname.maxLength">First name must have at most 
                                {{$v.firstname.$params.maxLength.max}} letters
                            </span>
                        </div>
                    </div>
                    <div class="form-group ">
                        <label>Last name</label>
                        <input 
                            type="text" 
                            class="form-control" 
                            v-model.trim="$v.lastname.$model" 
                            :class="{
                                'is-invalid': $v.lastname.$error, 'is-valid': !$v.lastname.$invalid
                            }"
                        >
                        <div class="valid-feedback">Your last name is valid!</div>
                        <div class="invalid-feedback">
                            <span v-if="!$v.lastname.required">last name is required</span>
                            <span v-if="!$v.lastname.minLength">last name must have at least 
                                {{$v.lastname.$params.minLength.min}} letters
                            </span>
                            <span v-if="!$v.lastname.maxLength">last name must have at most 
                                {{$v.lastname.$params.maxLength.max}} letters
                            </span>
                        </div>
                    </div>
                    <div class="form-group">
                        <label>username</label>
                        <input 
                            type="text" 
                            class="form-control" 
                            v-model.trim="$v.username.$model" 
                            :class="{
                                'is-invalid': $v.username.$error, 'is-valid': !$v.username.$invalid
                            }"
                        >
                        <div class="valid-feedback">Your username is valid!</div>
                        <div class="invalid-feedback">
                            <span v-if="!$v.username.required">Username is required</span>
                            <span v-if="!$v.username.isUnique">Username is already registered</span>
                        </div>
                    </div>
                    <div class="form-group">
                        <label>Email</label>
                        <input 
                            type="email" 
                            class="form-control" 
                            v-model.trim="$v.email.$model" 
                            :class="{
                                'is-invalid': $v.email.$error, 'is-valid': !$v.email.$invalid
                            }"
                        >
                        <div class="valid-feedback">Your email is valid!</div>
                        <div class="invalid-feedback">
                            <span v-if="!$v.email.required">Email is required</span>
                            <span v-if="!$v.email.isUnique">Email is already registered</span>
                        </div>
                    </div>
                    <div class="form-group">
                        <label>password</label>
                        <input 
                            type="password"
                            id="password" 
                            class="form-control" 
                            v-model.trim="$v.password.$model" 
                            :class="{
                                'is-invalid': $v.password.$error, 'is-valid': !$v.password.$invalid
                            }"
                        >
                        <div class="valid-feedback">Your password is valid!</div>
                        <div class="invalid-feedback">
                            <span v-if="!$v.password.required">Password is required</span>
                            <span v-if="!$v.password.minLength">
                                {{$v.password.$params.minLength.min}}
                                characters minimum
                            </span>
                        </div>
                    </div>
                    <div class="form group form-check">
                        <input 
                            type="checkbox" 
                            id="showpassword" 
                            class="form-check input" 
                            @click="toggleShowpassword"
                            v-model="showpassword"
                        >
                        <label class="form-check-label" for="showpassword">Show password</label>
                    </div>
                    <div class="form-group">
                        <label>Repeat password</label>
                        <input 
                            type="password"
                            id="password" 
                            class="form-control" 
                            v-model.trim="$v.repeatpassword.$model" 
                            :class="{
                                'is-invalid': $v.repeatpassword.$error, 'is-valid': (password != '') ? 
                                !$v.repeatpassword.$invalid : ''
                            }"
                        />
                        <div class="valid-feedback">Your password is identical!</div>
                        <div class="invalid-feedback">
                            <span v-if="!$v.repeatpassword.sameAspassword">
                                Password must be identical
                            </span>
                        </div>
                    </div>
                    <div class="form-group">
                        <label>Phone Number</label>
                        <input 
                            type="number" 
                            class="form-control" 
                            v-model.number.lazy="$v.phone.$model" 
                            :class="{
                                'is-invalid': $v.phone.$error, 'is-valid':!$v.phone.$invalid 
                            }"
                        />
                        <div class="valid-feedback">Your phone number is valid</div>
                        <div class="invalid-feedback">
                            <span v-if="!$v.phone.required">Phone number is required</span>
                            <span v-if="!$v.phone.numeric">This phone number only numeric accepted</span>
                        </div>
                    </div>
                    <div class="form-group">
                        <label>Web Site</label>
                        <input 
                            type="url" 
                            class="form-control" 
                            v-model.trim="$v.url.$model" 
                            :class="{
                                'is-invalid': $v.url.$error, 'is-valid':!$v.url.$invalid 
                            }"
                        />
                        <div class="valid-feedback">Your website is valid</div>
                        <div class="invalid-feedback">
                            <span v-if="!$v.url.required">Url is required</span>
                            <span v-if="!$v.url.url">This website is invalid </span>
                        </div>
                    </div>
                </div>
                <button type="submit" class="btn btn-success">
                    Submit {{submitstatus}}
                </button>
            </form>
        </div>
    </div>
</template>

<script>
import {required, minLength, maxLength, email, sameAs, numeric, url } from 'vuelidate/lib/validators'
export default {
    name: "FormValidation",
    data() {
        return {
            firstname: "",
            lastname: "",
            username: "",
            email: "",
            password: "",
            repeatpassword: "",
            showpassword: false,
            phone: "",
            url: "",
            submitstatus: null
        }
    },
    validations: {
        firstname: {
            required,
            minLength: minLength(3),
            maxLength: maxLength(10),
        },

        lastname: {
            required,
            minLength: minLength(5),
            maxLength: maxLength(12)
        },

        username: {
            required,
            isUnique(value) {
                if(value === "") {
                    return true
                }
                return new Promise((resolve) => {
                    setTimeout(() => {
                        resolve(typeof value === "string" && value.length % 2 !==0 )
                    }, 350 + Math.random() * 300)
                })
            }
        },

        email: {
            required,
            email,
            isUnique(value) {
                if(value === "") {
                    return true
                }

                return new Promise((resolve) => {
                    setTimeout(() => {
                        resolve(typeof value === "string" && value.length % 2 !==0 )
                    }, 350 + Math.random() * 300)
                })
            }
        },

        password: {
            required,
            minLength: minLength(8)
        },

        repeatpassword: {
            sameAspassword: sameAs('password')
        },
        phone: {
            required,
            numeric,
            minLength: minLength(12)
        },
        url: {
            required,
            url
        }
    },
    methods: {
        toggleShowpassword() {
            var show = document.getElementById('password')
            if(this.showpassword == false) {
                this.showpassword = true
                show.type = "text"
            } else {
                this.showpassword = false
                show.type = "password"
            }
        },
        submitForm() {
            this.$v.$touch()
            if(this.$v.$invalid) {
                this.submitstatus = "FAIL"
            } else {
                this.submitstatus = "SUCCESS"
            }
        }
    }
}
</script>    

<style scoped>
    label {
        padding: 5px;
    }
    .card {

    }
    .card-body {
        display: flex;
        flex-direction: column;

    }
    .form-row {
        display:flex;
        flex-direction: column;
    }
    .form-group {
        display: flex;
        flex-direction: column;
        padding: 5px;
    }
    .form-group input {
        font-size: 25px;
    }
    .valid-feedback {
        color: green;
    }
    

</style>