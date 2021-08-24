<template>
  <div
    class="
      uk-card
      uk-card-default
      uk-margin
      uk-margin-medium-top
      uk-margin-medium-bottom
    "
  >
    <div class="uk-card-header">
      <h3 class="uk-card-title">Composition PwdGen</h3>
    </div>

    <div class="uk-card-body">
      <div class="uk-margin-remove">
        <div class="uk-inline">
          <span class="uk-form-icon uk-form-icon-flip" uk-icon="icon: copy">
            <p>{{ generatedPassword }}</p>
          </span>
        </div>
      </div>

      <div class="setting">
        <label>Password length</label>
        <input
          class="uk-input uk-width-1-4@m"
          v-model="passwordLength"
          type="number"
          id="length"
          min="4"
          max="20"
        />
      </div>
      <div class="uk-margin">
        <div class="uk-form-controls">
          <div class="uk-flex uk-flex-column">
            <div class="setting uk-margin-remove">
              <label> Include Uppercase Character</label>
              <input
                class="checkbox"
                v-model="includeUpperCase"
                type="checkbox"
              />
            </div>
            <div class="setting uk-margin-remove">
              <label> Include Number Character</label>
              <input class="checkbox" v-model="includeNumber" type="checkbox" />
            </div>
            <div class="setting uk-margin-remove">
              <label> Include Symbol Character</label>
              <input class="checkbox" v-model="includeSymbol" type="checkbox" />
            </div>
          </div>
        </div>
      </div>
      <button
        class="uk-button uk-button-default uk-align-right"
        @click="generatePassword()"
      >
        Generate password
      </button>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue'

export default {
  setup() {
    const passwordLength = ref(20)
    const includeUpperCase = ref(false)
    const includeNumber = ref(false)
    const includeSymbol = ref(false)
    const generatedPassword = ref('SelectChoices+Generate')

    const clipboard = ref('')

    const generatePassword = () => {
      let password = ''
      let characters = 'abcdefghijklmnopqrstuvwxyz'
      if (includeUpperCase.value) characters += 'ABCDEFGHIJKLMNOPQRSTUVWXYZ'
      if (includeNumber.value) characters += '0123456789'
      if (includeSymbol.value) characters += '!@#$%^&*(){}[]=<>/,.'

      for (let i = 0; i < passwordLength.value; i++) {
        password += characters.charAt(
          Math.floor(Math.random() * characters.length)
        )
        navigator.clipboard.writeText(password)
      }
      generatedPassword.value = password
    }

    return {
      passwordLength,
      includeUpperCase,
      includeNumber,
      includeSymbol,
      clipboard,
      generatePassword,
      generatedPassword,
    }
  },
}
</script>
