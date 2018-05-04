<template>
  <div class="wrap-per">
    <el-row class="wrap-per disb">
      <el-row type="flex" class="wrap-per" justify="center" align="middle" >
        <el-col :span="10">
          <h1 class="box-title">{{ msg }}</h1>
          <el-card class="box-card">
            
            <el-form :rules="rules2" ref="ruleForm2" status-icon :model="formData" label-width="60px">
              <el-form-item label="账号:" prop="userName">
                <el-input v-model="formData.userName" auto-complete="off"></el-input>
              </el-form-item>
              <el-form-item label="密码:" prop="pass">
                <el-input type="password" v-model="formData.pass" auto-complete="off"></el-input>
              </el-form-item>
              <el-form-item label="验证码:" prop="verifCode" >
                <el-row type="flex" class="hello" justify="center" align="middle" >
                  <el-input v-model="formData.verifCode"></el-input>
                  <img src="http://testcds.heroenglish.net/captcha.html" style="margin-left: 10px"/>
                </el-row>
              </el-form-item>
              <el-form-item>
                <el-button type="primary" @click="submitForm('ruleForm2')"> {{loginState}} </el-button>
                <el-button>取消</el-button>
              </el-form-item>
            </el-form>
          </el-card>
        </el-col>
      </el-row>
    </el-row>

    <el-row class="wrap-per">
      <el-row type="flex" class="wrap-per" justify="center" align="middle" >
        <el-col :span="8">
          <el-card class="box-card">
            <div class="logoWrap">
              <img src="https://forms.wechatify.com/Content/images/S&PEventRegistration.jpg"/>
            </div>
            <el-form :rules="rules_sp" ref="ruleForm_sp" status-icon :model="formData_sp" >
              <el-form-item prop="userName">
                <el-input v-model="formData_sp.userName" auto-complete="off"></el-input>
              </el-form-item>
              <el-form-item prop="pass">
                <el-input type="password" v-model="formData_sp.pass" auto-complete="off"></el-input>
              </el-form-item>
              <el-form-item style="text-align:right">
                <el-button>Cancel</el-button>
                <el-button type="danger" @click="submitForm_sp('ruleForm_sp')"> {{loginState1}} </el-button>
              </el-form-item>
            </el-form>
          </el-card>
        </el-col>
      </el-row>
    </el-row>
  </div>
</template>

<script>
export default {
  name: "Login",
  data() {

    var validatePass = (rule, value, callback) => {
      console.log(value);
      if (value === "") {
        callback(new Error("请输入密码"));
      } else {
         console.log(value,1);
        // if (this.form.pass !== "") {
        //   this.$refs.form.validateField("checkPass");
        // }
        callback();
      }
    };
    var validateVerifyCode = (rule, value, callback) => {
      console.log(value);
      if (value === "") {
        callback(new Error("请输入验证码"));
      } else {
         console.log(value,1);
        callback();
      }
    };
    var validateName = (rule, value, callback) => {
      console.log(value);
      if (value === "") {
        callback(new Error("请输入姓名"));
      } else {
         console.log(value,1);
        callback();
      }
    };

    var validatePass_sp = (rule, value, callback) => {
      console.log(value);
      if (value === "") {
        callback(new Error("请输入密码-sp"));
      } else {
         console.log(value,1);
        // if (this.form.pass !== "") {
        //   this.$refs.form.validateField("checkPass");
        // }
        callback();
      }
    };
    var validateName_sp = (rule, value, callback) => {
      console.log(value);
      if (value === "") {
        callback(new Error("请输入姓名-sp"));
      } else {
         console.log(value,1);
        callback();
      }
    };

    return {
      msg: "CDS 后台管理系统",
      loginState: '登录',
      loginState1: 'Submit',
      formData: {
        userName: '',
        pass: '',
        verifCode: '',
      },
      formData_sp: {
        userName: '',
        pass: '',
      },
      rules2: {
        userName: [
          { validator: validateName, trigger: 'blur' }
        ],
        pass: [
          { validator: validatePass, trigger: 'blur' }
        ],
        verifCode: [
          { validator: validateVerifyCode, trigger: 'blur' }
        ],
      },
      rules_sp: {
        userName: [
          { validator: validateName_sp, trigger: 'blur' }
        ],
        pass: [
          { validator: validatePass_sp, trigger: 'blur' }
        ],
      }
    };
  },
  methods: {
    submitForm(formName) {
      this.beforeSubmit();
      this.$refs[formName].validate(valid => {
        if (valid) {
          alert("submit!");
          console.log('submit!',this.formData.userName,this.formData_sp.pass,
          this.formData_sp.verifCode); 
          // this.$router.push({name: 'HomePage'});
          this.$router.push({ path: '/' })
          this.$refs[formName].resetFields(); 
        } else {
          console.log("error submit!!");
          return false;
        }
      });
    },
    submitForm_sp(formName) {
      this.beforeSubmit();
      this.$refs[formName].validate(valid => {
        if (valid) {
          alert("submit!");
          console.log('submit!',this.formData_sp.userName,this.formData.pass,this.formData.verifCode); 
          this.$router.push({ path: '/' })
          this.$refs[formName].resetFields(); 
        } else {
          console.log("error submit!!");
          return false;
        }
      });
    },
    resetForm(formName) {
      this.$refs[formName].resetFields();
    },
    // onSubmit() {
    //   this.beforeSubmit();
    //   console.log('submit!',this.formData.userName,this.formData.pass,this.formData.verifCode);
    //   this.$router.push({name: 'HomePage'})
    // },
    beforeSubmit: function(){
      this.isDisabled = true
      this.loginState = "正在登录..."
    },
    beforeRouteEnter (to, from, next) {
      console.log("00000")
      next(vm => {
        if (vm.userName != "") {
          // next({ path: '/' })
          vm.$router.push({name:'HomePage'})
        } else {
          next()
        }
      })
    },
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1,
h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}


.box-title {
  text-align: center;
}

.box-card {
  /* padding: 20px 5px; */
}

.wrap-per{
  height: 100%;
}

.logoWrap {
  max-width: 300px;
  margin: 10px auto 30px auto;
}

.disb {
  display: none;
}


.logoWrap img {
  max-width: 100%;;
  margin: 0 auto;
  height: auto;
  display: block;
}
</style>
