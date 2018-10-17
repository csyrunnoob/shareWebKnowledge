# vue优化参考 #
1.频繁隐藏显示采用v-show,否则采用v-if  
2.v-for循环时，绑定唯一key时数据有唯一ID时绑定数据的唯一ID值,如若没有绑定index值（尽量避免绑定index）  
3.当某个组件过于庞大时 拆分组件  
4.尽量减少watch的数据  
5.组件样式加上scoped 例如：`<style scoped></style>`  
6.router建议使用懒加载，例如：resolve => require(['pages/home/Home'], resolve)  
7.vuex管理状态过多时采用modules模块化方案  
8.data中对象确定不会在添加修改属性时用Object.freeze冻结数据