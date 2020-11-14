<template>
  <div class="container">
    <div class="generic-form">
      <div class="row justify-content-center">
        <div class="col-md-8">
          <div class="form-block">
            <form v-on:submit.prevent="onSubmit" v-show="form">
              <div class="form-group">
                <input
                  v-model.trim="$v.dataForm.firstName.$model"
                  type="text"
                  class="form-control"
                  placeholder="test"
                  @input="$v.dataForm.firstName.$touch"
                  :class="{ error: $v.dataForm.firstName.$error }"
                />
                <span class="placeholder-animation">firstName</span>
                <div v-if="$v.dataForm.firstName.$dirty" class="errors">
                  <span class="error" v-if="!$v.dataForm.firstName.regex"
                    >Name contain only character</span
                  >
                  <span class="error" v-if="!$v.dataForm.firstName.required"
                    >First name required</span
                  >
                </div>
              </div>
              <div class="form-group">
                <input
                  v-model.trim="$v.dataForm.LastName.$model"
                  type="text"
                  class="form-control"
                  placeholder="test"
                  @input="$v.dataForm.LastName.$touch"
                  :class="{ error: $v.dataForm.LastName.$error }"
                />
                <span class="placeholder-animation">Last name: </span>
                <div v-if="$v.dataForm.LastName.$dirty" class="errors">
                  <span class="error" v-if="!$v.dataForm.LastName.required"
                    >Last Name Required</span
                  >
                  <span class="error" v-if="!$v.dataForm.LastName.minLength"
                    >Last Name Required</span
                  >
                </div>
              </div>
              <div class="form-group">
                <input
                  v-model.trim="$v.dataForm.Email.$model"
                  type="email"
                  class="form-control"
                  placeholder="test"
                  @input="$v.dataForm.Email.$touch"
                  :class="{ error: $v.dataForm.Email.$error }"
                />
                <span class="placeholder-animation">Email: </span>
                <div v-if="$v.dataForm.Email.$dirty" class="errors">
                  <span class="error" v-if="!$v.dataForm.Email.required"
                    >Email Required</span
                  >
                  <span class="error" v-if="!$v.dataForm.Email.email"
                    >Email Invalid</span
                  >
                </div>
              </div>
              <div class="form-group">
                <input
                  v-model.trim="$v.dataForm.Password.$model"
                  type="password"
                  class="form-control"
                  placeholder="test"
                  @input="$v.dataForm.Password.$touch"
                  :class="{ error: $v.dataForm.Password.$error }"
                />
                <span class="placeholder-animation">Password: </span>
                <div v-if="$v.dataForm.Password.$dirty" class="errors">
                  <span class="error" v-if="!$v.dataForm.Password.required">
                    Password Required
                  </span>
                  <span class="error" v-if="!$v.dataForm.Password.minLength">
                    Password min length 8 character
                  </span>
                </div>
              </div>
              <div class="form-group">
                <input
                  v-model.trim="$v.dataForm.ConfirmPassword.$model"
                  type="password"
                  class="form-control"
                  placeholder="test"
                  @input="$v.dataForm.ConfirmPassword.$touch"
                  :class="{ error: $v.dataForm.ConfirmPassword.$error }"
                />
                <span class="placeholder-animation">Confirm Password: </span>
                <div v-if="$v.dataForm.ConfirmPassword.$dirty" class="errors">
                  <span
                    class="error"
                    v-if="!$v.dataForm.ConfirmPassword.sameAsPassword"
                    >Confirm Password NotMatched</span
                  >
                </div>
              </div>
              <div class="form-group">
                <textarea
                  v-model.trim="$v.dataForm.Message.$model"
                  type="number"
                  class="form-control"
                  placeholder="test"
                  @input="$v.dataForm.Message.$touch"
                  :class="{ error: $v.dataForm.Message.$error }"
                ></textarea>
                <span class="placeholder-animation">Message: </span>
                <div v-if="$v.dataForm.Message.$dirty" class="errors">
                  <span class="error" v-if="!$v.dataForm.Message.required"
                    >Message required</span
                  >
                  <span class="error" v-if="!$v.dataForm.Message.minLength"
                    >min lenght must be 50</span
                  >
                </div>
              </div>

              <div class="form-group">
                <select
                  class="form-select"
                  required
                  v-model="$v.dataForm.Select.$model"
                  @change="$v.dataForm.Select.$touch"
                  :class="{ error: $v.dataForm.Select.$error }"
                >
                  <option
                    v-for="op in dataForm.Options"
                    :value="op.val"
                    :key="op.id"
                    >{{ op.opt }}</option
                  >
                </select>
                <span class="placeholder-animation">Example select: </span>
                <div v-if="$v.dataForm.Select.$dirty" class="errors">
                  <span class="error" v-if="!$v.dataForm.Select.required"
                    >Message required</span
                  >
                </div>
              </div>
              <div class="check">
                <label for="">Gender</label>
                <div
                  class="form-check"
                  v-for="genders in dataForm.genderType"
                  :key="genders.id"
                >
                  <label class="form-check-label">
                    <input
                      class="form-check-input"
                      v-model.trim="$v.dataForm.Genders.$model"
                      @change="$v.dataForm.Genders.$touch"
                      type="radio"
                      :name="genders.type"
                      :value="genders.id"
                      checked
                    />
                    {{ genders.type }}
                  </label>
                </div>

                <div v-if="$v.dataForm.Genders.$dirty" class="errors">
                  <span class="error" v-if="!$v.dataForm.Genders.required"
                    >Gender Required.</span
                  >
                </div>
              </div>

              <div class="form-check check-box">
                <label class="form-check-label">
                  <input
                    class="form-check-input"
                    type="checkbox"
                    v-model.trim="$v.dataForm.Agree.$model"
                    @change="$v.dataForm.Agree.$touch"
                  />
                  Example checkbox
                </label>
              </div>
              <div v-if="$v.dataForm.Agree.$dirty" class="errors">
                <span class="error" v-if="!$v.dataForm.Agree.required"
                  >Gender Required.</span
                >
              </div>
              <div class="form-group">
                <vue-recaptcha
                  ref="recaptcha"
                  @verify="onVerify"
                  sitekey="6LdnhNsZAAAAAEm6A7LSelfjPfLy5kTda94m-6fY"
                  :loadRecaptchaScript="true"
                ></vue-recaptcha>
                <div v-if="isReCaptchaRequired" class="errors">
                  <span class="error">ReCaptcha Required</span>
                </div>
              </div>

              <div class="submit">
                <button
                  class="btn btn-primary btn-submit"
                  :disabled="$v.$invalid"
                >
                  Submit
                </button>
              </div>
            </form>

            <div class="success-msg" v-show="successMsg">
              <p class="msg-description">Form is submited successfully</p>
            </div>
            <div class="form-loader" v-show="loading">
              <img src="../assets/spinner.gif" />
            </div>
            <div class="toaster">Error message</div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
//npm install --save vue-recaptcha
import VueRecaptcha from "vue-recaptcha";
import { validationMixin } from "vuelidate";
import {
  required,
  minLength,
  email,
  sameAs,
  helpers
} from "vuelidate/lib/validators";

const ValidationName = helpers.regex(
  "alpha",
  /^([\u0621-\u064A/a-zA-Z_ ]){1,}$/
);

export default {
  name: "HelloWorld",
  components: { VueRecaptcha },
  mixins: [validationMixin],
  data() {
    return {
      form: true,
      dataForm: {
        firstName: "",
        LastName: "",
        Email: "",
        Message: "",
        Select: "",
        Options: [
          {
            val: 1,
            opt: "option1"
          },
          {
            val: 2,
            opt: "option2"
          },
          {
            val: 3,
            opt: "option3"
          },
          {
            val: 4,
            opt: "option4"
          }
        ],
        Password: "",
        ConfirmPassword: "",
        genderType: [
          {
            id: "option1",
            type: "male"
          },
          {
            id: "option2",
            type: "femal"
          }
        ],
        Agree: "",
        Genders: ""
      },
      loading: false,
      successMsg: false,
      isReCaptchaRequired: false,
      recapResponse: null
    };
  },
  validations: {
    dataForm: {
      firstName: {
        required,
        regex: ValidationName
      },
      LastName: {
        required,
        minLength: minLength(20)
      },
      Email: {
        required,
        email
      },
      Password: {
        required,
        minLength: minLength(8)
      },
      ConfirmPassword: {
        required,
        sameAsPassword: sameAs("Password")
      },
      Message: {
        required,
        minLength: minLength(50)
      },
      Select: {
        required
      },
      Genders: {
        required
      },
      Agree: {
        required
      }
    }
  },
  methods: {
    onSubmit() {
      this.$v.dataForm.$touch();

      if (this.$v.dataForm.$anyError) {
        console.log(this.$v.dataForm.$anyError);
        return;
      } else if (this.recapResponse == null) {
        this.isReCaptchaRequired = true;
        return;
      } else {
        this.form = false;
        this.loading = true;
        this.successMsg = true;
        this.loading = false;
      }
    },
    onVerify(response) {
      this.recapResponse = response;
      console.log("verify" + this.recapResponse);
      this.isReCaptchaRequired = false;
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
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
label {
  display: block;
  text-align: left;
}
.form-control,
.form-select {
  outline: none;
  box-shadow: none;
  height: unset;
}
.generic-form {
  margin: 50px;
  .check,
  .check-box {
    margin-bottom: 45px;
  }
  .form-group {
    position: relative;
    margin-bottom: 45px;

    input {
      height: unset;
    }
    textarea {
      resize: none;
    }
    input,
    textarea,
    .form-select {
      position: relative;
      outline: none;
      box-shadow: none;
      width: 100%;
      padding: 15px 20px;
      border: solid 1px #c1b6b6;
      background-color: transparent;
      font-size: 14px;
      border-radius: 0;
      &.error {
        border: 1px solid #eb7e7c;
      }
      &::placeholder {
        /* Chrome, Firefox, Opera, Safari 10.1+ */
        color: #fff;
        opacity: 1; /* Firefox */
      }

      &:-ms-input-placeholder {
        /* Internet Explorer 10-11 */
        color: #fff;
      }

      &::-ms-input-placeholder {
        /* Microsoft Edge */
        color: #fff;
      }
    }

    .placeholder-animation {
      font-size: 14px;
      font-weight: bold;
      position: absolute;
      color: #000;
      pointer-events: none;
      left: 15px;
      top: 13px;
      padding: 5px;
      background-color: #fff;
      -webkit-transition: 0.5s ease all;
      transition: 0.5s ease all;
    }

    input:focus + .placeholder-animation,
    input:not(:placeholder-shown) + .placeholder-animation,
    select:focus + .placeholder-animation,
    select:not(:focus):valid + .placeholder-animation,
    textarea:focus + .placeholder-animation,
    textarea:not(:placeholder-shown) + .placeholder-animation {
      top: -15px;
    }
  }
  .error {
    font-size: 11px;
    color: #eb7e7c;
  }
  .errors {
    float: left;
  }
  .submit {
    text-align: center;
    .btn-submit {
      width: 200px;
      padding: 5px 10px;
      border-radius: 0;
      margin: 0 auto;
      margin-top: 50px;
    }
  }

  .form-block {
    position: relative;
    .form-loader {
      position: absolute;
      top: 0;
      right: 0;
      width: 100%;
      height: 100%;
      display: flex;
      justify-content: center;
      align-items: center;
    }
    .toaster {
      font-size: 18px;
      padding: 10px;
      background-color: rgba(0, 0, 0, 0.8);
      border: 1px solid #fff;
      color: #ffffff;
      position: fixed;
      font-weight: normal;
      left: 10px;
      bottom: -85px;
      -webkit-transition: 0.5s;
      transition: 0.5s;
      z-index: 10;
    }
  }
}
</style>
