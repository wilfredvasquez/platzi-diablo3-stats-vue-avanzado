<template>
  <div>
    <h2 class="my-4 font-diablo">Hero List</h2>
    <b-table
      hover
      striped
      dark
      :items="heroes"
      :fields="fields"
      stacked="sm"
      small
    >
      <template v-slot:cell(name)="data">
        <HeroIco :hero="data.item"/>
      </template>
      <template v-slot:cell(class)="data">
        <HeroNameLevel :hero="{ classSlug: data.item.class, level: data.item.level }"/>
      </template>
      <template v-slot:cell(kills)="data">
        <span>{{ data.item.kills.elites | formatNumber }}</span>
      </template>
    </b-table>
  </div>
</template>

<script>
import HeroIco from './HeroIco'
import HeroNameLevel from './HeroClassLevel'
import { formatNumber } from '@/filters/numeral'

export default {
  name: 'HeroesList',
  props: {
    heroes: {
      required: true,
      type: Array
    }
  },
  filters: {
    formatNumber
  },
  components: { HeroIco, HeroNameLevel },
  data () {
    return {
      fields: [
        {
          key: 'name',
          label: 'Name'
        },
        {
          key: 'class',
          label: 'Class',
          sortable: true
        },
        {
          key: 'kills',
          label: 'Elite Kills',
          sortable: true
        }
      ]
    }
  }
}
</script>
