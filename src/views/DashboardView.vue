<template>
  <div class="dashboard">
    <div class="stats">
      <div class="stat-card">
        <h2>Departments</h2>
        <p>{{ departmentCount }}</p>
      </div>
      <div class="stat-card">
        <h2>Employees</h2>
        <p>{{ employeeCount }}</p>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";
import employeeService from "@/services/employee.service.js";
import departmentService from "@/services/department.service.js";

// Khai báo biến để lưu số lượng phòng ban và nhân viên
const departmentCount = ref(0);
const employeeCount = ref(0);

// Hàm lấy số lượng phòng ban
const fetchDepartmentCount = async () => {
  try {
    const response = await departmentService.getDepartments();
    departmentCount.value = response.data.length;
  } catch (error) {
    console.error("Error fetching department count:", error);
  }
};

// Hàm lấy số lượng nhân viên
const fetchEmployeeCount = async () => {
  try {
    const response = await employeeService.getEmployees();
    employeeCount.value = response.data.length;
  } catch (error) {
    console.error("Error fetching employee count:", error);
  }
};

// Khi component được render, lấy dữ liệu
onMounted(() => {
  fetchDepartmentCount();
  fetchEmployeeCount();
});
</script>

<style scoped>
.dashboard {
  padding: 20px;
  font-family: Arial, sans-serif;
}

.stats {
  display: flex;
  gap: 20px;
  margin-top: 20px;
}

.stat-card {
  background: #f5f5f5;
  padding: 20px;
  border-radius: 8px;
  text-align: center;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.stat-card h2 {
  margin: 0;
  font-size: 18px;
  color: #333;
}

.stat-card p {
  margin: 10px 0 0;
  font-size: 24px;
  font-weight: bold;
  color: #007bff;
}
</style>
