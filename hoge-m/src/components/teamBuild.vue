<template>
  <div style="font-size: .2rem">
    <header align="center">
      <div>{{title}}</div>
      <span @click="$router.go(-1)"><img src="./../assets/images/public/left.jpg" alt="" title="back"></span>
    </header>
    <!--<div style="height: .3rem;"></div>-->
    <yd-lightbox :num="list.length">
        <yd-lightbox-img v-for="item in list" width="48%" height="50%" style="float:left;padding:1%;" :src="item.host+item.dir+item.filepath+item.filename" ></yd-lightbox-img>

      <yd-lightbox-txt>
        <!--<yd-lightbox-img v-for="item in list" width="100%" height="100%" :src="item.src" :original="item.original1" ></yd-lightbox-img>-->
        <!--<yd-lightbox-txt>-->
        <h1 style="font-size: .2rem;color:white;" slot="top">{{title}}</h1>
        <div class="image-content" style="font-size: .2rem;color:white;" slot="content">
          <p>{{time}}</p>
        </div>
      </yd-lightbox-txt>
    </yd-lightbox>
  </div>
</template>
<script>
  export default {
    data () {
      return {
        title: '加载中…',
        time: '',
        id: this.$route.query.id,
        list: []
      }
    },
    mounted () {
      let that = this
      console.log(this.id)
//      setTimeout(() => {
//        this.list = [
//          {src: 'http://static.ydcss.com/uploads/lightbox/meizu_s1.jpg', original1: 'http://static.ydcss.com/uploads/lightbox/meizu_1.jpg'},
//          {src: 'http://static.ydcss.com/uploads/lightbox/meizu_s2.jpg', original1: 'http://static.ydcss.com/uploads/lightbox/meizu_2.jpg'},
//          {src: 'http://static.ydcss.com/uploads/lightbox/meizu_s3.jpg', original1: 'http://static.ydcss.com/uploads/lightbox/meizu_3.jpg'},
//          {src: 'http://static.ydcss.com/uploads/lightbox/meizu_s4.jpg', original1: 'http://static.ydcss.com/uploads/lightbox/meizu_4.jpg'},
//          {src: 'http://static.ydcss.com/uploads/lightbox/meizu_s5.jpg', original1: 'http://static.ydcss.com/uploads/lightbox/meizu_5.jpg'},
//          {src: 'http://static.ydcss.com/uploads/lightbox/meizu_s6.jpg', original1: 'http://static.ydcss.com/uploads/lightbox/meizu_6.jpg'}
//        ]
//      }, 10)
      this.$http.get('http://www.hoge.cn/m2o/pub/content.php?id=' + this.id)
        .then(function (response) {
          that.title = response.data[0].title
          that.time = response.data[0].publish_time
          that.list.length = 0
          that.list = response.data[0].childs_data
//          Array.prototype.push.apply(that.list, response.data[0].childs_data)
          console.log(that.list)
        })
        .catch(function (err) {
          console.log(err)
        })
    }
  }
</script>
<style scoped>
  header {
    height: .88rem;
    width: 100%;
    font-size: .36rem;
    text-align: center;
  }

  header > div {
    padding-left:.7rem;
    padding-right:.7rem;
    position: relative;
    top: .26rem;
    height: .36rem;
    font-size: .36rem;
    line-height: .36rem;
    overflow: hidden;
    white-space: nowrap;
    text-overflow: ellipsis;
  }

  header > span {
    display: block;
    height: .36rem;
    width: .21rem;
    position: absolute;
    top: .26rem;
    left: .24rem;
  }

  header > span  img {
    width: 100%;
    height: 100%;
  }
</style>
