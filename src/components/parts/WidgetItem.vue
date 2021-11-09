<template>
  <div class="widget-family">
    <div class="widget"
      @mouseover="onMouseOver"
      @mouseleave="onMouseLeave"
      v-bind:class="{mouseover: widget.mouseover}"
    >
      ・<input v-model="widget.text" class="transparent" placeholder="本文" />
      <div v-show="widget.mouseover" class="buttons">
        <div class="button-icon" v-if="layer < 3" @click="onClickChildWidget(widget)">
          <i class="fas fa-sitemap"></i>
        </div>
        <div class="button-icon" @click="onClickAddWidgetAfter(parentWidget, widget)">
          <i class="fas fa-plus-circle"></i>
        </div>
        <div class="button-icon" @click="onClickDelete(parentWidget, widget)">
          <i class="fas fa-trash"></i>
        </div>
        <div class="button-icon">
          <i class="fas fa-cog"></i>
        </div>
      </div>
    </div>
    <div class="child-widget">
      <WidgetItem
        v-for="childWidget in widget.children"
        v-bind:widget="childWidget"
        v-bind:parentWidget="widget"
        v-bind:layer="layer + 1"
        v-bind:key="childWidget.id"
        @delete="onClickDelete"
        @addChild="onClickChildWidget"
        @addWidgetAfter="onClickAddWidgetAfter"
      />
    </div>
  </div>
</template>

<script>
export default {
  name: 'WidgetItem',
  props: [
    'widget',
    'parentWidget',
    'layer',
  ],
  methods: {
    onMouseOver : function() {
      this.widget.mouseover = true;
    },
    onMouseLeave : function() {
      this.widget.mouseover = false;
    },
    onClickDelete : function(parentWidget, widget) {
      this.$emit('delete', parentWidget, widget);
    },
    onClickChildWidget : function(widget) {
      this.$emit('addChild', widget);
    },
    onClickAddWidgetAfter : function(parentWidget, widget) {
      this.$emit('addWidgetAfter', parentWidget, widget);
    },
  },
}
</script>

<style scoped lang="scss">
.widget {
  width: 100%;
  min-height: 40px;
  display: flex;
  align-items: center;
  padding: 5px 10px;
  color: rgba(25, 23, 17, 0.6);
  .buttons {
    display: flex;
    flex-direction: row;
    cursor: pointer;
    .button-icon {
      padding: 3px;
      margin-left: 3px;
      border-radius: 5px;
    }
  }
}
.child-widget {
  padding-left: 10px;
}
</style>