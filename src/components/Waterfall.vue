<template>
  <div class="waterfall" ref="waterfall" @scroll="_scroll">
    <el-row>
      <el-col class="water_col" :span="4" v-for="(item, index) in waterList" :key="index">
        <el-card :body-style="{ padding: '10px', height: '100%', width: '100%', boxSizing: 'border-box' }" shadow="hover">
          <img :src="item.src" class="water_image">
          <div class="water_desc">
            <span>{{item.name}}</span>
            <div class="bottom clearfix">
              <time class="time">{{item.title}}</time>
            </div>
          </div>
        </el-card>
      </el-col>
    </el-row>
    <img @click="backTop" class="backToTop" src="/static/images/OA_backToTop.png" alt="返回顶部">
  </div>
</template>
<script>
  import { mapState, mapActions, mapMutations } from 'vuex'
  export default {
    data () {
      return {}
    },
    computed: {
      ...mapState({
        waterList: state => state.WaterFall.imagesList
      })
    },
    methods: {
      ...mapActions([
        'reqImagesDate'
      ]),
      ...mapMutations([
        'clearWaterFallData'
      ]),
      backTop () {
        this.$refs.waterfall.scrollTop = 0
      },
      _scroll () {
        if ((event.currentTarget.scrollHeight - event.currentTarget.clientHeight) === (event.currentTarget.scrollTop)) {
          this.reqImagesDate()
          return
        }
      }
    },
    created() {
      this.reqImagesDate()
    },
    beforeDestroy() {
      this.clearWaterFallData()
    }
  }
</script>
<style lang="less" scoped>
  .waterfall {
    height: 100%;
    width: 100%;
    overflow-x: hidden;
    overflow-y: auto;
    .water_col {
      height: 400px;
      width: 300px;
      margin: 10px;
      .el-card {
        height: 100%;
        width: 100%;
        .el-card__body {
          img {
            height: 330px;
            margin-bottom: 10px;
          }
          .water_desc {
            span {
              color: #000;
            }
            .bottom {
              margin-top: 10px;
              color: #aaaaaa;
            }
          }
        }
      }
    }
    .water_image {
      height: 100%;
      width: 100%;
    }
    .backToTop {
      position: fixed;
      right: 20px;
      bottom:20px;
      height: 40px;
      width: 40px;
    }
  }
</style>
