<template>
  <div id="app" class="small-container">
    <h1>Employees</h1>

    <employee-form @add:employee="addEmployee"/>
    <employee-table
                  :employees="employees"
                  @delete:employee="deleteEmployee"
                  @edit:employee="editEmployee"
    />
    <Flavor />
    <DisplayFlavor />
  </div>
</template>

<script>
  import EmployeeForm from '@/components/EmployeeForm.vue'
  import EmployeeTable from '@/components/EmployeeTable.vue'
  import Flavor from '@/components/Flavor.vue'
  import DisplayFlavor from '@/components/DisplayFlavor.vue'

  export default {
    name: 'app',
    components: {
      EmployeeForm,
      EmployeeTable,
      Flavor,
      DisplayFlavor
    },
    data () {
      return {
        employees: [
          {
          id: 1,
          name: 'Richard Hendricks',
          email: 'richard@piedpiper.com',
          },
          {
            id: 2,
            name: 'Bertram Gilfoyle',
            email: 'gilfoyle@piedpiper.com',
          },
          {
            id: 3,
            name: 'Dinesh Chugtai',
            email: 'dinesh@piedpiper.com',
          },
        ],
      }
    },
    methods: {
      addEmployee(employee) {
        console.log('reading event from employee form');
        const lastId = this.employees.length > 0
                      ? this.employees[this.employees.length - 1].id
                      : 0;
        const id = lastId + 1;
        const newEmployee = { ...employee, id};

        this.employees = [...this.employees, newEmployee];
        //this.employees.push(employee);
      },

      deleteEmployee(id) {
        this.employees = this.employees.filter(
          employee => employee.id !== id
        );
      },

      editEmployee(id, updatedEmployee) {
        this.employees = this.employees.map(employee =>
          employee.id === id ? updatedEmployee : employee
        )
      },

    },
  }
</script>

<style>
  button {
   background: #009435;
   border: 1px solid #009435;
 }

 .small-container {
   max-width: 680px;
 }
</style>
