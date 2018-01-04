<template>
    <div class="vertical-list">
        <ul>
            <li v-if="list.length" v-for="item in list" v-bind:key="item.id">
                <img v-bind:src="item.imageUrl">
                <a v-bind:href="item.url">{{item.title}}</a>
                <div class="meta-info">
                    date created: {{item.dateAdded}}
                </div>
            </li>
            <li v-if="!list.length" class="empty">Loading data...</li>
        </ul>
    </div>
</template>


<script>
import axios from 'axios';

export default {
  title: 'VerticalList',
  props: ['subreddit'],
  data() {
    return {
      list: [],
    };
  },
  created() {
    this.updateData();
  },
  methods: {
   /*  getImgUrl: (item) => {
      if (item.imgUrl && item.preview.images.length) {
        return item.preview.images[0].source.url;
      }
      return 'https://vignette.wikia.nocookie.net/theamazingworldofgumball/images/e/ec/Reddit_Logo.png/revision/latest?cb=20170105232917';
    }, */

    updateData(subreddit) {
      let url;
      this.list = [];
      if (subreddit) {
        url = `https://www.reddit.com/r/${subreddit}.json`;
      } else {
        url = 'http://localhost:3020/graphql';
      }
      return axios
        .post(url, {
          query: `
            query {
              allLinks {
                title
                imageUrl
                url
                dateAdded
              }
            }  
        `})
        .then(response => response.data.data.allLinks)
        .then((parsed) => {
          this.list = parsed;
        });
    },
  },
  watch: {
    subreddit(newVal, oldVal) {
      // watch it
      this.updateData(newVal);
    },
  },
};
</script>

<style>
li {
  list-style: none;
  height: 65px;
  border-bottom: 1px solid silver;
  text-align: left;
  margin: 5px;
  padding: 5px;
  display: block;
  font-size: 1.2em;
  position: relative;
}
li.empty {
  border: none;
}
li div.meta-info {
  font-size: 0.8em;
  font-weight: bold;
  position: absolute;
  bottom: 10px;
  left: 70px;
}

li a {
  text-decoration: none;
  color: darkslategrey;
  line-height: 1.3em;
  padding-left: 5px;
}
li img {
  float: left;
  width: 50px;
  height: 50px;
}
</style>