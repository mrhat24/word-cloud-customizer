<template>
  <div class="hello">
    <div v-if="currentTag">
      <input  v-model="currentTag.title" type="text">
      <input  v-model="currentTag.order" type="range" min="0" max="32" step="1">{{ currentTag.order }}
      <input  v-model="currentTag.size" type="range" min="0" max="72" step="1">{{ currentTag.size }}px
    </div>
    <div class="services-tags">
      <div id="services-tags">
        <span v-for="tag in orderedTags" v-on:click="setcurtag(tag)" v-bind:style="{ fontSize: tag.size + 'px' }">{{ tag.title }} </span>
      </div>
    </div>
    <input type='checkbox' v-model="showTextarea">
    <textarea v-if="showTextarea" v-model="jsonTags" cols="120" rows="20"></textarea>
  </div>
</template>
<script>
var jtags = require('./../tags.json')
export default {
  name: 'hello',
  data () {
    return {
      msg: 'Welcome to Your   Vue.js  App',
      tags: jtags,
      title: '',
      currentTag: {},
      showTextarea: false
    }
  },
  methods: {
    addtag () {
      this.tags.push({title: this.title, size: 16, order: this.tags.length})
      this.title = ''
    },
    setcurtag (tag) {
      this.currentTag = tag
    }
  },
  computed: {
    jsonTags () {
      return JSON.stringify(this.tags, null, 2)
    },
    orderedTags:
      function () {
        return this.tags.sort(function (a, b) {
          return a.order - b.order
        })
      }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
.services-tags {
  margin: 0 auto;
  width: 1110px;
  padding-top: 30px;
  margin-top: 30px;
  position: relative;
  text-align: justify;
}
#services-tags span{
  font-family: Roboto;
  font-weight: bold;
  text-transform: uppercase;
  color: #808080;
  margin: 0.5em;
}
.services-tags:before {
  content: '';
  display: block;
  width: 100%;
  position: absolute;
  top: 0;
  height: 2px;
	background-color: #d6d6d6;
  -webkit-box-shadow: 1px 1px #fff, inset 1px 1px rgba(0,0,0,.17);
	-moz-box-shadow: 1px 1px #fff, inset 1px 1px rgba(0,0,0,.17);
	box-shadow: 1px 1px #fff, inset 1px 1px rgba(0,0,0,.17);
}
</style>
