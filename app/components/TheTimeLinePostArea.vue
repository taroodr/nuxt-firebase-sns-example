<template lang="html">
  <div class="field-wrapper">
    <form class="field is-grouped" @submit.prevent="doPost">
      <p class="control is-expanded">
        <input
          class="input"
          type="text"
          placeholder="What's happening?"
          v-model="body"
        />
      </p>
      <p class="control">
        <button class="button is-primary" :disabled="!this.body">Post</button>
      </p>
    </form>
  </div>
</template>

<script>
import { mapGetters } from 'vuex'

export default {
  data() {
    return {
      body: ''
    }
  },
  computed: {
    ...mapGetters(['user'])
  },
  methods: {
    async doPost() {
      if (!this.body) return
      await this.$store.dispatch('ADD_POST', {
        email: this.user.email,
        body: this.body
      })
      this.body = ''
    }
  }
}
</script>

<style scoped>
.field-wrapper {
  position: sticky;
  top: 0;
  z-index: 10;
  border-top: solid 32px #fafafa;
}

.field {
  margin-bottom: 16px;
  padding: 16px;
  background: #fff;
  border: solid 1px #e6e6e6;
}

.button.is-primary {
  background: #1da1f2;
}
</style>
