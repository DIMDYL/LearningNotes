## 什么是nacos

nacos是用于管理微服务注册中心，调配新服务和检测服务的是否还运行

## 服务注册

在服务启动的时候都应该将自己的启动信息提交到Nacos中，这个动作称为服务注册

配置完成启动项目，在Nacos中服务列表中就能查看到启动的服务

#### 依赖

``` xml
<dependency>
    <groupId>com.alibaba.cloud</groupId>
    <artifactId>spring-cloud-starter-alibaba-nacos-discovery</artifactId>
</dependency>
```

#### 配置

```yml
spring:
  application:
    name: item-service # 服务名称
  cloud:
    nacos:
      server-addr: 127.0.0.1:8848 # nacos服务地址
```

## 服务发现

``` xml
<dependency>
    <groupId>com.alibaba.cloud</groupId>
    <artifactId>spring-cloud-starter-alibaba-nacos-discovery</artifactId>
</dependency>
```

服务调用者需要在注册中心拉去服务列表，这个动作称为服务发现

## 使用

discoveryClient.getInstances("item-service")：根据服务名称获取服务列表

instances.get(RandomUtil.randomInt(instances.size()))：随机获取一个服务

serviceInstance.getUri()：获取服务url

```java
@Service
@RequiredArgsConstructor
public class CartServiceImpl extends ServiceImpl<CartMapper, Cart> implements ICartService {
    private final DiscoveryClient discoveryClient;

    private void handleCartItems(List<CartVO> vos) {
        // 根据服务名称获取服务实例
        List<ServiceInstance> instances = discoveryClient.getInstances("item-service");
        if (CollUtils.isEmpty(instances)){
            return;
        }
        // 手写负载均衡
        ServiceInstance serviceInstance = instances.get(RandomUtil.randomInt(instances.size()));
        // 获取商品id
        Set<Long> itemIds = vos.stream().map(CartVO::getItemId).collect(Collectors.toSet());
        // 查询列表
        ResponseEntity<List<ItemDTO>> response = restTemplate.exchange(
                serviceInstance.getUri()+"/items?ids={ids}", // 调用接口
                HttpMethod.GET,
                null,
                new ParameterizedTypeReference<List<ItemDTO>>() {
                },
                Map.of("ids", CollUtils.join(itemIds, ","))
        );
        if (!response.getStatusCode().is2xxSuccessful()){
            return;
        }
        List<ItemDTO> items = response.getBody();
        if (CollUtils.isEmpty(items)) {
            return;
        }
        // 3.转为 id 到 item的map
        Map<Long, ItemDTO> itemMap = items.stream().collect(Collectors.toMap(ItemDTO::getId, Function.identity()));
        // 4.写入vo
        for (CartVO v : vos) {
            ItemDTO item = itemMap.get(v.getItemId());
            if (item == null) {
                continue;
            }
            v.setNewPrice(item.getPrice());
            v.setStatus(item.getStatus());
            v.setStock(item.getStock());
        }
    }

 
}
```
