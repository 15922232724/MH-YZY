<template>
  <div>
    <public-content :name="$options.name">
      <el-collapse accordion>
        <el-collapse-item>
          <template slot="title">
            <img src="/icons/filtrate.png" width="20px" height="20px" />
            {{$t('infoMap.high-levelScreening')}}
          </template>
          <enum-type :name="$options.name" :enumerateArray="$allConfig[$options.name]"></enum-type>

          <filter-by-dict
            :line="true"
            :dictName1="'tableSearch.property'"
            :dictName="'产权'"
            dictKey="equity"
            @returnData="(e) => {$set(info, 'equity', e)}"
          ></filter-by-dict>
        </el-collapse-item>
      </el-collapse>
    </public-content>
  </div>
</template>

<script>
import publicContent from '../public/content'
import enumType from '../public/enumerateType'
import filterByDict from '../public/filterByDict'

export default {
  name: 'pipeSection',
  components: {
    publicContent,
    enumType,
    filterByDict
  },
  data () {
    return {
      info: {}
    }
  },
  watch: {
    info: {
      handler: function (newVal) {
        this.$store.commit('updateDisplayListConfig', {
          name: this.$options.name,
          val: newVal
        })
      },
      deep: true
    }
  }

}
</script>
