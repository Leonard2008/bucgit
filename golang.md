golang.org
$ mkdir $HOME/work
$ export GOPATH=$HOME/gitws/work
$ export PATH=$PATH:$GOPATH/bin

beego.me
go get github.com/astaxie/beego
~/gitws/work/src/....i/astaxie
go get github.com/beego/bee
~/gitws/work/src/..../bee

cd $GOPATH/src
bee new hello
cd hello
bee run
curl http://localhost:8080/


go build -o hello hello.go
--------------------



