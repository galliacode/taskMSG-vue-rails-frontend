<template>
  <div class="md-layout">
    <div class="md-layout-item md-medium-size-40 md-xsmall-size-100 md-size-30">
      <!-- <UserLeftDock /> -->
    </div>
    <div class="md-layout-item md-medium-size-60 md-xsmall-size-100 md-size-70 tasks">
      <stats-card header-color="">
        <template slot="header" style="padding-top: 10px">
          <p class="category" style="float: left; color: blue; font-weight: 700; padding-top: 10px;">accounts</p>
          <p class="category create-account" style="float: right; color: blue; font-weight: 700; padding-top: 5px;" @click="createaccount" >Create account</p>
        </template>
        
        <template slot="footer">
          <div v-for="(account,n) in urAccountsStates.accounts" :key="'tag'+n" class="account-info">
            <DetailAccount :account="account"/>
            <md-divider class="md-hr md-theme-demo-light" />
          </div>
        </template>
      </stats-card>
    </div>
  </div>
</template>
<script>
import { mapGetters } from "vuex";
import store from "@/store";
import { act_user } from "@/store/types/actions.type";
// import EditUser from "./edit.vue";
import { StatsCard } from "@/components";
// import LeftDock from "../LeftDock.vue";
import DetailAccount from "./detail.vue";

export default {
  name: 'accounts',
  computed: {
    ...mapGetters(["urAccountsStates"])
  },
  components: {
    StatsCard,
    DetailAccount
    // UserLeftDock,
  },
  beforeRouteEnter(to, from, next) {
    Promise.all([
      store.dispatch(act_user.accounts.search),
    ]).then(() => {
      next();
    });
  },
  data() {
    return {
    };
  },
  methods: {
    createaccount() {
      alert('view create form...');
    },
  }
};
</script>
<style lang="scss">
  .tasks {
    .md-card-header {
      padding: 0;
    }
    .md-card-tabs .md-list .md-list-item .md-list-item-button .md-list-item-content {
      padding: 0;
    }
    .tab-content {
      display: inline;
    }
    .create-task:hover {
      cursor: pointer;
    }
  }
</style>
