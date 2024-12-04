<template>
  <el-checkbox
      :label="label"
      v-model="localDone"
      @change="handleCheckboxChange"
      class="todo-item"
  >
    {{ label }}
  </el-checkbox>
</template>

<script>
export default {
  props: {
    label: String,
    done: Boolean,
    id: Number
  },
  data() {
    return {
      localDone: this.done
    };
  },
  watch: {
    done(newVal) {
      this.localDone = newVal;
    }
  },
  methods: {
    handleCheckboxChange() {
      this.$emit('checkbox-changed', this.localDone);
    }
  }
};
</script>

<style scoped>
.todo-item {
  margin: 10px 0;
  font-size: 16px;
  color: #333;
}

.todo-item .el-checkbox {
  --el-checkbox-size: 20px; /* 增大复选框的大小 */
}

.todo-item .el-checkbox__input.is-checked + .el-checkbox__label {
  text-decoration: line-through;
  color: #999;
}
</style>
