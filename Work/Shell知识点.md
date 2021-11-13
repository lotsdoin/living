# Shell 知识点

## find 
* 查找项目所用到的头文件
`find . -name ".[ch]" | xargs grep "#include" | sort | uniq`
