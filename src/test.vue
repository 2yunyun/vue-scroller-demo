<template>
  <div class="wraper" @scroll="onScroll($event)">
    <div class="item" v-for="item in items">
      {{item}}
    </div>
  </div>
</template>
 
<script>
export default {
  data () {
    return {
      items:[],
      pgSize:36,
      rawItems:[],
      pgNo:1
    }
  },
  
  ready () {
    for(var i=0;i<=1000;i++){
      this.rawItems.push(i)
    }
    this.changePgItems()
  },
  methods:{
    onScroll(event){
      var offsetHeight = event.currentTarget.offsetHeight,
      scrollHeight = event.target.scrollHeight,
      scrollTop = event.target.scrollTop,
      scrollBottom = offsetHeight + scrollTop
      if(scrollTop===0)
      {
        if(this.pgNo===1)
        {
          return
        }
        this.pgNo--
        this.changePgItems()
        event.target.scrollTop=offsetHeight-1
      }
      if(scrollBottom===scrollHeight || scrollBottom===scrollHeight+2)
      {
        if(this.pgNo==Math.ceil(this.rawItems.length/this.pgSize))
        {
          return
        }
        this.pgNo++
        this.changePgItems()
        event.target.scrollTop=1
      }
    },
    changePgItems(){
      var start = (this.pgNo-1) * this.pgSize,
      items = this.rawItems.slice(start,this.pgSize+((this.pgNo-1)*this.pgSize))
      this.items = items
    }
  }
}
 
 
</script>
 
<style lang="less">
 
.wraper{
  border:1px solid red;
  height:100vh;
  overflow-y: auto;
  box-sizing: border-box;
 
 
  .item{
    height: 30px;
    border-bottom: 1px solid #ccc;
  }
}
</style>