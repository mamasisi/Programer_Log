# Go Module 包管理
- 视频 https://www.bilibili.com/video/av91313893/

- 参考
    - [Go Modules 不完全教程](https://learnku.com/go/t/33859)
    - [Break up go project into subfolders](https://stackoverflow.com/questions/23154898/break-up-go-project-into-subfolders)
        - 很有用-GitHub 代码 https://github.com/J7mbo/go-subdirectories-with-modules
    - GitHub
        - https://github.com/jasonkeene/go-modules-demo
        - 非常详细 https://github.com/go-modules-by-example/index

- 总结
    - 同一个文件夹内只能存在一个package，否则编译时会报错。
        - go的package不局限于一个文件，可以由多个文件组成。
    - 同一个文件夹内的所有文件，所有变量或函数可以互相调用，不分大小写，不得同名
    - 子文件夹，也是不同的package ，也可互相导入
    - go不要求package的名称和所在目录名相同，但是你最好保持相同，否则容易引起歧义。因为引入包的时候，go会使用子目录名作为包的路径，而你在代码中真正使用时，却要使用你package的名称。
    - package与文件夹名相同

- 与Python的区别
    - Python通过文件名py来管理导入
    - GO通过package来管理导入

- demo 文件夹
    - 创建模块
        - go mod init a
        - 生成go.mod
    - 运行程序 go run .
    - a.go
        - package main
        - 使用a2.go的变量，直接调用
            - fmt.Println("a2.go abc2:", abc2)
        - 使用dir1/b.go的变量
            - 变量名要大写
            - import "a/dir1"
            - fmt.Println("dir1/b.go bbb1:", dir1.bbb1)
    - a2.go
        - package main
            - 不能用其他包名 package xxx 会报错
        - 变量 var abc2 = 2343
    - dir1
        - b.go
            - 不需要创建模块go.mod
            - package dir1
            - 变量 var bbb1 = "b.go bbb1"
                - 变量名要大写
        - b2.go
            - package dir1
            - 函数名第一个字母，大写func T1() 
            - 使用dir2/d2.go的变量
                - import "a/dir2"
                - fmt.Println("dir2/d2.go ddd2:", dir2.ddd2)
    - dir2
        - d2.go
            - package dir2
            - 变量 var ddd2 = "d2.go ddd2"