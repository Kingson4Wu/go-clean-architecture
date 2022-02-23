此代码对应文章：Golang 简洁架构实战 https://www.luozhiyun.com/archives/640


<pre>
├── cmd/
│   └── main.go //启动函数
├── etc
│   └── dev_conf.yaml              // 配置文件
├── global
│   └── global.go //全局变量引用，如数据库、kafka等
├── internal/
│       └── service/
│           └── xxx_service.go //业务逻辑处理类
│           └── xxx_service_test.go
│       └── model/
│           └── xxx_info.go//结构体
│       └── api/
│           └── xxx_api.go//路由对应的接口实现
│       └── router/
│           └── router.go//路由
│       └── pkg/
│           └── datetool//时间工具类
│           └── jsontool//json 工具类
</pre>

<pre>
go run cmd/main.go 
# command-line-arguments
cmd/main.go:4:12: undefined: InitServer

该出错原因属于go的多文件加载问题，采用go run命令执行的时候，需要把待加载的.go文件都包含到参数里面。通过go run *.go(目录里面没有test.go才行)

(1)
cd main
go build
./cmd

(2)
cd main
go run *.go    
# command-line-arguments
./wire_gen.go:18:6: InitServer redeclared in this block
        /Users/kingsonwu/Personal/go-src/go-clean-architecture/cmd/wire.go:14:20: previous declaration

???        

</pre>