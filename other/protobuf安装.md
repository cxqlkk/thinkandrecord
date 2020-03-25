#### protobuf 

 下载protobuf

cd  protobuf-3.5.0

###4. 设置编译目录

./configure --prefix=/usr/local/protobuf
/usr/local/protobuf/ 为自己配置的编译安装目录

###5. 安装
还是在解压的目录下进行

make
make install

#### golang protobuf 插件
go install google.golang.org/protobuf/cmd/protoc-gen-go


#### go-micro
 protoc --proto_path=.  --go_out=plugins=micro:logs  protodemo/message.proto 
