<template>
  <section class="app-main" :style="!sidebar.hide ? 'height: calc(100vh - 105px)': 'height: calc(100vh - 65px)'">
    <router-view v-slot="{ Component, route }">
      <transition name="fade-transform" mode="out-in">
        <keep-alive :include="tagsViewStore.cachedViews">
          <component v-if="!route.meta.link" :is="Component" :key="route.path"/>
        </keep-alive>
      </transition>
    </router-view>
    <iframe-toggle />
  </section>
</template>

<script setup>
import iframeToggle from "./IframeToggle/index"
import useTagsViewStore from '@/store/modules/tagsView'
import useAppStore from '@/store/modules/app'

const sidebar = computed(() => useAppStore().sidebar);
const tagsViewStore = useTagsViewStore()
</script>

<style lang="scss" scoped>
.app-main {
  /* 50= navbar  50  */
//   min-height: calc(100vh - 105px);
//   width: 100%;
//   position: relative;
//   overflow: hidden;
  height: calc(100vh - 105px);
  width: 100%;
  position: relative;
  overflow-x: hidden;
  overflow-y: auto;
}

.fixed-header + .app-main {
//   padding-top: 50px;
  padding-top: 105px;
    height: 100%;
}

.hasTagsView {
  .app-main {
    /* 84 = navbar + tags-view = 50 + 34 */
    // min-height: calc(100vh - 84px);
  }

  .fixed-header + .app-main {
    // padding-top: 84px;
    padding-top: 105px;
    height: 100%;
  }
}
</style>

<style lang="scss">
// fix css style bug in open el-dialog
.el-popup-parent--hidden {
  .fixed-header {
    padding-right: 6px;
  }
}

::-webkit-scrollbar {
  width: 6px;
  height: 6px;
}

::-webkit-scrollbar-track {
  background-color: #f1f1f1;
}

::-webkit-scrollbar-thumb {
  background-color: #c0c0c0;
  border-radius: 3px;
}
</style>

