<template>
  <div class="headercomp flex flex-space-between">
    <div class="flex">
      <div class="flex flex-vert-cent flex-space-around link" id="logo" @click="router('/')">
        <div id="logo-icon" class="icon"></div>
      </div>
      <div v-if="user != null" class="flex flex-vert-cent flex-space-around link" @click="router('/')">
        <p>Home</p>
      </div>
      <div v-if="user != null" class="flex flex-vert-cent flex-space-around link" @click="router('/camp')">
        <p>Camp</p>
      </div>
      <div v-if="user != null" class="flex flex-vert-cent flex-space-around link" @click="router('/staff')">
        <p>Staff</p>
      </div>
      <div v-if="user != null" class="flex flex-vert-cent flex-space-around link" @click="router('/info')">
        <p>Info</p>
      </div>
    </div>
    <div v-if="user != null" class="flex">
      <div class="flex flex-vert-cent flex-space-around link " id="notification">
        <div id="inbox-icon" class="icon"></div>
      </div>
      <div class="flex flex-vert-cent flex-space-around link" id="profile" @click="router('/profile')">
        <p>{{user.username}}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'headercomp',
  data() {
      return {
        
      }
  },
  methods: {
    router(path) {
      this.$router.push(path);
    },

  },
  computed: {
    user() {
      return this.$store.state.user;
    },
  },
  created() {

  }
}
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css?family=Roboto+Slab:700&display=swap');
/* General */
.headercomp {
  width: 100vw;
  height: 65px;
  background-color: rgb(44, 129, 220);
  box-shadow: 0px 3px 3px rgb(190, 190, 190);
  border-bottom: 3px solid white;
  padding-right: 20px;
}
</style>

<style scoped>
/* Links */
.link {
  height: 100%;
  min-width: 50px;
  padding: 0px 20px;
  transition: all .2s ease;
  cursor: pointer;
  color: #fefefe;
  font-size: 1.3em;
  font-weight: bolder; 
  font-family: 'Roboto Slab', serif;
}

#profile {
  padding-right: 50px;
}

.active {
  background-color: rgba(224, 244, 253, 0.5) !important;
  color: #fefefe;
}




p {
  font-weight: lighter;
  text-align: center;
  font-size: .9em;
}

#login {
  padding: 0px 30px;
}

#register {
  padding: 0px 30px;
}
</style>

<style scoped>
/* Logos */
.icon
{
  display: block;
  width: 30px;
  height: 30px;
  background-size: 100% 100%;
  background-position: center;
}

.icon.left {
  margin-right: 10px;
}

#logo-icon {
  width: 35px;
  height: 35px;
  background-image: url("../../assets/General/logo.png");
  opacity: .8;
  transition: all .2s ease;
}

.link:hover #logo-icon {
  opacity: 1;
}

#inbox-icon {
  background-image: url("../../assets/General/inbox.png");
  opacity: .8;
  transition: all .2s ease;
}

#profile-icon {
  background-image: url("../../assets/General/profile.png");
  opacity: .8;
  transition: all .2s ease;
}

.link:hover #inbox-icon {
  opacity: 1;
}


.link:hover #profile-icon {
  opacity: 1;
}


.link:hover #files-icon {
  opacity: 1;
}
</style>

