# TL2TS-Data
TL2TS数据，详见：[TL2TS](https://github.com/BIGXT/TL2TS)

## 基于:

*实验应用：[TrainTicket](https://github.com/FudanSELab/train-ticket)

*混沌实验: [Chaosblade](https://github.com/chaosblade-io/chaosblade#chaosblade-an-easy-to-use-and-powerful-chaos-engineering-toolkit)

## 实验用例

| 注入故障对象 | 故障编号 | 故障根本原因 | 详细描述 |
| ------ | ------ | ------ | ------ |
| TrainTicket应用 | F1 | JVM产生OOM错误。 | 使应用的堆内存占用超出了Xmx的限制，引发溢出。 |
|  | F2 | 微服务间网络存在异常，使得通讯存在延迟，产生意外错误。 | 使ts-cancel-service的通讯产生200ms延迟，部分发送的取消请求超时。 |
|  | F3 | 微服务间网络存在异常，使得通讯丢失，产生意外错误。 | 使ts-travel2-service的通讯产生70%丢包，部分发送通知的请求被丢失。 |
|  | F4 | 服务被意外删除。 | 删除pod：ts-admin-user-service，该服务用于提供用户管理操作。 |
|  | F5 | 容器内Java进程CPU满载。 | ts-admin-route-service服务容器内java进程CPU满载。 |
|  | F6 | 由于方法存在延迟，导致部分请求的处理时间意外增长。 | ts-order-service服务的java进程中creatNewOrder方法注入3s故障，该方法控制新订单的产生。 |
| 物理资源 | F7 | 额外的应用占用80%CPU使用时间。	| 消耗80%CPU时间片 |
|  | F8 | 额外的应用占用95%CPU使用时间。	| 消耗95%CPU时间片 |
| 底层容器 | F9 | 引发微服务容器的错误挂起，导致业务处理出现意外错误。	| 挂起ts-notification-service的容器。 |
|  |F10 | 容器内CPU负载100%。 | 增加ts-config-service的pod负载 |

## 文件说明

### trace logs

#### all trace logs

实验中所收集的所有trace logs。

#### faulty trace logs

包含我们注入故障实验所产生的trace logs，已进行分类和分割。

### fault injection

包含我们用于产生故障注入实验的用例，其中.yaml格式的使用方法为：`kubectl apply -f F*.yaml`