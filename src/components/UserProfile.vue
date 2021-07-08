<template>
    <div class="user-profile">
        <div class="user-profile__user-panel">
            <h1 class="user-profile__username">@{{user.username}}</h1>
            <div class="user-profile__badges">
                <div class="user-profile__admin-badge" v-if="user.isAdmin">
                Admin
               </div>
              <div class="user-profile__verification-badge" v-if="user.isVerified">
                V
              </div>
            </div>
            <div class="user-profile__follower-count">
                <strong>Followers: </strong> {{followers}}
            </div>
            <form class="user-profile__create-conspiracy">
                <label for="newConspiracy">
                    <strong>
                        New Conspiracy
                    </strong>
                </label>
                <textarea id="newConspiracy" rows="4" v-model="newConspiracyContent"/>

                <div class="user-profile__create-conspiracy-type">
                    <label for="newConspiracyType"><strong>Type: </strong></label>
                    <select id="newConspiracyType">
                        <option :value="option.value" 
                        v-for="(option, index) in conspiracyTypes"
                        :key="index"
                        >
                        {{option.name}}
                        </option>
                    </select>
                </div>
            </form>
        </div>
        <div class="user-profile__conspiracies-wrapper">
            <ConspiracyItem 
            v-for="conspiracy in user.conspiracies"
            :key="conspiracy.id"
            :username="user.username"
            :conspiracy="conspiracy"
            @favourite="toggleFavourite"
            />
        </div>
    </div>
</template>

<script>
import ConspiracyItem from './ConspiracyItem.vue'

export default {
  name: 'UserProfile',
  components: {ConspiracyItem},
  data() {
    return {
      newConspiracyContent: '',
      selectedConspiracyType: 'draft',
      conspiracyTypes: [
          {value: 'draft', name: 'Draft'},
          {value: 'instant', name: 'Instant Conspiracy'}
      ],
      followers: 0,
      user: {
        id: 1,
        username: '_MaryJane1988',
        firstName: 'Mary',
        lastName: 'Jane',
        email:'maryjane@conspiracy.com',
        isAdmin: true,
        isVerified: false,
        conspiracies : [
            {id: 1, content: 'Aliens Exist!!!'},
            {id: 2, content: '9/11 was an inside job'},
            {id: 3, content: 'Tupac is still alive'},
            {id: 4, content: 'We live in a simulation'}
        ]
      }
    }
  },
  watch: {
    followers(newFollowerCount, oldFollowerCount){
      if(oldFollowerCount < newFollowerCount){
        console.log(`${this.user.username} has gained a follower!`)
      }
    }
  },
  computed: {
    fullName(){
      return `${this.user.firstName} ${this.user.lastName}`
    }
  },
  methods: {
    followUser(){
      this.followers++
    },
    toggleFavourite(id){
        console.log(`Favourited conspiracy with id: #${id}`)
    }
  },
  mounted(){
    this.followUser();
  }
}
</script>

<style scoped>
.user-profile {
    display: grid;
    grid-template-columns: 1fr 3fr;
    width: 100%;
    padding: 50px 5%;
}

.user-profile__user-panel {
    display: flex;
    flex-direction: column;
    margin-right: 50px;
    padding: 20px;
    background-color: white;
    border-radius: 5px;
    border: 1px solid #dfe3e8;
}

h1 {
    margin: 0;
}

.user-profile__admin-badge, .user-profile__verification-badge{
    background-color: purple;
    color: white;
    border-radius: 5px;
    margin-right: auto;
    padding: 0px 15px;
    font: bold;
}

.user-profile__verification-badge{
    background-color: rgb(135, 206, 250);
}

.user-profile__badges{
    display: flex;
    padding: 15px 0px 10px;
}

.user-profile__create-conspiracy{
    padding-top: 20px;
}

textarea {
    width: 100%;
}

</style>