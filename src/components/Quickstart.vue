<template>
  <div class="mb-6">
    <div class="d-flex border-bottom mb-4 pb-4">
      <div class="hide-sm hide-md">
        <img width="100" height="100" class="mr-4 mb-4" src="/img/me.jpg"/>
      </div>
      <p>Hey <b>{{ username }}</b>! You seem to be just arrived in the city. You may try to make some friends but I rather suggest you to start to defend yourself before starting any friendship. Nobody knows how much time you will stand there, but everyone will try to steal what you are producing! You should fulfill theses missions before getting some new ones.</p>
    </div>
    <ul class="missions list-style-none">
      <li>
        <Icon class="mr-2" :name="mission1 ? 'check' : 'chevron-right'"/>
        <router-link to="/buildings">Upgrade the headquarters</router-link>
      </li>
      <li>
        <Icon class="mr-2" :name="mission2 ? 'check' : 'chevron-right'"/>
        <router-link to="/drugs">Increase your DRUGS production</router-link>
      </li>
      <li>
        <Icon class="mr-2" :name="mission3 ? 'check' : 'chevron-right'"/>
        <router-link to="/weapons">Increase your WEAPONS production</router-link>
      </li>
      <li>
        <Icon class="mr-2" :name="mission4 ? 'check' : 'chevron-right'"/>
        <router-link to="/alcohols">Increase your ALCOHOLS production</router-link>
      </li>
      <li>
        <Icon class="mr-2" :name="mission5 ? 'check' : 'chevron-right'"/>
        <router-link to="/buildings">Build a training facility!</router-link>
      </li>
      <li>
        <Icon class="mr-2" :name="mission6 ? 'check' : 'chevron-right'"/>
        <router-link to="/units">Recruit some units</router-link>
      </li>
      <li>
        <Icon class="mr-2" :name="mission7 ? 'check' : 'chevron-right'"/>
        <router-link to="/fight">Start a fight</router-link>
      </li>
    </ul>
  </div>
</template>

<script>
import buildings from 'drugwars/buildings.json';

export default {
  data() {
    return {
      username: this.$store.state.auth.username,
    };
  },
  computed: {
    mission1() {
      const building = this.$store.state.game.user.buildings.find(
        b => b.building === 'headquarters',
      );
      return !!(building && building.lvl > 0);
    },
    mission2() {
      return !!this.$store.state.game.user.buildings.find(
        b =>
          b.building &&
          buildings[b.building].production_type === 'drugs' &&
          buildings[b.building].production_rate > 0,
      );
    },
    mission3() {
      return !!this.$store.state.game.user.buildings.find(
        b =>
          b.building &&
          buildings[b.building].production_type === 'weapons' &&
          buildings[b.building].production_rate > 0,
      );
    },
    mission4() {
      return !!this.$store.state.game.user.buildings.find(
        b =>
          b.building &&
          buildings[b.building].production_type === 'alcohol' &&
          buildings[b.building].production_rate > 0,
      );
    },
    mission5() {
      const building = this.$store.state.game.user.buildings.find(
        b => b.building === 'training_facility',
      );
      return !!(building && building.lvl > 0);
    },
    mission6() {
      return this.$store.state.game.user.units.length > 0;
    },
    mission7() {
      return !!this.$store.state.game.fights.find(f => f.username === this.username);
    },
  },
};
</script>

<style scoped lang="less">
.missions {
  li {
    font-size: 18px;
    margin-bottom: 12px;

    .iconfont {
      font-size: 18px;
    }
  }
}
</style>
