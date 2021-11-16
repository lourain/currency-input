<template>
  <div>
    <el-input style="width: 300px;" @input="inputFormat" :value="monthlyIncome" maxlength="19"></el-input>
  </div>
</template>
<script>
export default {
    data() {
        return {
            monthlyIncome: ''
        }
    },
    methods: {
      inputFormat(val) {
        const reg = /[^\d]/g;
        if (reg.test(val)) {
          this.monthlyIncome = val;
          // 去除非数字的字符，给一个延迟200ms（体验）
          setTimeout(() => {
            const temp = val.replace(reg, "");
            if (temp) {
              this.monthlyIncome = Number(temp).toThousands();
            } else {
              this.monthlyIncome = temp;
            }
          }, 200);
          return;
        }
        if (val.includes(".")) {
          const temp = val.replace(/\./g, "");
          this.monthlyIncome = Number(temp).toThousands();
        } else {
          // 当val值为空时候 直接return
          if (val === "") {
            this.monthlyIncome = "";
            return;
          }
          this.monthlyIncome = Number(val).toThousands();
        }
      },
    },
}
</script>