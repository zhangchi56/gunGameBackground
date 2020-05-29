<template>
  <div>
      <!-- 面包屑导航区 -->
    <el-breadcrumb separator-class="el-icon-arrow-right">
      <el-breadcrumb-item :to="{ path: '/home' }">首页</el-breadcrumb-item>
      <el-breadcrumb-item>首页管理</el-breadcrumb-item>
      <el-breadcrumb-item>轮播图管理</el-breadcrumb-item>
    </el-breadcrumb>
      <router-link to='/swiper/addSwiper' style="color:#FFF"><el-button size="small" type="primary"> 添加图片 </el-button></router-link>
    <el-table :data="swiperList" border stripe>
      <!-- stripe: 斑马条纹
      border：边框-->
      <el-table-column type="index" label="#" align='center'></el-table-column>
      <el-table-column prop="swiper" label="轮播图"  align='center' width="180px">
        <template slot-scope="scope">
          <div>
            <img style="width:150px;" :src="scope.row.img" alt="">
            <!-- {{scope.row.img}} -->
          </div>
        </template>
      </el-table-column>
      <el-table-column prop="link" label="链接"  align='center'></el-table-column>
      <el-table-column prop="order" label="排序" width="80px"  align='center'></el-table-column>
      <!-- <el-table-column label="状态">
        <template slot-scope="scope">
          <el-switch v-model="scope.row.mg_state" @change="userStateChanged(scope.row)"></el-switch>
        </template>
      </el-table-column> -->
      <el-table-column label="操作" width="200px"  align='center'>
        <template slot-scope="scope">
          <el-button
            type="primary"
            icon="el-icon-edit"
            size="mini"
            @click="showEditDialog(scope.row)"
          >编辑</el-button>
          <el-button
            type="danger"
            icon="el-icon-delete"
            size="mini"
            @click="removeUserById(scope.row.id)"
          >删除</el-button>
        </template>
      </el-table-column>
    </el-table>
  </div>
</template>

<script>
/*eslint-disable*/
export default {
    data() {
        return {
            swiperList:[]
        }
    },
    created() {
        this.getSwiperList()
    },
    methods: {
      //获取轮播图数据列表
        getSwiperList(){
            this.swiperList = [
                {index:1,img:'http://d.wentushop.com//uploads/jpg/2020/04/fe8f5844-9900-42d4-a341-79943d006940.png',link:'http://d.wentushop.com//uploads/jpg/2020/04/fe8f5844-9900-42d4-a341-79943d006940.png',order:1},
                {index:1,img:'http://d.wentushop.com//uploads/jpg/2020/04/fe8f5844-9900-42d4-a341-79943d006940.png',link:'http://d.wentushop.com//uploads/jpg/2020/04/fe8f5844-9900-42d4-a341-79943d006940.png',order:1},
                {index:1,img:'http://d.wentushop.com//uploads/jpg/2020/04/fe8f5844-9900-42d4-a341-79943d006940.png',link:'http://d.wentushop.com//uploads/jpg/2020/04/fe8f5844-9900-42d4-a341-79943d006940.png',order:1},
                {index:1,img:'http://d.wentushop.com//uploads/jpg/2020/04/fe8f5844-9900-42d4-a341-79943d006940.png',link:'http://d.wentushop.com//uploads/jpg/2020/04/fe8f5844-9900-42d4-a341-79943d006940.png',order:1}
            ]
        },
        //编辑轮播图
        showEditDialog(obj){
          console.log(obj)
          this.$router.push({path:'/swiper/editSwiper',query:obj})
        }
    },
};
</script>

<style lang="less" scoped>

</style>