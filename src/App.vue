<template>
  <div id="app">
    <div>
    <el-form :model="ruleForm" :rules="rules" ref="ruleForm" label-width="120px" class="demo-ruleForm">
    
    <!-- input for first name -->
    <el-form-item label="First Name" prop="name1"> <br>
    <el-input placeholder="Please input" v-model="ruleForm.name1"></el-input></el-form-item>

     <!-- input for last name -->
    <el-form-item label="Last Name" prop="name2"> <br>
    <el-input placeholder="Please input" v-model="ruleForm.name2"></el-input></el-form-item> 
    </el-form>

    <!-- input for email -->
    <el-form :model="dynamicValidateForm" ref="dynamicValidateForm" label-width="120px" class="demo-dynamic">
    <el-form-item
      prop="email"
      label="Email"
      :rules="[
      { required: true, message: 'Email address is required', trigger: 'blur' },
      { type: 'email', message: 'Please input correct email address', trigger: ['blur', 'change'] }
      ]"
    > <br>
    <el-input placeholder="Please input" v-model="dynamicValidateForm.email"></el-input>
    </el-form-item>
    </el-form>

    <!-- create checkbox for agreement -->
    <el-form :model="ruleForm" :rules="rules" ref="ruleForm" label-width="120px" class="demo-ruleForm">
    <el-form-item label="Agreement" prop="type">
    <el-checkbox v-model="ruleForm.type" label="Do you agree to let us contact you?"></el-checkbox>
    </el-form-item>

    <!-- input for subject title -->
    <el-form-item label="Claim Title" prop="title"> <br>
    <el-input placeholder="Please input" v-model="ruleForm.name3"></el-input></el-form-item>

    <!-- textarea for a claim request content -->
    <el-form-item label="Claim Request" prop="textarea"> <br>
    <el-input
      type="textarea"
      :rows="2"
      placeholder="Please input"
      v-model="textarea">
    </el-input>
    </el-form-item>

      <!-- button to submit -->
    <el-button type="primary" @click="dialogVisible = true">Submit</el-button>
    

      <!-- popup (dialog) to confirm the content -->
    <el-dialog
    title="Confirmation"
    :visible.sync="dialogVisible"
    width="30%"
    :before-close="handleClose">
    <span>Are you sure to submit this claim? 
      First name 
      Last name
      Email
      Claim title 
      Claim content
       </span>
    <span slot="footer" class="dialog-footer">
    <el-button @click="dialogVisible = false">Cancel</el-button>
    <el-button type="primary" @click="dialogVisible = false">Confirm</el-button>
  </span>
</el-dialog>
</el-form>
    </div>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'app',
  components: {
    HelloWorld
  },

  data() {
    return {
    ruleForm: {
          name1: '',
          name2: '',   
          type: [],  
          title: '',
          textarea: ''
    },
    rules: {
          name1: [
            { required: true, message: 'First Name is required', trigger: 'blur' },
            { min: 3, max: 5, message: 'Length should be 3 to 5', trigger: 'blur' }
          ],
           name2: [
            { required: true, message: 'Last Name is required', trigger: 'blur' },
            { min: 3, max: 5, message: 'Length should be 3 to 5', trigger: 'blur' }
          ],
          type: [
            { type: 'array', required: true, message: 'Agreement is required', trigger: 'change' }
          ],
          title: [
            { required: true, message: 'Claim title is required', trigger: 'blur' },
            { min: 1, message: 'Length should be 3 to 10', trigger: 'blur' }
          ],
          textarea: [
            { required: true, message: 'Claim Request is required', trigger: 'blur' },
            { min: 1, max: 5, message: 'Length should be 3 to 100', trigger: 'blur' }
          ],
        },

      // input Email
      dynamicValidateForm: {
          email: '',
      },

      dialogVisible: false
      }
     },

    methods: {submitForm(formName) {
        this.$refs[formName].validate((valid) => {
          if (valid) {
            alert('submit!');
          } else {
            console.log('error submit!!');
            return false;
          }
        });
      },
      resetForm(formName) {
        this.$refs[formName].resetFields();
      }
    },

methods: {
      handleClose(done) {
        this.$confirm('Are you sure to close this dialog?')
          .then(_ => {
            done();
          })
          .catch(_ => {});
      }
    }

}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: left;
  color: #2c3e50;
  margin: 100px;
}

</style>
