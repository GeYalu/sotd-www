<template>
<div class="component-DappDetailBodyContentRank">
  <div class="wrapper">
    <p class="description">
      <strong>Platform</strong> 
      &nbsp;
      <nuxt-link
        @click.native="trackPlatform(platform)"
        :to="{
          name: 'rankings-platform',
          params: {
            platform: platform.toLowerCase()},
            query: {
              reload: 'true'
            }
          }">{{ platform }}</nuxt-link>
    </p>
  </div>
</div>
</template>

<script>
import { trackDappPlatform } from '~/helpers/mixpanel'

export default {
  props: ['platform', 'slug'],
  methods: {
    trackPlatform (platform) {
      const action = trackDappPlatform(platform, this.slug)
      this.$mixpanel.track(action.name, action.data)
    }
  }
}
</script>


<style lang="scss" scoped>
@import '~assets/css/settings';

.description {
  margin-bottom: 0;
  text-align: center;
  @include tweakpoint('min-width', 1000px) {
    text-align: left;
  }
}

.wrapper {
  margin: 0 10px 24px 10px;
  padding-bottom: 24px;
  border-bottom: 1px solid darken($color--gray, 6%);
}
</style>
