<template lang="pug">
page(title='Validators')
  modal-search(v-if="filters.validators.search.visible" type="validators")
  tab-bar
    router-link(to="/validators" exact) Online ({{ online }})
    a Offline (0)
  tool-bar
    a(@click='setSearch(true)'): i.material-icons search
  list-item(
    v-for="i in filteredValidators"
    icon='storage'
    :key="i.node_info.moniker"
    :subtitle="TODOAtoms"
    :title="i.node_info.moniker"
    :to="`/validators/${urlsafeIp(i.node_info.moniker)}`")
</template>

<script>
import { mapGetters } from 'vuex'
import { includes, orderBy } from 'lodash'
import Mousetrap from 'mousetrap'
import ListItem from '../common/NiListItem'
import ModalSearch from '../common/ModalSearch'
import Page from '../common/NiPage'
import TabBar from '../common/NiTabBar'
import ToolBar from '../common/NiToolBar'
export default {
  name: 'page-validators',
  components: {
    ListItem,
    ModalSearch,
    Page,
    TabBar,
    ToolBar
  },
  computed: {
    ...mapGetters(['validators', 'filters']),
    filteredValidators () {
      let query = this.filters.validators.search.query
      let list = orderBy(this.validators, ['node_info.moniker', 'desc'])
      if (this.filters.validators.search.visible) {
        return list.filter(i => includes(i.node_info.moniker, query))
      } else {
        return list
      }
    },
    online () { return this.validators.length }
  },
  data: () => ({
    TODOAtoms: '13.37M ATOM'
  }),
  methods: {
    setSearch (bool) { this.$store.commit('setSearchVisible', ['validators', bool]) },
    urlsafeIp (ip) { return ip.split('.').join('-') }
  },
  mounted () {
    Mousetrap.bind(['command+f', 'ctrl+f'], () => this.setSearch(true))
    Mousetrap.bind('esc', () => this.setSearch(false))
  }
}
</script>
