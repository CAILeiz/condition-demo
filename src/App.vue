<template>
  <div>
    <h2 v-if="curModelOpts.showApk">apk 上传</h2>
    <h2 v-if="curModelOpts.showWL">围栏</h2>
    <el-form
      :label-position="labelPosition"
      label-width="80px"
      :model="curModelOpts.form"
    >
      <el-form-item
        :label="itm.label"
        v-for="(itm, index) in curModelOpts.formL"
        :key="index"
      >
        <div v-if="itm.type === 'input'">
          <el-input v-model="curModelOpts.form[itm.name]"></el-input>
        </div>
        <div v-else-if="itm.type === 'select'">
          <el-select v-model="curModelOpts.form[itm.name]" placeholder="请选择">
            <el-option
              v-for="item in itm.options"
              :key="item.value"
              :label="item.label"
              :value="item.value"
            >
            </el-option>
          </el-select>
        </div>
        <div v-else-if="itm.type === 'time'">
          <el-input v-model="curModelOpts.form[itm.name]"></el-input>
        </div>
      </el-form-item>
      <el-button @click="formCommit">提交</el-button>
    </el-form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      labelPosition: "left",
      formLabelAlign: {
        name: "",
        region: "",
        type: "",
      },
      curModelOpts: {},
    };
  },
  created() {
    this.curModelOpts = this.getModelOpts();
  },
  methods: {
    formCommit() {
      console.log(this.curModelOpts.form);
    },
    getModelOpts(id = "") {
      return {
        showApk: true,
        showWL: true,
        formL: [
          {
            type: "select",
            label: "区域选择",
            name: "area",
            options: [
              {
                label: "北京",
                value: 100,
              },
              {
                label: "南京",
                value: 1001,
              },
            ],
          },
          {
            type: "input",
            label: "app数量",
            name: "count",
          },
          {
            type: "time",
            label: "时间选择",
            name: "time",
          },
        ],
        form: {
          area: "",
          count: "",
          time: "",
        },
      };
    },
  },
};
</script>

<style lang="less">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>
