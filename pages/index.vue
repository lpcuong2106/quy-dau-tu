<template>
  <div style="width: 100%">
    <a-skeleton :loading="!info" />
    <a-row v-if="info" type="flex">
      <a-col v-for="ccq in info" :key="ccq" :span="6" class="gutter-row">
        <a-card
          v-if="ccq.trade_code"
          :title="ccq.trade_code"
          :bordered="true"
          style="width: 300px"
        >
          <p>{{ ccq.nav_ccq }}</p>
          <p>{{ ccq.per_nav_change }}</p>
          <p>{{ formatDate(ccq.trade_date) }}</p>
        </a-card>
      </a-col>
    </a-row>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
import axios from 'axios'
import { DataDef } from 'vue/types/options'
import format from 'date-fns/format'
import parse from 'date-fns/parse'

export default Vue.extend({
  name: 'IndexPage',
  data(): DataDef<
    {
      info:
        | null
        | {
            [key: string]: {
              nav_ccq: string
              trade_date: string
              per_nav_change: string
              trade_code: string
            }
          }[]
      tester: null | { name: String }
    },
    null,
    any
  > {
    return {
      info: null,
      tester: null,
    }
  },
  async mounted() {
    const { data } = await axios.get(
      'https://cors-anywhere.herokuapp.com/https://dragoncapital.com.vn/apiv2/nav/getAllLatestNav.php'
    )
    console.log(data)
    // @ts-ignore
    this.info = data
  },
  methods: {
    formatDate(date: string) {
      let parDate = parse(date, 'yyyy-MM-dd HH:mm:ss', new Date())
      if (!isNaN(parDate.getTime())) {
        return format(parDate, 'dd-MM-yyyy')
      }
    },
  },
})
</script>
