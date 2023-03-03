<template>
  <Submenu :name="`${parentName}`">
    <template slot="title">
      <div style="color: white">
        <common-icon :type="parentItem.icon || ''" />
        <span>{{ showTitle(parentItem) }}</span>
      </div>
    </template>
    <!--  -->
    <template v-for="item in children">
      <!-- 三级菜单 -->
      <template v-if="item.children && item.children.length === 1">
        <div style="color: white" :key="`menu-${item.name}`">
          <side-menu-item
            v-if="showChildren(item)"
            :parent-item="item"
          ></side-menu-item>
          <menu-item v-else :name="getNameOrHref(item, true)"
            ><common-icon :type="item.children[0].icon || ''" /><span>{{
              showTitle(item.children[0])
            }}</span></menu-item
          >
        </div>
      </template>
      <!-- 二级菜单 -->
      <template v-else>
        <side-menu-item
          v-if="showChildren(item)"
          style="color: white; background: #203562"
          :key="`menu-${item.name}`"
          :parent-item="item"
        ></side-menu-item>
        <menu-item
          style="color: white; background: #203562"
          v-else
          :name="getNameOrHref(item)"
          :key="`menus-${item.name}`"
          ><common-icon :type="item.icon || ''" /><span>{{
            showTitle(item)
          }}</span></menu-item
        >
      </template>
    </template>
  </Submenu>
</template>
<script>
import mixin from './mixin'
import itemMixin from './item-mixin'
export default {
  name: 'SideMenuItem',
  mixins: [mixin, itemMixin]
}
</script>
