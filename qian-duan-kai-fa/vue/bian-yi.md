# 编译

### parse

使用正则解析template中的Vue指令变量等，形成语法树AST

### optimize

标记一些静态节点，用作后续的性能优化，在diff的时候直接略过

### generate

把语法树AST转化为渲染函数 render function

