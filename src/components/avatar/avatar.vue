<template>
  <div class="h-avatar" :class="avatarClass">
    <div :style="avatarImageStyle" :class="avatarImageClass" class="h-avatar-image-container">
      <div class="h-avatar-image" :style="imageStyle"></div>
    </div>
    <div class="h-avatar-info" :style="infoStyle">
      <slot></slot>
    </div>
  </div>
</template>

<script>
import config from '../../utils/config';

export default {
  name: 'hAvatar',
  props: {
    shape: {
      type: String,
      default: 'circle' // square
    },
    src: String,
    width: {
      type: Number,
      default: 50
    },
    distance: {
      type: Number,
      default: 15
    },
    imageTop: Number,
    type: String
  },
  computed: {
    imageStyle() {
      if(this.src) {
        return {
          'background-image': `url(${config.getOption('avatar').handleSrc.call(this, this.src)})`
        }
      }
      return {};
    },
    avatarClass() {
      return {
        [`h-avatar-type-${this.type}`]: !!this.type,
        [`h-avatar-shape-${this.shape}`]: !!this.shape,
      }
    },
    avatarImageClass() {
      if (!this.imageTop) {
        return {
          'h-avatar-middle': true
        }
      }
    },
    avatarImageStyle() {
      let s = {
        width: `${this.width}px`,
        height: `${this.width}px`,
      }
      if (this.imageTop) {
        s.top = `${this.imageTop}px`;
      }
      return s;
    },
    infoStyle() {
      return {
        'padding-left': `${this.width + this.distance}px`,
        'min-height': `${this.width}px`,
      }
    }
  },
};
</script>
