# element表单验证

## 通过两个el-date-picker组件选取结束时间比开始时间至少多一天的联级选择

```
<template>
	<el-form :model="form" :rules="rules" ref="form">
		<el-row>
			<el-col :span="23" :offset="1">
				<el-form-item label="开始日期：" prop="startTime">
                                         <el-date-picker
                                             v-model="startTime"
                                             type="date"
                                             placeholder="选择开始日期"
                                             :picker-options="pickerOptions0"
                                            @change='handlePurchaseStartTime' clearable>
                                         </el-date-picker>
				</el-form-item>
                                <el-form-item label="结束日期：" prop="endTime">
                                        <el-date-picker
                                            v-model="endTime"
                                            type="date"
                                            placeholder="选择结束日期"
                                            :picker-options="pickerOptions1"
                                            @change='handlePurchaseEndTime' clearable>
                                        </el-date-picker>
				</el-form-item>
		       </el-col>
	       </el-row>
	</el-form>	
</template>
<script>
export default {
  data() {
    return {
      form: {
        startTime: "",
        endTime: ""
      },
      rules: {
        startTime: [
          {
            required: true,
            message: "请选择开始日期",
            trigger: "change"
          }
        ],
        endTime: [
          {
            required: true,
            message: "请选择结束日期",
            trigger: "change"
          }
        ]
      },
      pickerOptions0: {
        disabledDate: time => {
          if (this.endTime != "") {
            return time.getTime() > this.endTime - 24 * 60 * 60 * 1000;
          }
        }
      },
      pickerOptions1: {
        disabledDate: time => {
          if (this.startTime != "") {
            return time.getTime() < this.startTime + 24 * 60 * 60 * 1000;
          }
        }
      }
    };
  },
  methods: {
    handlePurchaseStartTime(value) {
      this.startTime = value.getTime();
      this.form.startTime = this.formatDateTime(value);
    },
    handlePurchaseEndTime(value) {
      this.endTime = value.getTime();
      this.form.endTime = this.formatDateTime(value);
    },
    formatDateTime(inputTime) {
      var date = new Date(inputTime);
      var y = date.getFullYear();
      var m = date.getMonth() + 1;
      m = m < 10 ? "0" + m : m;
      var d = date.getDate();
      d = d < 10 ? "0" + d : d;
      return y + "-" + m + "-" + d;
    }
  }
};
</script>
```

## 通过两个el-input组件输入金额区间
``` 
<template>
	<el-form :inline="true" :model="form" ref="form" :rules="rules">
		<el-row>
			<el-col :span="7" :offset="1">
				<el-form-item label="金额区间：" prop="amountInterval">
					<el-form-item label="" prop="minVal">
						<el-input v-model="form.minVal" placeholder="请输入最小值" style="width:150px" @change="handleMinValChange"></el-input>
					</el-form-item>
					至
					<el-form-item label="" prop="maxVal">
						<el-input v-model="form.maxVal" placeholder="请输入最大值" style="width:150px" @change="handleMaxValChange"></el-input>
					</el-form-item>
				</el-form-item>
			</el-col>
		</el-row>
	</el-form>
</template>
<script>
	export default {
		data () {
			let validateCom = (rule, value, callback)=>{
				console.log(6666)
				if(!isNaN(value)){
					const one = Number(value);
					if (one < 0) {
						return callback(new Error('输入值必须大于0'));
					}
					return callback();
				}
				return callback(new Error('输入值必须为数字'));
			}
			let validateMin = (rule, value, callback)=>{
				const one = Number(value);
				const max = Number(this.form.maxVal);
				if (!max || one < max) {
					return callback();
				}
				return callback(new Error('最小值不得大于最大值'));
			}
			let validateMax = (rule, value, callback)=>{
				const one = Number(value);
				const min = Number(this.form.minVal);
				if (!min || one > min) {
					return callback();
				}
				return callback(new Error('最大值不得小于最小值'));
			}
			return {
				form: {
					minVal:'',
					maxVal:''
				},
				rules: {
					minVal: [
						{ validator: validateCom, trigger: 'blur' },
						{ validator: validateMin, trigger: 'blur' },
					],
					maxVal: [
						{ validator: validateCom, trigger: 'blur' },
						{ validator: validateMax, trigger: 'blur' },
					]
				}
			}
		},
		methods: {
			handleMinValChange(){
				this.$refs.form.validateField("minVal");
			},
			handleMaxValChange(){
				this.$refs.form.validateField("maxVal");
			}
		}
	}
</script>
```
