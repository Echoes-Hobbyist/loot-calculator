<template>
  <div class="relative">
    <div class="p-2 bg-black bg-opacity-30">
      <div
        class="flex flex-wrap -mx-0.5 mb-2">
        <div
          v-for="item in displayedItems"
          :key="item.id"
          class="w-1/2 md:w-1/3 lg:w-1/4 px-0.5 mb-1">
          <shared-loot-item
            :item="item"
            :member-loot="memberLoot" />
        </div>
      </div>
    </div>
    <div class="z-30 py-2 bg-black border-t border-green-600 md:sticky md:bottom-0 bg-opacity-70">
      <div class="flex items-center justify-between">
        <div class="px-4 py-2 text-3xl text-white">
          {{ memberLoot.loot.length }} <span class="-ml-1 text-sm text-gray-400">item(s)</span>
        </div>
        <div class="flex pr-4">
          <div>
            <div class="text-sm text-gray-400">
              Estimated Total
            </div>
            <div class="text-2xl text-yellow-400">
              {{ lootValue ? lootValue.toLocaleString() : 0 }}
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { mapGetters } from 'vuex';
import SharedLootItem from "./SharedLootItem";
export default {
  props: ['items', 'member-loot'],
  components: {
    SharedLootItem,
  },
  computed: {
    ...mapGetters([
      'averageLootValue'
    ]),
    lootValue () {
      if (!this.memberLoot.loot_value) {
        return 0
      }
      return this.memberLoot.loot_value
    },
    displayedItems () {
      return this.items
    },
    lootValueDiffPercent () {
      const diff = this.lootValue - this.averageLootValue
      return Math.floor((diff / this.averageLootValue) * 100)
    },
    hasLootValueDiff () {
      return Math.abs(this.lootValue - this.averageLootValue)
    },
  }
}
</script>

<style>

</style>
