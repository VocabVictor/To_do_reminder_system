<template>
  <el-container class="container">
    <el-header>
      <el-row>
        <el-col :span="21">
          <span>我的日程</span>
          <el-dropdown>
            <el-button type="primary">
              更多菜单<i class="el-icon-arrow-down el-icon--right"></i>
            </el-button>
            <el-dropdown-menu slot="dropdown">
            </el-dropdown-menu>
          </el-dropdown>
        </el-col>
        <el-col :span="2">
          <el-button type="text" icon="el-icon-plus" @click="plus"></el-button>
        </el-col>
        <el-col :span="1">
          <el-button type="text" icon="el-icon-more" @click="more"></el-button>
        </el-col>
      </el-row>
    </el-header>
    <el-main>
      <el-image :src="image">
      </el-image>
      <div class="thy-empty-extra">
        <span translate="calendar.NO_EVENT_PLEASE_CLICK_ADD" class="text-desc">当前暂无日程，点击 </span>
        <el-button type="text">创建日程</el-button>
      </div>
    </el-main>
  </el-container>
</template>
<script>

export default {
  data() {
    return {
      value: new Date(),
      notLabel: [],
      label: [],
      loading: true,
      image:require("@/assets/images/calender.svg")
    };
  },
  computed: {},
  created() {
    this.$nextTick(() => {
      // 点击上个月
      let prevBtn = document.querySelector(
        ".el-calendar__button-group .el-button-group>button:nth-child(1)"
      );
      prevBtn.addEventListener("click", () => {
        this.value = this.moment(this.value).format("YYYY-MM");
        console.info(this.value);
        this.handleSchedule();
      });
      // 点击今天
      let currBtn = document.querySelector(
        ".el-calendar__button-group .el-button-group>button:nth-child(2)"
      );
      currBtn.addEventListener("click", () => {
        this.value = this.moment(this.value).format("YYYY-MM");
        console.info(this.value);
        this.handleSchedule();
      });
      // 点击下个月
      let nextBtn = document.querySelector(
        ".el-calendar__button-group .el-button-group>button:nth-child(3)"
      );
      nextBtn.addEventListener("click", () => {
        this.value = this.moment(this.value).format("YYYY-MM");
        console.info(this.value);
        this.handleSchedule();
      });
    });
  },
  mounted() {
    this.handleSchedule();
    console.log(this.label);
  },
  methods: {
    // 添加日程
    handleAdd() {
      this.$refs.canlendarDialog.handleOpen();
    },
    // 添加成功
    handleSuccess() {
      // 添加日程成功后去刷新列表
      this.handleSchedule();
    },
    handleSelected(day) {
      let flag = "1";
      this.label.forEach((item) => {
        if (item == day) {
          flag = "2";
          return;
        }
      });
      return flag;
    },
    // 获取当月的日程信息
    handleSchedule() {
      // 将日期传入接口，判断当前时间是否有日程
      getScheduleList(this.moment(this.value).format("YYYY-MM"))
        .then((res) => {
          if (res.code == 0) {
            // this.label.push(res.data);
            this.label = res.data.map((item) => {
              return item.scheduleDate;
            });
            this.notLabel = res.data;
            this.loading = false;
          }
        })
        .catch();
    },
    // 点击
    clickCalendar(day) {
      this.notLabel.forEach((item) => {
        if (item.scheduleDate == day.day) {
          // 展示日程
          this.$refs.canlendarDialog.handleOpen(item);
        }
      });
    },
  },
};
</script>
<style scoped>
.cal {
  width: 100%;
  height: 100%;
}

.cal ::v-deep.el-calendar-day .calendar_nolabel {
  margin: 0 auto;
  padding: 2px;
  text-align: center;
}
.cal ::v-deep.el-calendar-day .calendar_label {
  border: 1px solid #F93937;
  border-radius: 50%;
  width: 23px;
  margin: 0 auto;
  padding: 2px;
  text-align: center;
}

.add-canlendar {
  width: 90%;
  height: 35px;
  line-height: 13px;
  background: #409eff;
  color: #fff;
  margin-top: 5px;
}

.el-header .el-row{
  display: flex;
  flex-grow: 1;
  width: 100%;
}

.el-col{
  display: flex;
  align-items: center;
}

.el-main{
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}
</style>
