# gateway
- use golang write a gateway router (use [GIN](https://github.com/gin-gonic/gin) enginer, if use [fasthttp](https://github.com/valyala/fasthttp); fasthttp don't support http2,[issue](https://github.com/valyala/fasthttp/issues/45)); 
- support limit rate, filter, aggregation, fusing, loadbalancing(swrr/hash), health check ... etc; 
- like those -> [krakend](https://github.com/devopsfaith/krakend) 、 [gateway](https://github.com/fagongzi/gateway)、use go kit [go-kit](https://github.com/go-kit/kit), [go-micro](https://github.com/micro/go-micro)

## micro-service tradeoff from [this video](https://www.youtube.com/watch?v=JXEjAwNWays) and [this video](https://www.youtube.com/watch?v=NX0sHF8ZZgw&t=1401s) 
<div align="center"><img src="https://raw.githubusercontent.com/weegate/gateway/master/solve-cause.png" width="100%" height="100%"></div>
<div align="center"><img src="https://raw.githubusercontent.com/weegate/gateway/master/solved.png" width="100%" height="100%"></div>
<div align="center"><img src="https://raw.githubusercontent.com/weegate/gateway/master/caused.png" width="100%" height="100%"></div>
<div align="center"><img src="https://raw.githubusercontent.com/weegate/gateway/master/caused1.png" width="100%" height="100%"></div>
<div align="center"><img src="https://raw.githubusercontent.com/weegate/gateway/master/know-more.png" width="100%" height="100%"></div>

## 总体框框
<div align="center"><img src="https://raw.githubusercontent.com/weegate/gateway/master/gateway.png" width="100%" height="100%"></div>

## 请求处理框框(context)
- 实现设计上可以参考有赞的[网关设计](https://tech.youzan.com/api-gateway-in-practice/)
- 对请求的上下文，以pipeline(pipe链)的处理方式处理；根据后端微服务定义的处理模块(mw)串起来处理请求;
- pipe链(责任链)的形式，和nginx的请求处理流程类似，如果采用[lua-nginx-module](https://github.com/openresty/lua-nginx-module)开发网关，通过请求处理的不同阶段[指令块](https://github.com/openresty/lua-nginx-module#directives)进行相应的处理；nginx自带实现了负载均衡(hash,rr,wrr,swrr)，backpoint后端服务健康检查(tcp/http)


## 参考阅读 
> Notice: 学习了，还需要提炼出来，形成自己的行为模式，之乎者也就过了
- [SOA和微服务的区别](https://www.zhihu.com/question/37808426)
- [微服务、SOA 和 API：是敌是友？](https://www.ibm.com/developerworks/cn/websphere/library/techarticles/1601_clark-trs/1601_clark.html)
- [集成架构发展](https://www.ibm.com/developerworks/cn/websphere/library/techarticles/1503_clark/1305_clark.html)（SOA的缘来）
- [nginx+](https://www.nginx.com/products/nginx/) (基础功能服务借鉴使用)
- [HTTP1.\*和http2区别](https://www.zhihu.com/question/34074946)
- [Istio](https://istio.io/) An open platform to connect, manage, and secure microservices （k8s 自动化运维部署监控 punning）
