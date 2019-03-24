<template>
    <div>
        <form @submit.prevent="submit">
            <div class="form-step-one" v-show="step === 1">
                <input type="text" name="firstName" id="firstName" v-model.trim="$v.firstName.$model" class="form-control" :class="{ 'is-invalid': $v.firstName.$error }" />
                <div v-if="submitted && !$v.firstName.required" class="invalid-feedback">First Name is required</div>
                <input type="submit">
                {{$v.firstName}}

                <div class="navigation">
                    <button @click="nextStep()"></button>
                </div>
            </div>

            <div class="form-step-one" v-show="step === 2">
                <input type="text" name="firstName" id="firstName" v-model.trim="$v.firstName.$model" class="form-control" :class="{ 'is-invalid': $v.firstName.$error }" />
                <div v-if="submitted && !$v.firstName.required" class="invalid-feedback">First Name is required</div>
                <input type="submit">
                {{$v.firstName}}

                <div class="navigation">
                    <button @click="nextStep()"></button>
                </div>
            </div>

        </form>
    </div>
</template>

<script>
    import axios from 'axios'
    import Vue from 'vue'
    import { required, between } from "vuelidate/lib/validators"
    import Vuelidate from 'vuelidate'
    Vue.use(Vuelidate);

    export default {
        name: 'HelloWorld',
        props: {
            msg: String
        },
        data() {
            return {
                step: 1,
                firstName: '',
                submitted: false
            }
        },
        validations: {
            firstName: {
                required,
                between: between(20, 30)
            },

        },
        methods: {
            submit() {
                this.submitted = true;
                // this.$v.form.$touch();
                // console.log(this.validation)\
                if (this.$v.$invalid) {
                    return;
                }

                alert("SUCCESS!! :-)\n\n" + JSON.stringify(this.firstName));
            },
            nextStep() {
                this.step ++
            }
        },

        mounted() {
            axios
                .get('validation.json')
                .then(response => (this.validation = response))
                .catch(function (error) {
                    console.log(error)
                })
        }
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    h3 {
        margin: 40px 0 0;
    }

    ul {
        list-style-type: none;
        padding: 0;
    }

    li {
        display: inline-block;
        margin: 0 10px;
    }

    a {
        color: #42b983;
    }
</style>
