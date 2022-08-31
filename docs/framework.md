# DDD框架的文件包结构

DDD涉及众多的概念，Golang有自己的文件与包的组织形式。go-ddd框架的文件与包的结构组织形式应该是什么样的，需要汲取两者的能力进行融合。

## 架构设计
### 基于context拆分微服务
### 依赖倒置
> 面向抽象设计而不是面向实现设计     

infrastructure 仅提供 interface, 代码组织如下：
```go
package repo

type interface Repo{
    List() any
    GetByPK() any
}

// 工厂方法返回接口类型对象，实现抽象。
func RepoFactory() Repo{
    //any init code
    r := newsqlRepo()
    return r
}

// Repo 实现
type sqlRepo struct {
    dbConn any
}


type newsqlRepo() *sqlRepo{
    return &sqlRepo{dbConn: any}
}

// List 实现
func (s *sqlRepo)List() any {return nil}
```

### Facade vs Adapter


### 需要注意的点

#### 粗粒度 vs 细粒度
拆分的过细粒度，对于一些业务逻辑比较简单的 context，可能会过于冗余。但是我们同时也希望简单的业务在架构上保持一致。所以在生成脚手架的时候，需要支持简单的框架生成。