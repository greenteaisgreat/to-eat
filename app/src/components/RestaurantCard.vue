<!-- tells vue to use the typescript compiler -->
<script lang="ts">
/**
 * Restaurant
 */

import { defineComponent } from 'vue'
//helps typescript understand the Options API convention for property types
//it MUST be prefaced with 'type', as that's basically all it is
import type { PropType } from 'vue'

type Restaurant = {
  id: string
  name: string
  address: string
  website: string
  status: string
}

export default defineComponent({
  props: {
    restaurant: {
      //provides a more specific type of Object
      type: Object as PropType<Restaurant>,
      required: true,
    },
  },
  emits: ['delete-restaurant'],
  computed: {
    statusColor() {
      switch (this.restaurant.status) {
        case 'Want to Try':
          return 'is-warning'
        case 'Recommended':
          return 'is-success'
        case 'Do Not Recommend':
          return 'is-danger'
        default:
          return ''
      }
    },
  },
  methods: {
    deleteRestaurant() {
      this.$emit('delete-restaurant', this.restaurant)
    },
  },
})
</script>

<template>
  <article class="box">
    <div class="media">
      <aside class="media-left">
        <img src="https://placehold.jp/150x150.png" alt="" />
      </aside>
      <div class="media-content">
        <p class="title is-4 is-spaced mb-1">
          {{ restaurant.name }}
        </p>
        <p class="subtitle mb-2">
          <span class="tag" :class="statusColor">{{ restaurant.status }}</span>
        </p>
        <div class="content mb-2">
          {{ restaurant.address }}
        </div>
        <div>
          <button @click="deleteRestaurant" class="button is-small is-danger is-light">Delete</button>
        </div>
      </div>
    </div>
  </article>
</template>

<style></style>
