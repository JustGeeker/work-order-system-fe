/*
 * @Author: Skye Young
 * @Date: 2019-11-12 21:48:02
 * @Last Modified by: Skye Young
 * @Last Modified time: 2019-11-26 22:06:50
 */

<template>
  <div>
    <header>
      <h2>部门成员管理</h2>
    </header>
    <main @mousewheel.stop>
      <what-table
        :columns="columns"
        :dataSource="tableData"
        :options="options"
        :pagination="pagination"
        :fetch="fetchData"
      ></what-table>
      <edit-user
        :user-data="userData"
        :is-visible="editUserIsVisible"
        @toggle-is-visible="toggleEditUser"
      ></edit-user>
    </main>
  </div>
</template>

<script lang="ts">
import Vue from "vue";
import WhatTable from "@/components/Etc/WhatTable.vue";
import EditUser from "./Edit.vue";
import { AxiosResponse } from "axios";

interface UserData {
  dtpId: number;
  dptname: string;
  name: string;
  worknum: string;
  gender: string;
  birthday: string;
  enterTime: string;
  phone: string;
  techTittle: string;
  eduBgd: string;
  degree: string;
  school: string;
  major: string;
  doubleTeacher: number;
  background: number;
  tutor: number;
  permission: number;
}

export default Vue.extend({
  components: {
    WhatTable,
    EditUser
  },
  data() {
    return {
      editUserIsVisible: false,
      userData: {},
      tableData: [],
      columns: [
        {
          prop: "name",
          label: "姓名",
          width: 120
        },
        {
          prop: "gender",
          label: "性别",
          width: 60
        },
        {
          prop: "worknum",
          label: "工号"
        },
        {
          prop: "phone",
          label: "联系电话"
        },
        {
          prop: "techTittle",
          label: "职称"
        },
        {
          button: true,
          label: "操作",
          width: 200,
          group: [
            {
              // you can props => type size icon disabled plain
              name: "编辑",
              type: "warning",
              icon: "el-icon-edit",
              plain: true,
              onClick: (userData: UserData, index: number) => {
                // 箭头函数写法的 this 代表 Vue 实例
                this.$data.userData = userData;
                this.$data.editUserIsVisible = true;
              }
            }
          ]
        }
      ],
      options: {
        mutiSelect: false,
        mutiSelectFixed: false,
        index: true, // 显示序号
        indexFixed: false,
        loading: false, // 表格动画
        initTable: true // 是否一挂载就加载数据
      },
      pagination: {
        total: 0,
        pageIndex: 1,
        pageSize: 20
      }
    };
  },
  methods: {
    fetchData() {
      this.options.loading = true;

      this.$http
        .post(
          "/api/online/collegeAdmin/getDptUserInfo",
          // "/api/userTableData",
          {
            page: this.pagination.pageIndex,
            size: this.pagination.pageSize
          },
          {
            headers: {
              token: this.$store.state.userInfo.token
            }
          }
        )
        .then((res: AxiosResponse) => {
          if (res.data.code === 0) {
            const { list, total } = res.data.data;
            this.tableData = list;
            this.pagination.total = total;
          } else {
            this.$message({
              message: res.data.msg || "由于未知因素，无法获取表格",
              type: "warning"
            });
          }
          this.options.loading = false;
        })
        .catch(() => {
          this.$message({
            message: "由于未知因素，无法获取表格",
            type: "warning"
          });
          this.options.loading = false;
        });
    },
    toggleEditUser(isVisible: boolean) {
      if (typeof isVisible === "undefined") {
        this.editUserIsVisible = !this.editUserIsVisible;
      } else {
        this.editUserIsVisible = isVisible;
      }
    }
  }
});
</script>

<style lang="scss" scoped>
header,
main {
  margin-left: 15px;
}
</style>

<style scoped>
div >>> .el-table {
  max-height: 65vh !important;
}

div >>> .el-table__body-wrapper,
div >>> .el-table__fixed-body-wrapper {
  height: 58vh !important;
}
</style>
