<template>
  <div class="content-body">
    <div class="header-content">
      <div class="title">Danh sách nhân viên</div>
      <div class="content-feature">
        <button
          id="btnAdd"
          class="m-btn m-btn-default"
          v-on:click="btnAddOnClick"
        >
          <div class="m-btn-icon icon-add"></div>
          <div class="btn-text">Thêm nhân viên</div>
        </button>
        <Details
          :isHide="isHideParent"
          @outIsHide="outIsHide"
          :dataEmployee="employeesTemp"
        />
      </div>
    </div>
    <div class="filter-bar">
      <div class="filter-left">
        <input
          id="txtSearchEmployee"
          class="icon-search input-search"
          type="text"
          placeholder="Tìm kiếm theo Mã, Tên hoặc Số điện thoại"
          v-model="textSearch"
        />
        <select
          id="cbxDepartment"
          fieldName="CustomerGroupName"
          fieldValue="CustomerGroupId"
          api="/api/customergroups"
          class="m-control"
          v-model="departmentId"
        >
          <option value="">
            Tất cả phòng ban
          </option>
          <option value="142cb08f-7c31-21fa-8e90-67245e8b283e">
            Văn phòng Marketting
          </option>
          <option value="7a0b757e-41eb-4df6-c6f8-494a84b910f4">
            Phong đào tạo công nghệ
          </option>
          <option value="17120d02-6ab5-3e43-18cb-66948daf6128">
            Phòng Nhân sự
          </option>
        </select>
        <select
          id="cbxPosition"
          fieldName="CustomerGroupName"
          fieldValue="CustomerGroupId"
          api="/api/customergroups"
          class="m-control"
          v-model="positionId"
        >
          <option value="">
            Tất cả vị trí
          </option>
          <option value="3700cc49-55b5-69ea-4929-a2925c0f334d">Giám đốc</option>
          <option value="25c6c36e-1668-7d10-6e09-bf1378b8dc91">
            Trưởng phòng
          </option>
          <option value="148ed882-32b8-218e-9c20-39c2f00615e8">
            Nhân viên
          </option>
        </select>
      </div>
      <div class="filter-right">
        <button id="btnRefresh" class="m-second-button m-btn-refresh"></button>
      </div>
    </div>
    <!-- <v-data-table
      :headers="headers"
      :items="desserts"
      :items-per-page="5"
      class="elevation-1"
    >
    </v-data-table> -->

    <div
      class="grid grid-employee el-table el-table--fit el-table--scrollable-y el-table--enable-row-hover el-table--enable-row-transition"
    >
      <table
        id="tbListData"
        cellspacing="0"
        cellpadding="0"
        border="0"
        class="el-table__body"
        style="min-width: 100%"
      >
        <thead class="has-gutter">
          <tr class="el-table__row">
            <th
              colspan="1"
              rowspan="1"
              class="el-table_30_column_114 is-leaf"
              fieldName="EmployeeCode"
            >
              <div class="cell">Mã nhân viên</div>
            </th>
            <th
              colspan="1"
              rowspan="1"
              class="el-table_30_column_115 is-leaf"
              fieldName="FullName"
            >
              <div class="cell">Họ và tên</div>
            </th>
            <th
              colspan="1"
              rowspan="1"
              class="el-table_30_column_116 is-leaf"
              fieldName="GenderName"
            >
              <div class="cell">Giới tính</div>
            </th>
            <th
              colspan="1"
              rowspan="1"
              class="el-table_30_column_116 is-leaf"
              fieldName="DateOfBirth"
              formatType="ddmmyyyy"
              style="text-align: center"
            >
              <div class="cell">Ngày sinh</div>
            </th>
            <th
              colspan="1"
              rowspan="1"
              class="el-table_30_column_116 is-leaf"
              fieldName="PhoneNumber"
            >
              <div class="cell">Điện thoại</div>
            </th>
            <th
              colspan="1"
              rowspan="1"
              class="el-table_30_column_116 is-leaf"
              fieldName="Email"
            >
              <div class="cell">Email</div>
            </th>
            <th
              colspan="1"
              rowspan="1"
              class="el-table_30_column_116 is-leaf"
              fieldName="PositionName"
            >
              <div class="cell">Chức vụ</div>
            </th>
            <th
              colspan="1"
              rowspan="1"
              class="el-table_30_column_116 is-leaf"
              fieldName="DepartmentName"
            >
              <div class="cell">Phòng ban</div>
            </th>
            <th
              colspan="1"
              rowspan="1"
              class="el-table_30_column_116 is-leaf"
              fieldName="Salary"
              formatType="Money"
            >
              <div class="cell" style="text-align: right">Mức lương cơ bản</div>
            </th>
            <th
              colspan="1"
              rowspan="1"
              class="el-table_30_column_116 is-leaf"
              fieldName="WorkStatusName"
            >
              <div class="cell">Tình trạng công việc</div>
            </th>
            <th class="gutter" style="width: 6px"></th>
          </tr>
        </thead>
        <tbody>
          <tr
            class="el-table__row"
            v-for="employee in getTextSearch"
            :key="employee.EmployeeId"
            @dblclick="rowOnClick(employee)"
          >
            <td>
              <div class="cell">{{ employee.EmployeeCode }}</div>
            </td>
            <td>
              <div class="cell">{{ employee.FullName }}</div>
            </td>
            <td>
              <div class="cell">{{ employee.GenderName }}</div>
            </td>
            <td>
              <div class="cell">{{ employee.DateOfBirth }}</div>
            </td>
            <td>
              <div class="cell">{{ employee.PhoneNumber }}</div>
            </td>
            <td>
              <div class="cell">{{ employee.Email }}</div>
            </td>
            <td>
              <div class="cell">{{ employee.PositionName }}</div>
            </td>
            <td>
              <div class="cell">{{ employee.DepartmentName }}</div>
            </td>
            <td>
              <div class="cell">{{ employee.Salary }}</div>
            </td>
            <td>
              <div class="cell">{{ employee.WorkStatusName }}</div>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
    <div class="paging-bar">
      <div class="paging-record-info">Hiển thị <b>1-10/1000</b> nhân viên</div>
      <div class="paging-option">
        <div class="btn-select-page m-btn-firstpage"></div>
        <div class="btn-select-page m-btn-prev-page"></div>
        <div class="m-btn-list-page">
          <button class="btn-pagenumber btn-pagenumber-selected">1</button>
          <button class="btn-pagenumber">2</button>
          <button class="btn-pagenumber">3</button>
          <button class="btn-pagenumber">4</button>
        </div>
        <div class="btn-select-page m-btn-next-page"></div>
        <div class="btn-select-page m-btn-lastpage"></div>
      </div>
      <div class="paging-record-option"><b>10</b> nhân viên/trang</div>
    </div>
    <transition
      name="fade"
      enter-active-class="animated slideInDown"
      leave-active-class="animated slideOutDown"
    >
      <div class="popup" v-if="isShowPopUp">
        <div class="popup_child">
          <h3>Edit User</h3>
          <p class="closePopUp" @click="closePopUp">x</p>
          <hr />
          <p>
            Lorem ipsum dolor sit amet consectetur adipisicing elit. Vitae
            voluptatum unde laboriosam eius incidunt nemo, magnam non eum
            obcaecati voluptatibus a saepe dolorum distinctio quidem praesentium
            deserunt dolore velit minima?
          </p>
          <div class="editUser">
            <button type="button" class="btn btn-danger">
              <i class="far fa-trash-alt"></i>
              Xóa
            </button>
            <button type="button" class="btn btn-warning" @click="isHowForm">
              <i class="fas fa-edit"></i>
              Sửa
            </button>
          </div>
        </div>
      </div>
    </transition>
  </div>
</template>
<script>
import * as axios from "axios";
import Details from "./EmployeeProfileDetail";
export default {
  name: "Employees",
  components: {
    Details,
  },
  methods: {
    btnAddOnClick() {
      this.isHideParent = !this.isHideParent;
    },
    rowOnClick(employee) {
      this.isShowPopUp = true;
      this.employeesTemp = employee;
    },
    outIsHide(e) {
      this.isHideParent = e;
      this.employeesTemp = {};
    },
    closePopUp() {
      this.isShowPopUp = false;
    },
    isHowForm() {
      this.closePopUp();
      this.isHideParent = !this.isHideParent;
    },
  },
  computed: {
    getTextSearch() {
      let filterPosition = this.positionId,
        filterDepartment = this.departmentId,
        filterText = this.textSearch;

      return this.employees.filter(function (item) {
        let filtered = true;
        if (filterPosition && filterPosition.length > 0) {
          filtered = item.PositionId == filterPosition;
        }
        if (filtered) {
          if (filterDepartment && filterDepartment.length > 0) {
            filtered = item.DepartmentId == filterDepartment;
          }
        }
        if (filtered) {
          if (filterText && filterText.length > 0) {
            filtered = item.FullName.toLowerCase().includes(filterText.toLowerCase()) || item.EmployeeCode.toLowerCase().includes(filterText.toLowerCase());
          }
        }
        return filtered;
      });
    },
  },
  data() {
    return {
      textSearch: "",
      isShowPopUp: false,
      employeesTemp: {},
      isHideParent: true,
      positionId: "",
      departmentId: "",
      selectedEmployee: {
        EmployeeId: 1,
        FullName: "Nguyễn Văn Mạnh",
      },
      employeeTemp: {},
      employees: [
        {
          EmployeeId: 1,
          FullName: "Nguyễn Văn Mạnh",
        },
        {
          EmployeeId: 2,
          FullName: "Nguyễn Văn Mạnh",
        },
        {
          EmployeeId: 3,
          FullName: "Nguyễn Văn Mạnh",
        },
      ],
      headers: [
        {
          text: "Mã nhân viên",
          align: "start",
          sortable: false,
          value: "EmployeeCode",
        },
        { text: "Họ và tên", value: "FullName", align: "end" },
        { text: "Ngày sinh", value: "DateOfBirth" },
        { text: "Giới tính", value: "GenderName" },
        { text: "Vị trí", value: "PositionName" },
        { text: "Phòng ban", value: "DepartmentName" },
        { text: "Địa chỉ Email", value: "Email" },
        { text: "Số điện thoại", value: "PhoneNumber" },
        { text: "Mức lương", value: "Salary" },
        { text: "Địa chỉ", value: "Address" },
        { text: "Trạng thái công việc", value: "WorkStatusName" },
      ],
      desserts: [
        {
          name: "Frozen Yogurt",
          calories: 159,
          fat: 6.0,
          carbs: 24,
          protein: 4.0,
          iron: "1%",
        },
        {
          name: "Ice cream sandwich",
          calories: 237,
          fat: 9.0,
          carbs: 37,
          protein: 4.3,
          iron: "1%",
        },
        {
          name: "Eclair",
          calories: 262,
          fat: 16.0,
          carbs: 23,
          protein: 6.0,
          iron: "7%",
        },
        {
          name: "Cupcake",
          calories: 305,
          fat: 3.7,
          carbs: 67,
          protein: 4.3,
          iron: "8%",
        },
        {
          name: "Gingerbread",
          calories: 356,
          fat: 16.0,
          carbs: 49,
          protein: 3.9,
          iron: "16%",
        },
        {
          name: "Jelly bean",
          calories: 375,
          fat: 0.0,
          carbs: 94,
          protein: 0.0,
          iron: "0%",
        },
        {
          name: "Lollipop",
          calories: 392,
          fat: 0.2,
          carbs: 98,
          protein: 0,
          iron: "2%",
        },
        {
          name: "Honeycomb",
          calories: 408,
          fat: 3.2,
          carbs: 87,
          protein: 6.5,
          iron: "45%",
        },
        {
          name: "Donut",
          calories: 452,
          fat: 25.0,
          carbs: 51,
          protein: 4.9,
          iron: "22%",
        },
        {
          name: "KitKat",
          calories: 518,
          fat: 26.0,
          carbs: 65,
          protein: 7,
          iron: "6%",
        },
      ],
    };
  },
  async created() {
    const response = await axios.get("http://api.manhnv.net/api/employees");
    this.employees = response.data;
    this.employeeTemp = response.data;
  },
};
</script>

<style scoped>
.grid-employee {
  margin-top: 10px;
  height: calc(100vh - 234px);
}

.el-avatar-employee {
  padding-top: 16px;
  padding-right: 16px;
}

.el-left {
  width: calc(100% - 180px);
}

.el-avatar-employee .el-avatar {
  border: 1px solid #ccc;
  width: 160px;
  height: 160px;
  margin: 0 auto;
  border-radius: 50%;
  cursor: pointer;
  /* background-image: url("/assets/img/default-avatar.jpg"); */
  background-repeat: no-repeat;
  background-position: center;
  background-size: cover;
}

.el-avatar-note {
  font-size: 12px;
}
.filter-left {
  display: flex;
}
.filter-left select {
  margin-left: 10px;
  margin-right: 10px;
}

.currency-for-input {
  position: absolute;
  right: 40px;
  line-height: 40px;
  font-style: italic;
}

#txtSearchEmployee {
  min-width: 300px;
}
/* --------------------------------------- */
.popup {
  position: fixed;
  top: 20px;
  width: 100%;
  height: 100%;
}
.popup_child[data-v-a72348a4] {
  background-color: #019160;
  width: 30%;
  margin-left: 20%;
  margin-top: 150px;
  border-radius: 10px;
  padding: 40px;
  font-size: 15px;
  position: relative;
  color: white;
}
.editUser {
  float: right;
}

.editUser button {
  margin-right: 20px;
  border-radius: 5px;
  padding: 7px;
  cursor: pointer;
  font-size: 15px;
  border: none;
  color: white;
}

button.btn.btn-danger {
  background-color: #ff0000db;
}

button.btn.btn-warning {
  background-color: yellow;
  color: black;
}
p.closePopUp {
  position: absolute;
  top: -10px;
  right: 15px;
  font-size: 20px;
  cursor: pointer;
}
</style>