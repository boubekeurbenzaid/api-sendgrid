<!-- Contact form -->
<template>
  <div class="contact-form">
    <!-- form -->
    <form>
      <div class="identite">
        <!-- first name -->
        <div>
          <input
            type="text"
            name="firstName"
            id="firstName"
            class="field-required field"
            v-model="firstName"
            pattern="[a-zA-Z \-]{3,}"
            placeholder="First name *"
            required
          />
          <span class="error-text error-fn">Veuillez remplir ce champs</span>
        </div>
        <!-- last name -->
        <div>
          <input
            type="text"
            name="lastName"
            id="lastName"
            class="field-required field"
            v-model="lastName"
            pattern="[a-zA-Z \-]{3,}"
            placeholder="Last name *"
            required
          />
          <span class="error-text error-ln">Veuillez remplir ce champs</span>
        </div>
      </div>
      <div class="coordonnees">
        <!-- email adress -->
        <div>
          <input
            name="emailAdress"
            id="emailAdress"
            class="field-required field"
            v-model="emailAddress"
            pattern="[a-zA-Z0-9.\-_]+[@]{1}[a-zA-Z0-9]+[.]{1}[a-z]{2,5}"
            placeholder="myadress@mail.com *"
            required
          />
          <span class="error-text error-ea">Veuillez remplir ce champs</span>
        </div>
        <!-- phone number -->
        <input
          type="tel"
          name="phone"
          id="phone"
          class="field"
          v-model="phone"
          maxlength="11"
          pattern="[0-9]{10,11}"
          placeholder="phone number *"
        />
      </div>
      <div class="compagnie">
        <!-- company -->
        <input
          type="text"
          name="company"
          id="company"
          class="field"
          v-model="company"
          placeholder="Company"
        />
      </div>
      <div class="sujet">
        <!-- subject -->
        <div>
          <input
            type="text"
            name="subject"
            id="subject"
            class="field-required field"
            v-model="subject"
            pattern="[a-zA-Z0-9 \-_'(éèçà)ù!:.,?%]{0,}"
            placeholder="Subject *"
            required
          />
          <span class="error-text error-s">Veuillez remplir ce champs</span>
        </div>
      </div>
      <div class="message">
        <!-- message -->
        <div>
          <textarea
            name="message"
            id="message"
            class="field-required field"
            v-model="message"
            rows="10"
            cols="57"
            placeholder="Message *"
            wrap="hard"
            required
          />
          <span class="error-text error-m">Veuillez remplir ce champs</span>
        </div>
      </div>
      <div class="valider">
        <!-- submit -->
        <input
          type="submit"
          id="submit"
          value="Submit"
          @click.prevent="sendMail"
        />
      </div>
    </form>
  </div>
</template>

<script>
export default {
  name: 'Contact',
  data() {
    return {
      firstName: '',
      lastName: '',
      emailAddress: '',
      phone: '',
      company: '',
      subject: '',
      message: '',
    }
  },
  methods: {
    // send email with contact form
    sendMail() {
      // All input fields selectors
      const inputField = document.querySelectorAll('.field')
      // All input fields required selectors
      const inputFieldRequired = document.querySelectorAll('.field-required')
      // All error text selectors
      const errorText = document.querySelectorAll('.error-text')

      // loop
      let error = false
      for (let i = 0; i < inputFieldRequired.length; i++) {
        if (inputFieldRequired[i].value === '') {
          errorText[i].style.display = 'block'
          errorText[i].style.position = 'absolute'
          errorText[i].style.color = '#ff0000'
          error = true
        } else {
          errorText[i].style.display = 'none'
        }
      }

      if (!error) {
        try {
          // send email method
          this.$mail.send({
            from: this.emailAddress,
            subject: this.subject,
            html: `First name : ${this.firstName}<br/>
            Last name : ${this.lastName}<br/>
            Email address : ${this.emailAddress}<br/>
            Phone number : ${this.phone}<br/>
            Compagny : ${this.company}<br/>
            Message : ${this.message}<br/> `,
          })
          alert(`Your message sent to ${process.env.MAILTO} !`)
          for (let i = 0; i < inputField.length; i++) {
            inputField[i].value = ''
          }
        } catch (e) {
          console.error(e)
        }
      }
    },
  },
}
</script>

<style scoped>
.contact-form {
  display: flex;
  justify-content: center;
  align-items: center;
  padding-bottom: 3rem;
}
.identite,
.coordonnees {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
form div input,
form div textarea {
  margin-bottom: 2rem;
  padding: 0.5rem 1rem;
  color: #fff;
  background-color: #383e51;
  border: 1px solid #fff;
  border-radius: 3px;
  outline: none;
}
form div input:focus:invalid,
form div textarea:focus:invalid {
  border-color: #ff0000;
}
form div input:valid,
form div textarea:valid {
  border-color: #56c93f;
}
input[name='phone']:valid {
  border-color: #fff;
}
input[name='company']:valid {
  border-color: #fff;
}
form div input:focus:valid,
form div textarea:focus:valid {
  border-color: #56c93f;
}
input[name='phone']:focus:valid {
  border-color: #fff;
}
input[name='company']:focus:valid {
  border-color: #fff;
}
textarea {
  resize: none;
}
#submit {
  padding: 0.5rem 3rem;
  font-size: 16px;
  color: #fff;
  background-color: #01a2a6;
  border: 1px solid #01a2a6;
  border-radius: 30px;
  float: right;
  cursor: pointer;
}
#submit:hover {
  background-color: #01a3a691;
  border: 1px solid #01a3a691;
}
.error-text {
  display: none;
  margin-top: -2rem;
  font-size: 12px;
}
</style>
