<template>
  <div>
    <el-tabs value="first">
      <el-tab-pane :label="$t('subdistricts.base_infomation')" name="first">
        <public-form-event
          style="width: 50%;"
          size="mini"
          label-width="100px"
          :eventBus="eventBus"
          :column="tableColumn"
        ></public-form-event>
      </el-tab-pane>
      <el-tab-pane :label="$t('subdistricts.Editing_machine_room')" name="second">
        <net-edit :eventBus="eventBus"></net-edit>
      </el-tab-pane>
    </el-tabs>
  </div>
</template>

<script>

import { column } from "../index.js";
import NetEdit from "../components/net/index";

export default {
  name: "AddContent",
  props: {
    request: Object,
    eventBus: Object
  },
  components: {
    NetEdit
  },
  computed: {
    tableColumn: function () {
      return Object.values(column)
        .filter(item => item.edit && item.edit.display)
        .filter(item => item.edit.display())
        .map(item => {
          return {
            title: item.title,
            key: item.key,
            ...item.edit
          };
        });
    }
  }
};
</script>
