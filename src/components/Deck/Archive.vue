<template lang='pug'>

#archive(v-if="$store.getters.member")
    .row.shipwrapper
        .shipbackground
        .four.columns(v-if='$store.getters.inbox.length > 0')
        .columns(:class='{eight: $store.getters.inbox.length > 0}')
            h3 {{$store.getters.member.name}} Archive
            panels(:c='$store.getters.recurasaurus')

</template>

<script>

import Panels from './Panels'

export default {
  components:{
      Panels,
  },
}

</script>

<style lang="stylus" scoped>

@import '../../styles/colours'
@import '../../styles/skeleton'
@import '../../styles/button'

#archive
    width: 100%

.floater
    position: relative;
    top: 0
    left: 0
    width: 100%
    min-height: 500px

.shipwrapper
    position: relative

.shipbackground
    background-image: url('../../assets/images/sunken_ship.png')
    background-repeat: no-repeat
    background-position: center center
    background-size: contain
    opacity: 0.2
    top: 0
    left: 0
    bottom: 0
    right: 0
    position: absolute
    z-index: -1
    width: 100%
    height: 100%
    min-height: 99vh

</style>
