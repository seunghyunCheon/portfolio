<template lang="">
  <div class="About_wrap">
      <div class="About_title">
        About me
      </div>
      <div class="About_text">
      안녕하세요 천승현입니다. 끝을 모르게 성장하고 싶습니다. 감사합니다.
      </div>
      <!-- info -->
      <div class="icons_dummy">
        <div class="icons_flex" v-for="(item, index) in user" :key="index">
          <i :class="icons[index]"></i>
          <div class="icons_flex_col">
            <span v-if="userInfo">{{userInfo[index]}}</span>
            <span>{{userInfoValue[index]}}</span>
          </div>
        </div>
      </div>
    </div>
</template>
<script>
export default {
  data() {
    return{
      userInfo : {},
      userInfoValue : {},
    }
  },
  computed: {
    icons() {
      return this.$store.state.icons;
    },
    user() {
      return this.$store.state.user;
    },
  },
  methods: {
    filter(f,iter){
      var res = [];
      for (const a of iter){
        if(f(a)) res.push(a);
      }
      return res;
    },
    map(f, iter){
      var res =[];
      for (const a of iter){
        res.push(f(a))
      }
      return res;
    },
  },
  created() {
    const user = [{이름:'천승현', 아이콘:true}, 
                  {생년월일 :'98.08.07', 아이콘:true},
                  {이메일: 'csh7215@naver.com',아이콘:true}, 
                  {학력: '삼육대학교(4학년) 컴퓨터공학과', 아이콘: true},
                  {주소지 : '서울시 노원구', 아이콘:true}]
   
    const icons = ['fas fa-user', 'fas fa-calendar-week', 'fas fa-envelope', 'fas fa-pencil-alt',
                   'fas fa-map-marker-alt'];
    this.$store.commit('SET_ICONS', icons);
    this.$store.commit('SET_USER', user);
  },
  mounted() {
     this.userInfo = this.map(u=> u.shift(),this.map(u=>Object.keys(u),this.user));
     console.log(this.userInfo);
     this.userInfoValue = this.map(u=>u.shift(),this.map(u=>Object.values(u),this.user));
  },
}
</script>
<style lang="">
  
</style>