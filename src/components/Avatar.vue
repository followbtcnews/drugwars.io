<template>
  <router-link
    :to="`/@${username}`"
    class="avatar"
    :style="{
      'width': `${this.size}px`,
      'height': `${this.size}px`,
    }"
  >
    <span class="avatar-img"
      :style="{
        'background-image': `url(https://steemitimages.com/u/${username}/avatar`,
        'width': `${this.size}px`,
        'height': `${this.size}px`,
       }"
    />
    <span class="avatar-border"/>
    <span class="level py-1 px-2" v-if="xp">
      {{ parseFloat(((Math.sqrt(625 + 100 * xp) - 25) / 50) + 1).toFixed(0) }}
    </span>
    <span class="rank py-1 px-2" v-if="rank">
      {{ rank }}
    </span>
  </router-link>
</template>

<script>
export default {
  props: ['username', 'size', 'xp', 'rank'],
};
</script>

<style scoped lang="less">
@import '../vars.less';

.avatar {
  position: relative;
  overflow: visible;

  .avatar-img {
    position: absolute;
    left: 0;
    top: 0;
    width: 100%;
    height: 100%;
    background-size: cover;
    background-repeat: no-repeat;
    background-position: 50% 50%;
    border-radius: 50%;
    border: 1px solid rgba(255, 255, 255, 0.4);
  }

  .level,
  .rank {
    display: inline-block;
    position: absolute;
    top: 0;
    left: -20px;
  }

  .avatar-border {
    display: inline-block;
    position: absolute;
    top: -5%;
    left: -12%;
    bottom: -18%;
    right: -10%;
    background-image: url('/img/avatar-border.png');
    background-size: contain;
    background-repeat: no-repeat;
  }
}
</style>
