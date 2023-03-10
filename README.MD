https://zhuanlan.zhihu.com/p/501843416


① 安装protoc编译器

protobuf编译器就叫protoc

到下面github地址，根据自己的系统版本选择下载，解压缩安装即可。

https://github.com/protocolbuffers/protobuf/releases
例如3.9.2版本压缩包介绍：

protoc-3.9.2-win64.zip - windows 64版本
protoc-3.9.2-osx-x86_64.zip - mac os 64版本
protoc-3.9.2-linux-x86_64.zip - linux 64版本
解压缩安装包之后，将 [安装目录]/bin 目录，添加到PATH环境变量。

② 安装编译器go语言插件

因为目前的protoc编译器，默认没有包含go语言代码生成器，所以需要单独安装插件。

go get -u github.com/golang/protobuf/protoc-gen-go
【/Users/bbt/.gvm/pkgsets/go1.20.1/global/bin/protoc-gen-go】


1. 建立目录 proto 创建文件 helloworld.proto

2. 编译proto协议文件
上面通过proto定义的接口，没法直接在代码中使用，因此需要通过protoc编译器，将proto协议文件，编译成go语言代码。
protoc -I proto/ --go_out=plugins=grpc:proto proto/helloworld.proto

-I 指定代码输出目录，忽略服务定义的包名，否则会根据包名创建目录
--go_out 指定代码输出目录，格式：--go_out=plugins=grpc:目录名
命令最后面的参数是proto协议文件
编译成功后在proto目录生成了helloworld.pb.go文件，里面包含了，我们的服务和接口定义。

遇到问题：protoc导出时遇到protoc-gen-go unable to determine Go import path解决方法
http://www.kaotop.com/it/909233.html

proto文件添加 option go_package ="../pb";
或生成在proto文件目录  option go_package ="../proto";




3. 实现服务端代码
文件:helloworld/server.go

go run server.go


4. 实现客户端代码
文件：helloworld/client.go
go run client.go



----------------
php grpc

protoc --proto_path=examples/protos \
  --php_out=examples/php/route_guide \
  --grpc_out=examples/php/route_guide \
  --plugin=protoc-gen-grpc=bins/opt/grpc_php_plugin \
  ./examples/protos/route_guide.proto



protoc --proto_path=examples/protos \
  --php_out=examples/php/route_guide \
  --grpc_out=examples/php/route_guide \
  --plugin=protoc-gen-grpc=bins/opt/grpc_php_plugin \
  ./examples/protos/helloword.proto  
