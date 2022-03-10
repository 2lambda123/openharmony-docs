# 设备使用信息统计概述

设备使用信息统计，包括app usage/notification usage/system usage等使用统计，目前只支持app usage使用统计。应用使用信息统计，用于保存和查询应用使用详情（app usage）、事件日志数据（event log）、应用分组（bundle group）情况。部件缓存的应用记录（使用历史统计和使用事件记录）会在事件上报后30分钟内刷新到数据库持久化保存。

## 设备使用信息统计功能说明

设备使用信息统计接口众多，目前只支持app usage使用统计，接下来介绍下应用使用详情（app usage）的接口逻辑。

- **应用使用统计信息落盘时机**：
>1.  每隔30分钟触发一次刷新；
>2.  系统时间变更触发一次刷新；
>3.  下一天开始触发一次刷新；

- **应用查询接口**：
>1.  根据起止时间查询所有应用的事件集合；
>2.  根据起止时间查询应用的使用时长；
>3.  根据起止时间查询当前应用的事件集合；
>4.  根据interval（日、周、月、年）类型和起止时间查询应用的使用时长；
>5.  查询调用者应用的优先级群组；
>6.  判断指定应用当前是否是空闲状态；

### 设备使用信息统计使用权限
- 设备使用信息统计的queryBundleActiveStates、queryBundleStateInfos、queryBundleStateInfoByInterval接口为系统api，调用前需要申请ohos.permission.BUNDLE_ACTIVE_INFO权限。
- 设备使用信息统计的queryCurrentBundleActiveStates、queryAppUsagePriorityGroup、isIdleState接口为三方api，调用时不需要申请权限。