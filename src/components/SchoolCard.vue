<!--
描述：高校主页用于搜索时显示的学校卡片
作者：蔡明宏
-->
<template>
  <div class="school_card">
    <!-- 排名小卡片 -->
    <el-card class="rank_card">
      <div class="rank_text">
        <div>{{ school.university_qs_rank }}</div>
        <div>{{ school.university_the_rank }}</div>
        <div>{{ school.university_usnews_rank }}</div>
      </div>
    </el-card>

    <el-card class="two_block hover_card" >
      <div class="two_block_hori">
        <div>
          <div class="avatar_text">
            <el-avatar shape="square" :size="70" :src="school.university_badge" />
            <div>
                <p class="enname">{{ school.university_enname }}</p>
                <p class="chname">{{ school.university_chname }}</p>
              
            </div>
          </div>
          <!-- 下面主要介绍在校人数、位置、简介 -->
          <div>
              <div style="margin:10px;"> 
                <el-row :gutter="10" justify="space-around">
                  <el-col :span="8">
                    <div >
                      <span class="info_text">在校人数:</span>
                      <span style="color:gray;">{{school.university_student_num}}</span>
                    </div>
                  </el-col>
                  <el-col :span="8">
                    <div>
                      <span class="info_text">位置：</span>
                      <span style="color:gray;">{{school.university_location}}</span>
                    </div>
                  </el-col>
                  <el-col :span="8">
                    <div>
                      <span class="info_text">学费：</span>
                      <span style="color:gray;">{{school.university_tuition}}</span>
                    </div>
                  </el-col>
                </el-row>
                </div>

                <div>
                    <span class="info_text">简介：</span>
                    <span style="color:gray;">{{school.university_introduction}}</span>
                </div>
              
          </div>
        </div>

        <!-- 右侧点击去看看 -->
        <div class="myButton">
          <div>
          <el-button type="warning" size="large" color="#626aef" @click="modifySchool"
            >修改</el-button
          >
          </div>
          <div>
          <el-button type="danger" size="large"  @click="delete_dialog_visible = true"
            >删除</el-button
          >
          </div>
        </div>
      </div>
    </el-card>
    <el-dialog
      v-model="delete_dialog_visible"
      title="警告"
      width="30%"
      :before-close="handleClose"
    >
      <span style="font-size:18px">你确认要删除该大学信息吗? 此操作不可逆!</span>
      <template #footer>
        <span class="dialog-footer">
          <el-button @click="delete_dialog_visible = false">取消</el-button>
          <el-button type="primary" @click="deleteSchool">确认</el-button>
        </span>
      </template>
    </el-dialog>
  </div>
</template>

<script>
export default {
  props: ["school"],
  data() {
    return {
      delete_dialog_visible: false,
    };
  },
  methods: {
    modifySchool() {
      // <router-link target="_blank" :to="{path:'/home',query:{id:'1'}}">新页面打开home页</router-link>;
      this.$router.push({
        path: "/modify_school_detail",
        query: {
          school_id: this.school.university_id,
        },
      });
    },
    handleClose() {
      this.delete_dialog_visible = false;
    },
    deleteSchool(){
    //   console.log("1111");
    //   axios.delete(
    //     '/identity', {	
    //   params: {	// 请求参数拼接在url上
    //     identity_id: this.certif_infor.identity_id,
    //   }
    // })
    //   .then((res) => {
    //     this.delete_dialog_visible = false;
    //     console.log(res);
    //     if (res.data.status == true){
    //       ElMessage.success("删除成功!");
    //       this.$emit("deletecheck",true);
    //       this.need_refresh = !this.need_refresh;
    //     }else {
    //       ElMessage.error("删除失败!");
    //     }
    //   })
    //   .catch((errMsg) => {
    //     console.log(errMsg);
    //   });
    }
  },
};
</script>

<style>
.myButton {
  display: flex;
  flex-direction: column; /* 按照列(反方向)排列*/
  justify-content: space-around;
}
.hover_card:hover {
  border: #61acf6 0.2em solid;
}
.school_card {
  margin: 20px;
  width: 90%;
  height: 20%;
  display: flex;
  justify-content: center;
}
.rank_card {
  padding: 30px; /* 调整上下间距的 */
  margin: 30px;
  width: 20%;
  height: 30%;
  vertical-align: middle;
}
.rank_text {
  color: coral;
  font-size: 25px;
  vertical-align: middle;
  display: flex;
  justify-content: space-between;
}
.two_block {
  /* margin-left: 20px; */
  padding: 10px;
  height: 20%;
  width: 60%;
}
.two_block_hori {
  display: flex;
  justify-content: space-between;
}
.avatar_text {
  display: flex;
}
p.enname {
  color: rgb(57, 47, 65);
  font-family: "Lucida Console", "Courier New", monospace;
  font-size: 20px;
  margin-left: 30px;
  margin-top: 10px;
}
p.chname {
  color: dimgray;
  font-family: "Times New Roman", Times, serif;
  float: left;
  margin-top: -10px;
  margin-left: 30px;
}
span.info_text {
  font-family: Arial, Helvetica, sans-serif;
  font-size: 18px;
  color: rgb(121, 75, 75);
}
</style>
