# element����֤

## ͨ������el-date-picker���ѡȡ����ʱ��ȿ�ʼʱ�����ٶ�һ�������ѡ��

```
<template>
	<el-form :model="form" :rules="rules" ref="form">
		<el-row>
			<el-col :span="23" :offset="1">
				<el-form-item label="��ʼ���ڣ�" prop="startTime">
                                         <el-date-picker
                                             v-model="startTime"
                                             type="date"
                                             placeholder="ѡ��ʼ����"
                                             :picker-options="pickerOptions0"
                                            @change='handlePurchaseStartTime' clearable>
                                         </el-date-picker>
				</el-form-item>
                                <el-form-item label="�������ڣ�" prop="endTime">
                                        <el-date-picker
                                            v-model="endTime"
                                            type="date"
                                            placeholder="ѡ���������"
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
            message: "��ѡ��ʼ����",
            trigger: "change"
          }
        ],
        endTime: [
          {
            required: true,
            message: "��ѡ���������",
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

## ͨ������el-input�������������
``` 
<template>
	<el-form :inline="true" :model="form" ref="form" :rules="rules">
		<el-row>
			<el-col :span="7" :offset="1">
				<el-form-item label="������䣺" prop="amountInterval">
					<el-form-item label="" prop="minVal">
						<el-input v-model="form.minVal" placeholder="��������Сֵ" style="width:150px" @change="handleMinValChange"></el-input>
					</el-form-item>
					��
					<el-form-item label="" prop="maxVal">
						<el-input v-model="form.maxVal" placeholder="���������ֵ" style="width:150px" @change="handleMaxValChange"></el-input>
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
						return callback(new Error('����ֵ�������0'));
					}
					return callback();
				}
				return callback(new Error('����ֵ����Ϊ����'));
			}
			let validateMin = (rule, value, callback)=>{
				const one = Number(value);
				const max = Number(this.form.maxVal);
				if (!max || one < max) {
					return callback();
				}
				return callback(new Error('��Сֵ���ô������ֵ'));
			}
			let validateMax = (rule, value, callback)=>{
				const one = Number(value);
				const min = Number(this.form.minVal);
				if (!min || one > min) {
					return callback();
				}
				return callback(new Error('���ֵ����С����Сֵ'));
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
