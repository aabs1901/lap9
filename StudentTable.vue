<template>
<div>
     <div class="card student-list m-2 p-2">
         <h4 class="card-title">Student</h4>
         <div class="edit-table-toggle form-check">
            <input id="edit-table" type="checkbox" class="form-check-input" v-model="editTable">
            <label for="edit-table" class="form-check-label">Edit table? </label>
            </div>
         <div id="student-table">
             <table class="table">
                 <tr>
                     <th>Name</th>
                     <th>StarID</th>
                     <th>Present?</th>
                     <th v-show="editTable">Delete</th>
                 </tr>
                 <tr class="student-row" v-for="student in students" v-bind:key="student.name" v-bind:class="'present-'+ student.present">
                     <td>{{ student.name}}</td>
                     <td>{{student.starID}}</td>
                     <td><input type="checkbox" v-model="student.present" v-on:change="checked(student)"></td>
                </tr>
                <StudentRow
                   v-for="student in students" v-bind:key="student.name"
                   v-bind:student="student"
                   v-bind:edit="editTable"
                   v-on:student-persent="studentArrivedOrLeft"
                   v-on:delete-student="studentDeleted">
                  
                   
                </StudentRow>
             </table>
         </div>
    </div>
         
</div>     
    
</template>

<script>
import StudentRow from '@/components/StudentRow.vue'

// export
export default {
    name: 'StudentTable',
    componets: {StudentRow},
    data() {
        return {
            editTable:false
        }
    },
    props: {
        students: Array
    },
    methods: {
        studentArrivedOrLeft(student){
            this.$emit('student-present',student)
        },
        studentDeleted(student) {
            this.$emit('delete-student',student)
        }

        }
    }
    

    

</script>
<style >
.present-true {
    color: #31f300;
    font-style: italic;
}
.present-false {
    color: black;
    font-weight: bold;
}
</style>

