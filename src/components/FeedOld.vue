<template>
  <div>
    <div class="layout-padding">
      <!--<p><strong>{{posts.title}}</strong></p>
      <p><strong>{{posts.locname}}</strong></p>
      <p><strong>{{posts.desc}}</strong></p>
      <p><strong>{{posts.user}}</strong></p>
      <p><strong>{{posts.image}}</strong></p>-->
      <img :src="posts.image" />
      <!-- Uploaded Image of Incident-->
      <div v-if="!image">
        <input type="file" accept="image/*" @change="onFileChange">
      </div>
      <div v-else>
        <img :src="image" />
        <br/>
        <button class="negative" @click="removeImage">Remove image</button>
        <br/><br/><br/>
      </div>
      <div class="content">
        <h1>Incident Feed</h1>
        <div class="card bg-light">
        </div>
      </div>
      <PostBox
        :usrAvatar="avtr"
        :userName="usrnm"
        :postContent="ctn"
        :imgHere="flag"
        :postImg="imgs"/>
    </div>
  </div>
</template>

<script>

/* For Axios */
import Vue from 'vue'
import axios from 'axios'
import VueAxios from 'vue-axios'
Vue.use(VueAxios, axios)

import PostBox from './PostBox'
var avtr = '../statics/snorlax.png'
var usrnm = 'asdf'
var ctn = `check check this out check this out`
var flag = true

export default {
  components:
  {
    PostBox
  },
  data () {
    return {
      posts: [],
      avtr: avtr,
      usrnm: usrnm,
      ctn: ctn,
      flag: flag,
      imgs: avtr,
      image: ''
    }
  },
  onFileChange (e) {
    var files = e.target.files || e.dataTransfer.files
    if (!files.length) {
      return
    }
    this.createImage(files[0])
  },
  createImage (file) {
    // var image = posts.image
    var reader = new FileReader()
    var vm = this

    reader.onload = (e) => {
      vm.image = e.target.result
    }
    reader.readAsDataURL(file)
  },
  removeImage: function (e) {
    this.image = ''
  },
  created () {
    // http://jsonplaceholder.typicode.com/posts
    axios.get('http://sample-env.2fnpngmx26.us-west-2.elasticbeanstalk.com/report/5912b1739f222808f0b7b114')
    .then(response => {
      // JSON responses are automatically parsed.
      this.posts = response.data
    })
    .catch(e => {
      this.errors.push(e)
    })

    // async / await version (created() becomes async created())
    //
    // try {
    //   const response = await axios.get(`http://jsonplaceholder.typicode.com/posts`)
    //   this.posts = response.data
    // } catch (e) {
    //   this.errors.push(e)
    // }
  }
}
</script>

<style>
.content
{
  display:flex;
  flex-direction: column;
  align-items: center;
}


.header
{

}


.incident_block {
    background-color: #dcdfe6;
    color: #00000;
    margin-left: 5em;
    margin-right: 10em;
}


.incident_pic {
    height: auto;
    width: auto;
    max-width: 12em;
    max-height: 12em;
}


.postContainer
{
  margin-top: 25px;
  margin-bottom: 25px;

  min-width: 320px;

  width: 55vw;

  display: flex;
  flex-direction: column;
}


.postContainer > div {
  width:100%;
}


.imgHolder
{
  max-width: 100%;
  height:auto;
  overflow: hidden;
}


.imgContent
{
  width: 100%;

}

.postHeader
{
  display:flex;
  align-items: center;

}

.postHeader > div
{
  display: flex;
  align-items: center;
}








/*******************************************************/
/* FOR REDDIT STYLE TRIAL*/
.voteBtnContainer
{
  display:flex;
  flex-grow: 0;
}
.voteBtnContainer button
{
  display:flex;
}



.avatarImg
{
  width: 50px;
  height:50px;
  border-radius: 100%;
  margin: 5px 5px 5px 5px;
}

.postContent
{
  display:flex;
  flex-direction: column;
}

.postIn
{
  display:flex;;
  flex-direction: row;
}
.postText
{

}



.postContainer1
{
  margin-top: 25px;
  margin-bottom: 25px;

  /* for beautifying the box */
  background-color: #F6F6F6;
  padding: 10px 10px 10px 10px;
  -webkit-box-shadow: 1px 1px 6px 0.5px rgba(194,194,194,1);
  -moz-box-shadow: 1px 1px 6px 0.5px rgba(194,194,194,1);
  box-shadow: 1px 1px 6px 0.5px rgba(194,194,194,1);

  display:flex;
  flex-direction: row;

  align-items: center;
}
</style>
