<template>
  <div>
    <el-carousel indicator-position="outside" :autoplay=flag type="card"> 
      
      <el-carousel-item v-for="item in img" :key="item">
        <img :src=item alt="" width="100%" height="100%">
      </el-carousel-item>
    </el-carousel>
    <div v-for="(item, index) in data" :key="index" :style="{ width:width[index] , height:height[index] ,display:'inline-block'}">
      {{item.title}}--{{index}}
      <img :src="item.thumburl" alt="">
      
    </div>
    
  </div>
  
</template>

<script>
export default {
    data () {
      return {
        img:[],
        flag:false,
        data:[],
        width:[],
        height:[]
      }
    },
    mounted () {
      this.axios.get("/apis/open/tupian.json")
      .then(res =>{
        console.log(this.width)
        var that = this
        console.log(res.data)
        res.data.map(function(item ,index){
          that.img.push(item.thumburl)
          that.data.push(item)
          that.width.push(item.width+'px')
          that.height.push((20+item.height*1)+'px')
        })
        
      }).catch(err => (console.log(err)))
    }
}
</script>

<style>
  .el-carousel__item h3 {
    color: #475669;
    font-size: 18px;
    opacity: 0.75;
    line-height: 300px;
    margin: 0;
  }
  
  .el-carousel__item:nth-child(2n) {
    background-color: #99a9bf;
  }
  
  .el-carousel__item:nth-child(2n+1) {
    background-color: #d3dce6;
  }
</style>

