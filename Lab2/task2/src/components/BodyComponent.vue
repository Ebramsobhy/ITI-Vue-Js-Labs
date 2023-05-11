<template>
  <div>
    <table class="table table-striped table-bordered w-100 text-center mt-3">
      <thead>
        <tr>
          <th>ID</th>
          <th>Name</th>
          <th>City</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="student in students" :key="student.id">
          <td>{{student.id}}</td>
          <td>{{student.name}}</td>
          <td>{{student.city}}</td>
        </tr>
      </tbody>
      <tfoot>
        <tr>
          <th colspan="3"> Number Of Students {{students.length}}</th>
        </tr>
      </tfoot>
    </table>
    <button class="btn btn-primary" @click="openModal">Add Student</button>
    
    <div class="modal" :class="{'d-block': isModalOpen}">
      <div class="modal-dialog" >
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title">Add Student</h5>
          </div>
          <div class="modal-body">
            <form ref="addStudentForm" @submit.prevent="addStudent">
              <div class="form-group">
                <label for="student-name" class="col-form-label">Name:</label>
                <input type="text" class="form-control" id="student-name" v-model="studentName">
              </div>
              <div class="form-group">
                <label for="city-name" class="col-form-label">City:</label>
                <input type="text" class="form-control" id="city-name" v-model="cityName">
              </div>
            </form>
          </div>
          <div class="modal-footer">
            <button type="button" class="btn btn-primary" @click="addStudent">Add</button>
            <button type="button" class="btn btn-secondary"  @click="closeModal">Cancel</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import students from '../students'

export default {
  data: () => ({
    studentName:'',
    cityName:'',
    students: students,
    isModalOpen: false,
  }),
  methods: {
    openModal() {
      this.isModalOpen = true
    },
    closeModal() {
      this.isModalOpen = false
    },
    addStudent() {
      this.isModalOpen = false;
      const name = this.studentName;
      const city = this.cityName;
      const id = this.students.length > 0 ? this.students[this.students.length - 1].id + 100 : 100;
      this.students.push({ id, name, city });
    }
  }
}
</script>

<style>

</style>
