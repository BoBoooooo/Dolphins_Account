<template>
  <div>
    <router-link
      v-if="$route.path !== '/time-entries/log-time'"
      to="/time-entries/log-time"
      class="btn btn-primary">
      创建
    </router-link>

    <div v-if="$route.path === '/time-entries/log-time'">
      <h3>创建</h3>
    </div>

    <hr>

    <router-view></router-view>

    <div class="time-entries">
      <p v-if="!plans.length"><strong>还没有任何账单</strong></p>

      <div class="list-group">
        <a class="list-group-item" v-for="(plan,index) in plans">
          <div class="row">
            <div class="col-sm-2 user-details">
              <img :src="plan.avatar" class="avatar img-circle img-responsive" />
              <p class="text-center">
                <strong>
                  {{ plan.name }}
                </strong>
              </p>
            </div>

            <div class="col-sm-2 text-center time-block">
               <p class="label label-success text-center">
                <i class="glyphicon glyphicon-calendar"></i>
                {{ plan.date }}
              </p>
              <h3 class="list-group-item-text total-time">
                <i class="glyphicon glyphicon-yen"></i>
                {{ plan.totalMoney }}
              </h3>
             
            </div>

            <div class="col-sm-6 comment-section text-center">
              <p>{{ plan.comment }}</p>
            </div>

            <div class="col-sm-2 text-center">
              <button
                class="btn btn-xs btn-danger delete-button "
                @click="deletePlan(index)">
              删除
              </button>
            </div>

          </div>
        </a>

      </div>
    </div>
  </div>
</template>
<script>
    export default {
        name : 'TimeEntries',
        computed : {
          plans () {
            return this.$store.state.list
          }
        },
        methods : {
          deletePlan(idx) {
            // 减去总时间
            this.$store.dispatch('decTotalTime',this.plans[idx].totalTime)
            // 删除该计划
            this.$store.dispatch('deletePlan',idx)
          }
        }
    }
</script>
<style>
.avatar {
    height: 75px;
    margin: 0 auto;
    margin-top: 10px;
    margin-bottom: 10px;
  }
   .user-details {
    background-color: #f5f5f5;
    border-right: 1px solid #ddd;
    margin: -10px 0;
  }

.list{
  position: absolute;
  left: 50%;
  top:50%;
  transform: translate(-50%,-50%);

}
</style>
