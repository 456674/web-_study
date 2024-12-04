<template>
  <el-form @submit.prevent="onSubmit">
    <el-form-item>
      <el-input
          v-model="label"
          placeholder="What needs to be done?"
          clearable
      ></el-input>
    </el-form-item>
    <el-form-item>
      <el-button style="width: 100%" type="primary" @click="onSubmit">Add</el-button>
    </el-form-item>
  </el-form>
</template>

<script>
export default {
  data() {
    return {
      label: ""
    };
  },
  methods: {
    onSubmit() {
      if (this.label === "") {
        return;
      }
      this.$emit("todo-added", this.label);
      this.label = "";
    }
  }
};
</script>
