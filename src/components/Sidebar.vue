<template>
  <div class="panel panel-default">
    <div class="panel-heading">
      <h1 class="text-center">当月消费累计</h1>
    </div>

    <div class="panel-body">
      <h1 class="text-center">{{ money }} 元</h1>
    </div>

  </div>
</template>
<script>
    export default {
      name : 'Sidebar',
      computed: {
        money() {
          return this.$store.state.totalMoney
        }
      }
    }
</script>
