<template>
  <ElCard class="form-card">
    <ElForm :model="formData"
            label-position="top"
            :rules="rules"
            ref="addItemForm"
            >
      <ElFormItem label="Type"
                  prop="type">
        <ElSelect v-model="formData.type"
                  placeholder="Choose type..."
                  class="type-select"
        >
          <ElOption label="Income" value="INCOME"/>
          <ElOption label="Outcome" value="OUTCOME"/>
        </ElSelect>
      </ElFormItem>
      <ElFormItem label="Comments" prop="comment">
        <ElInput v-model="formData.comment"/>
      </ElFormItem>
      <ElFormItem label="Value" prop="value">
        <ElInput v-model.number="formData.value"/>
      </ElFormItem>
      <ElButton type="primary" @click="onSubmit">Submit</ElButton>
    </ElForm>
  </ElCard>
</template>

<script>
export default {
  name: "Form",
  data() {
    return {
      formData: {
        type: 'INCOME',
        comment: '',
        value: 0
      },
      rules: {
        type: [
          {
            required: true,
            message: 'Please select type',
            trigger: 'blur'
          }
        ],
        comment: [
          {
            required: true,
            message: 'Please write a comment',
            trigger: 'blur'
          }
        ],
        value: [
          {
            required: true,
            message: 'Please input value',
            trigger: 'change'
          },
          {
            type: "number",
            message: 'Value must be a number',
            trigger: 'change'
          }
        ]
      }

    }
  },
  methods: {
    onSubmit() {
      this.$refs.addItemForm.validate(valid => {
        if (valid) {
          this.$emit('submitForm', { ...this.formData }
          );
          this.$refs.addItemForm.resetFields();
        }
      })
    }
  }
}
</script>

<style scoped>
  .form-card {
    max-width: 500px;
    margin: auto;
  }

  .type-select {
    width: 100%;
  }
</style>