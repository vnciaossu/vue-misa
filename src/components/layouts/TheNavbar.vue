<template>
  <div>
    <div id="navbar" >
       <div v-bind:key="tabs[0].key"   @click="currentTabKey = tabs[0].key">
      <router-link class="logo-box" to="/index">
        <div class="sidebar"></div>
        <div class="logo"></div>
      </router-link></div>

      <div class="navbar-box" >
         <div v-bind:key="tabs[0].key" v-bind:class = "{'navbar-item-click':tabs[0].key == currentTabKey}"  @click="currentTabKey = tabs[0].key">
          <router-link class="navbar-item" to="/index" >
            <div class="navbar-icon icon-dashboard" ></div>
            <div class="navbar-text" >Tổng quan</div>
        </router-link></div>
        <div v-bind:key="tabs[1].key" v-bind:class = "{'navbar-item-click':tabs[1].key == currentTabKey}"  @click="currentTabKey = tabs[1].key">
        <router-link class="navbar-item" to="/report" >
          <div class="navbar-icon icon-report"></div>
          <div class="navbar-text">Báo cáo</div>
        </router-link></div>
         <div  v-bind:key="tabs[2].key" v-bind:class = "{'navbar-item-click':tabs[2].key == currentTabKey}"  @click="currentTabKey = tabs[2].key">
         <router-link class="navbar-item" to="/customer">
              <div class="navbar-icon icon-dic-employee"></div>
                <div class="navbar-text">Danh sách khách hàng</div>
            </router-link></div>
           <div  v-bind:key="tabs[3].key" v-bind:class = "{'navbar-item-click':tabs[3].key == currentTabKey}"  @click="currentTabKey = tabs[3].key">
             <router-link class="navbar-item" to="/employee">
               <div class="navbar-icon icon-dic-employee"></div>
                <div class="navbar-text">Danh sách nhân viên</div>
            </router-link></div>
             <div  v-bind:key="tabs[4].key" v-bind:class = "{'navbar-item-click':tabs[4].key == currentTabKey}"  @click="currentTabKey = tabs[4].key">
            <router-link class="navbar-item" to="/setting">
              <div class="navbar-icon icon-setting"></div>
              <div class="navbar-text">Cài đặt</div>
            </router-link></div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data(){
    return{
    currentTabKey: 'dashboard',
    tabs: [
        { key: 'dashboard'},
        { key: 'report' },
        { key: 'customer'},
        { key: 'employee'},
        { key: 'setting'},       
    ]}
  }
}
</script>

<style scoped>
#navbar {
  position:absolute;
  top: 0;
  width: 200px;
  height: 100vh;
  border-right: 1px solid #dedede;
}

.logo-box {
  display: flex;
  align-items: center;
  height: 60px;
  width: 100%;
  cursor: pointer;
}

.logo-box .sidebar {
  margin-left: 16px;
  flex-shrink: 0;
  width: 30px;
  height: 30px;
  background-image: url("../../assets/img/toggle.png");
  background-size: contain;
  background-repeat: no-repeat;
  background-position: center;
}

.logo-box .logo {
  margin-left: 8px;
  width: 100%;
  height: 30px;
  flex-shrink: 0;
  background-image: url("../../assets/img/cukcuk-logo.png");
  background-size: contain;
  background-position: left;
  background-repeat: no-repeat;
}
.navbar-box .navbar-item {
  display: flex;
  align-items: center;
  height: 44px;
  padding: 0;
}

.navbar-box .navbar-item:hover {
  background-color: #dedede;
  cursor: pointer;
}

.navbar-box .navbar-item:active {
  background-color: #bebebe;
  cursor: pointer;
}

.navbar-item-click{
  background-color: #dedede;
}

.navbar-item .navbar-icon {
  margin-left: 16px;
  width: 20px;
  height: 20px;
  background-size: contain;
  background-repeat: no-repeat;
  background-position: center;
}

.navbar-item .navbar-text {
  margin-left: 10px;
}

</style>