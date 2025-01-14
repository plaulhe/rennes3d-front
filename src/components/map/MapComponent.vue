<script setup lang="ts">
import { useLayersStore } from '@/stores/layers'
import type { MapCollection } from '@vcmap/core'
import { onMounted, ref } from 'vue'
import type { Ref } from 'vue'
import { prepareContext } from '../../services/vcmap/context'
import UiButton from '../ui/UiButton.vue'
import UiMap from '../ui/UiMap.vue'
import TransportButtons from './TransportButtons.vue'

let mapCollection: Ref<MapCollection | undefined> = ref(undefined)
const layerStore = useLayersStore()

onMounted(async () => {
  mapCollection.value = await prepareContext()
})

function setLayerVisible(layerName: string, visible: boolean) {
  const layer = mapCollection.value?.layerCollection.getByKey(layerName)
  if (visible) {
    layer?.activate()
  } else if (layer?.active) {
    layer.deactivate()
  }
}

function is3D(): boolean {
  return mapCollection.value?.activeMap.name === 'cesium'
}

function toggleMap() {
  mapCollection.value?.setActiveMap(is3D() ? 'ol' : 'cesium')
}

layerStore.$subscribe(() => {
  setLayerVisible('metro', layerStore.visibilities.metro)
  setLayerVisible('bus', layerStore.visibilities.bus)
  setLayerVisible('bike', layerStore.visibilities.bike)
})
</script>
<template>
  <UiMap :map="mapCollection"> </UiMap>
  <div class="absolute right-2 top-2 z-10">
    <TransportButtons></TransportButtons>
  </div>
  <div class="absolute right-2 bottom-2">
    <UiButton @click="toggleMap">{{ is3D() ? '2D' : '3D' }}</UiButton>
  </div>
</template>
