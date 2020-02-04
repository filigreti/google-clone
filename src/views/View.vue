<template>
  <div class="view">
    <div class="header">
      <div>
        <img class="google" src="@/assets/google.png" alt />
      </div>
      <img @click="$router.go(-1)" class="back" src="@/assets/back-arrow.svg" alt />
    </div>
    <div class="content">
      <span class="content-cont">
        <img class="color-icon" src="@/assets/color-logo.svg" alt />
        <router-link style="padding-left:5px" to="/view">All</router-link>
      </span>
    </div>
    <div v-if="$route.params.data && $route.params.clicked" class="main-body">
      <div>
        <h3>Search Result for {{$route.params.searched}}</h3>
        <div>
          <h3 style="color:#1a0dab;font-size:20px;margin-bottom:0px">{{$route.params.data.name}}</h3>
          <div style="padding-top:5px; color:#006621">{{$route.params.data.picture}}</div>
          <div style="width:55%">{{$route.params.data.about}}</div>
        </div>
      </div>
    </div>
    <div class="main-body" v-else-if="$route.params.data && !$route.params.clicked">
      <div style="font-size:15px" v-if="$route.params.data.length == 0">
        Your Search
        <b>-{{$route.params.searched}}-</b> did not match any documents
        <h3>Suggestions:</h3>
        <ul>
          <li>You can always use google</li>
          <li>Like why you decided to use this, ill never know</li>
          <li>😒</li>
        </ul>
      </div>
      <div v-else>
        <h3>Search Result for {{$route.params.searched}}</h3>
        <div v-for="item in $route.params.data" :key="item.id">
          <div>
            <h3 style="color:#1a0dab;font-size:20px;margin-bottom:0px">{{item.name}}</h3>
            <div style="padding-top:5px; color:#006621">{{item.picture}}</div>
            <div style="width:55%">{{item.about}}</div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>


<script>
export default {
  beforeRouteEnter(to, from, next) {
    next(vm => {
      if (from.name == null) {
        vm.$router.go(-1);
      } else {
        next();
      }
    });
  }
};
</script>

<style scoped>
.header {
  height: 10vh;
  width: 50%;
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-top: 5px;
}
.view {
  box-sizing: border-box;
}
.google {
  height: 33px;
  padding-left: 20px;
}
.back {
  height: 33px;
}
.content {
  border-bottom: 1px solid #e5e5e5;
  height: 6vh;
  display: flex;
  flex-direction: column;
  justify-content: flex-end;
}
.color-icon {
  height: 20px;
}
.content-cont {
  margin-left: 150px;
  display: flex;
  align-items: center;
  position: relative;
  width: 63px;
  padding-bottom: 15px;
}
.content-cont:after {
  position: absolute;
  content: "";
  height: 3px;
  width: 100%;
  background: #1a73e8;
  bottom: 0;
  left: -10px;
}
.main-body {
  margin-left: 150px;
  margin-top: 50px;
  color: #222;
  font-size: 14px;
}
.main-body b {
  color: black;
  font-size: 15px;
}
</style>
