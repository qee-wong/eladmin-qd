<template>
  <el-dialog :append-to-body="true" :visible.sync="dialog" :title="isAdd ? '新增' : '编辑'" width="500px">
    <el-form ref="form" :model="form" :rules="rules" size="small" label-width="80px">
      <el-form-item label="employeeid">
        <el-input v-model="form.employeeid" style="width: 370px;"/>
      </el-form-item>
      <el-form-item label="电话">
        <el-input v-model="form.phone" style="width: 370px;"/>
      </el-form-item>
      <el-form-item label="姓名">
        <el-input v-model="form.name" style="width: 370px;"/>
      </el-form-item>
      <el-form-item label="是否签到">
        <el-input v-model="form.sign" style="width: 370px;"/>
      </el-form-item>
      <el-form-item label="昵称">
        <el-input v-model="form.nickname" style="width: 370px;"/>
      </el-form-item>
      <el-form-item label="avatarurl">
        <el-input v-model="form.avatarurl" style="width: 370px;"/>
      </el-form-item>
      <el-form-item label="性别">
        <el-input v-model="form.gender" style="width: 370px;"/>
      </el-form-item>
      <el-form-item label="openid">
        <el-input v-model="form.openid" style="width: 370px;"/>
      </el-form-item>
      <el-form-item label="updatetime">
        <el-input v-model="form.updatetime" style="width: 370px;"/>
      </el-form-item>
      <el-form-item label="留言">
        <el-input v-model="form.signMessage" style="width: 370px;"/>
      </el-form-item>
      <el-form-item label="等级">
        <el-input v-model="form.dengji" style="width: 370px;"/>
      </el-form-item>
      <el-form-item label="标记">
        <el-input v-model="form.biaoji" style="width: 370px;"/>
      </el-form-item>
      
    </el-form>
    <div slot="footer" class="dialog-footer">
      <el-button type="text" @click="cancel">取消</el-button>
      <el-button :loading="loading" type="primary" @click="doSubmit">确认</el-button>
    </div>
  </el-dialog>
</template>

<script>
import { add, edit } from '@/api/userTest'
export default {
  props: {
    isAdd: {
      type: Boolean,
      required: true
    },
    sup_this: {
      type: Object,
      default: null
    }
  },
  data() {
    return {
      loading: false, dialog: false,
      form: {
        id: '',
        employeeid: '',
        phone: '',
        name: '',
        sign: '',
        nickname: '',
        avatarurl: '',
        gender: '',
        openid: '',
        updatetime: '',
        dengji: '',
        biaoji: '',
        avatarUrl: '',
        signMessage: ''
      }
    }
  },
  methods: {
    cancel() {
      this.resetForm()
    },
    doSubmit() {
      this.loading = true
      if (this.isAdd) {
        this.doAdd()
      } else this.doEdit()
    },
    doAdd() {
      add(this.form).then(res => {
        this.resetForm()
        this.$notify({
          title: '添加成功',
          type: 'success',
          duration: 2500
        })
        this.loading = false
        this.$parent.$parent.init()
      }).catch(err => {
        this.loading = false
        console.log(err.response.data.message)
      })
    },
    doEdit() {
      edit(this.form).then(res => {
        this.resetForm()
        this.$notify({
          title: '修改成功',
          type: 'success',
          duration: 2500
        })
        this.loading = false
        this.sup_this.init()
      }).catch(err => {
        this.loading = false
        console.log(err.response.data.message)
      })
    },
    resetForm() {
      this.dialog = false
      this.$refs['form'].resetFields()
      this.form = {
        id: '',
        employeeid: '',
        phone: '',
        name: '',
        sign: '',
        nickname: '',
        avatarurl: '',
        gender: '',
        openid: '',
        updatetime: '',
        dengji: '',
        biaoji: '',
        avatarUrl: '',
        signMessage: ''
      }
    }
  }
}
</script>

<style scoped>

</style>
