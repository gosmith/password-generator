<template>
  <div
    class="
      uk-card
      uk-card-default
      uk-margin-left
      uk-margin-medium-top
      uk-margin-medium-bottom
    "
  >
    <div class="uk-card-header">
      <h3 class="uk-card-title">Options PwdGen</h3>
    </div>
    <div class="uk-card-body">
      <div class="uk-margin-remove">
        <div class="uk-inline">
          <span class="uk-form-icon uk-form-icon-flip" uk-icon="icon: copy">
            {{ generatedPassword }}
          </span>
        </div>
      </div>
      <div class="setting" v-if="!isLoading">
        <label for="">Password Length</label>
        <input
          v-model="passwordLength"
          class="uk-input uk-width-1-4@m"
          type="number"
          min="1"
          max="30"
        />
      </div>
      <div class="uk-margin">
        <div class="uk-form-controls">
          <div class="uk-flex uk-flex-column">
            <div class="setting uk-margin-remove">
              <label for="">Include Uppercase Character</label>
              <input
                v-model="includeUpperCase"
                class="checkbox"
                type="checkbox"
              />
            </div>
            <div class="setting uk-margin-remove">
              <label for="">Include Number Character</label>
              <input v-model="includeNumber" class="checkbox" type="checkbox" />
            </div>
            <div class="setting uk-margin-remove">
              <label for="">Include Symbol Character</label>
              <input v-model="includeSymbol" class="checkbox" type="checkbox" />
            </div>
          </div>
        </div>
      </div>
      <button
        class="uk-button uk-button-default uk-align-right"
        @click="generatePassword()"
      >
        Generate Password
      </button>
    </div>
  </div>
</template>

<script>
export default {
  data: () => ({
    isLoading: false,
    generatedPassword: 'SelectChoices+Generate',
    passwordLength: 20,
    includeUpperCase: false,
    includeNumber: false,
    includeSymbol: false,
  }),
  methods: {
    generatePassword() {
      if (!this.passwordLength) return
      this.triggerLoading(true)
      let password = ''
      let characters = 'abcdefghijklmnopqrstuvwxyz'
      if (this.includeUpperCase) characters += 'ABCDEFGHIJKLMNOPQRSTUVWXYZ'
      if (this.includeNumber) characters += '0123456789'
      if (this.includeSymbol) characters += '!"#$%&\'()*+,-./:;<=>?@[\\]^_`{|}~'
      for (let i = 0; i < this.passwordLength; i++) {
        password += characters.charAt(
          Math.floor(Math.random() * characters.length)
        )
      }
      this.generatedPassword = password
      navigator.clipboard.writeText(password)
      this.triggerLoading(false)
    },
    triggerLoading(state) {
      this.isLoading = state
    },
  },
}
</script>

<style scoped>
.password {
  overflow-wrap: break-word;
}
</style>
