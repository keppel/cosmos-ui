<template lang="pug">
#app
  app-header
  #app-content
    #app-main: router-view
    app-footer
  notifications(:notifications='notifications' theme='cosmos')
</template>

<script>
import { mapGetters } from 'vuex'
import AppFooter from './components/common/AppFooter'
import AppHeader from './components/common/AppHeader'
import Notifications from '@nylira/vue-notifications'
import store from './vuex/store'
export default {
  name: 'app',
  components: {
    AppHeader,
    AppFooter,
    Notifications
  },
  computed: {
    ...mapGetters(['notifications'])
  },
  store
}
</script>

<style lang="stylus" src="./styles/app.styl"></style>
