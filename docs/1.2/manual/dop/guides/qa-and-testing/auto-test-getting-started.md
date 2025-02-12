# 自动化测试

## 指引

进入 **DevOps 平台 > 我的项目 > 项目详情 > 测试管理 > 测试用例 > 自动化测试**，创建一个或选择一个已有的测试空间，进入空间</br>
![](https://terminus-paas.oss-cn-hangzhou.aliyuncs.com/paas-doc/2021/08/23/fd6917b9-34a0-4f43-b41f-adb403336bf7.png)

功能指引：</br>
![](https://terminus-paas.oss-cn-hangzhou.aliyuncs.com/paas-doc/2021/08/23/7ad87a45-c413-4188-8d42-e43cdfe5616e.png)

Erda 提供了【[测试空间](#测试空间)】>【[场景集合](#场景集合)】>【[场景](#场景)】三级管理能力。</br>
![](https://terminus-paas.oss-cn-hangzhou.aliyuncs.com/paas-doc/2021/03/04/109f4836-4f70-4099-b47f-a68e1c3e8d72.png)

自动化测试使用流程图</br>
![](https://terminus-paas.oss-cn-hangzhou.aliyuncs.com/paas-doc/2021/07/06/25caf8f8-5145-45d3-9b2e-fd141412dde0.png)

## 测试空间

一个项目下可以创建多个测试空间，测试空间之间无任何关联，不互相影响，是完全隔离的空间。 很多项目只需要一个默认测试空间即可，使用多个测试空间有以下几种情况：
1. 一个项目下有多个子项目，子项目间没有产品上的联动，它们的自动化用例可以完全独立在自己空间
2. 一个项目要同时支持多个版本，那可以一个版本一个空间，当进入新版本迭代时，可以通过复制老版本的空间以创建新版本的空间，并在新版本空间上进行功能变动后的调整

注意：
1. 只有项目所有者和项目经理才有权限创建测试空间
2. 空间复制需要较长时间，复制过程中时，原空间无法操作

## 场景集合

**场景集合** 是一个完整闭环的自动化测试流程，这个完整的流程由多个场景组成，场景之间有简单的依赖（包括执行依赖和数据依赖） 场景集合或者说自动化测试流程有以下几个例子：

1. 登录流程
2. 购物流程
3. 退货流程

而一般来说流程中可能有正向的场景（比如登录成功、下单成功等）也有逆向或者预期失败的场景（比如密码错误次数过多登录失败、退货成功后不能退货），这些场景可以自由的在流程中添加和编排，你可以详细阅读 [场景](#场景) 以了解。

## 场景

**场景** 是自动化测试管理的最小单元，可以对应到功能测试的一条用例。如字面意思，是自动化测试的一个场景，以下将按几种场景集合分别举例：

1. 登录流程：
    - 正常登录场景
    - 异常登录场景
    - 密码错误次数过多场景
    - 登录成功后校验登录态场景
    - 等
2. 购物流程：
    - 商品查看场景（能够正确查询/或者下架商品无法查询）
    - 下单场景（无货时购买失败、优惠计算正确、库存扣减成功等逻辑）
    - 等
3. 退货流程：
    - 订单关闭退货失败的场景
    - 退货成功场景（成功后，后续状态流转正确、通知正确等逻辑）
    - 等

场景的设计理念是短小、尽量内聚，在同一个场景集合下场景们有一定的关联，一定的执行依赖，一定的数据依赖。

### 创建场景

进入测试管理-测试用例目录，选择自动化测试，进入对应的测试空间，选择一个场景集，选择"添加场景"</br>
![](https://terminus-paas.oss-cn-hangzhou.aliyuncs.com/paas-doc/2021/08/23/0c10f87d-4f96-4f22-8364-73c86820bb3d.png)</br>

#### 添加场景入参

添加场景完成后，在场景集中选中添加的场景，点击右侧场景入参区域的“添加“按钮即可完成场景入参添加</br>
![](https://terminus-paas.oss-cn-hangzhou.aliyuncs.com/paas-doc/2021/08/23/f4cf38ff-b60d-4027-b9fa-43d715da705b.png)</br>

#### 添加场景步骤

添加场景完成后，在场景集中选中添加的场景，点击右侧场景步骤区域的“接口“、”配置单“、等待其中任一按钮即可完成场景步骤添加</br>
![](https://terminus-paas.oss-cn-hangzhou.aliyuncs.com/paas-doc/2021/08/23/a88c70e0-d039-4cc5-a21b-fe2edc2d5bfe.png)</br>

##### 步骤类型

场景步骤类型分为：接口、配置单、等待

1、接口
点击”接口“按钮后，即可填写接口步骤信息。其中市场原型可以选择API管理中定义的接口，也可以不选择市场原型，直接输入URL</br>
![](https://terminus-paas.oss-cn-hangzhou.aliyuncs.com/paas-doc/2021/08/23/da35ba85-986f-4782-a116-2e0b0befdbff.png)</br>

2、配置单
点击”配置单“按钮后，即可选择对应的配置单，具体的配置单配置详见[配置单](#配置单)</br>
![](https://terminus-paas.oss-cn-hangzhou.aliyuncs.com/paas-doc/2021/08/23/2f5b33b9-0caf-4a56-aecd-52096fad57a4.png)</br>

3、等待
点击”等待“按钮后，即可添加等待的步骤，时间可输入</br>

##### 步骤编排

场景步骤的执行顺序支持编排，执行方式支持串行执行以及并行执行。执行顺序的编排可以通过步骤前面的拖拽按钮进行拖拽操作，执行方式可以通过点击”添加并行接口“按钮进行编辑，支持重新修改为串行执行，详见下图：</br>
![](https://terminus-paas.oss-cn-hangzhou.aliyuncs.com/paas-doc/2021/08/23/e6b8341c-2624-4a1d-af5d-2f4ae785be64.png)</br>

##### 请求参数

接口步骤的请求参数主要包含：Params、Headers以及Body。其中参数的值可选：固定值、本场景入参、 前置接口入参、全局变量入参以及mock参数。参数的值支持选择和过滤，选择后自动生成参数表达式
本场景入参表达式：
```
${{ params.xxxx }}
```
前置接口入参表达式：
```
${{ outputs.12345.xxxx }}
```
全局变量入参表达式：
```
${{ configs.autotest.xxxx }}
```
mock参数表达式：
```
${{ random.integer }}
```
其他类型的mock参数写法参考：[mock参数](#mock参数)</br>
![](https://terminus-paas.oss-cn-hangzhou.aliyuncs.com/paas-doc/2021/08/23/caa54121-f52e-4407-a991-350d70c20870.png)</br>

##### 循环策略

![](https://terminus-paas.oss-cn-hangzhou.aliyuncs.com/paas-doc/2021/08/23/7ac523f9-b61b-4656-bd4d-af7082d96b19.png)</br>

循环策略的配置意思是当条件没成立就会一直循环执行，当循环次数达到了`最大循环次数`就会退出

- 循环结束条件，可以配置例如 `task_status == 'Success'` 当前任务的状态是否是成功状态,`task_status == 'Failed'` 当前任务的状态是否是失败状态, <code v-text="'${{ outputs.40025.status }} == 401'"/> 前置步骤 `40025` 的出参 `status` 是否等于 `401`
- 最大循环次数(N)，代表循环条件没有成立的时候最大的循环次数
- 衰退比例(decline_ratio)，衰退最大值(decline_limit_sec)，起始间隔(interval_sec) 3 个参数遵循一个计算公式 `loop_interval = min(interval_sec * (decline_ratio)^N, decline_limit_sec)`, 通过公式计算得到的就是每次循环的间隔时间


##### 出参

步骤支持添加出参。出参的作用：作为断言参数、添加到场景出参、传递给下一个步骤。出参的表达式写法请参考：[出参表达式](#出参表达式)</br>
![](https://terminus-paas.oss-cn-hangzhou.aliyuncs.com/paas-doc/2021/08/23/6a689a4a-5382-4610-b83b-98bfd4e4df8d.png)</br>

##### 断言

步骤支持添加断言，可以通过选择对应的接口步骤、选中”Tests“TAB页后添加出参以及断言来完成断言的添加，具体断言的添加方式见[断言说明](#断言说明)</br>
![](https://terminus-paas.oss-cn-hangzhou.aliyuncs.com/paas-doc/2021/08/23/3f394144-31ba-48c4-9416-fd97fedb87fd.png)</br>

#### 添加场景出参

场景支持将步骤的出参添加到场景的出参中传递出去，供后面的场景作为入参使用，添加步骤如下图</br>
![](https://terminus-paas.oss-cn-hangzhou.aliyuncs.com/paas-doc/2021/08/23/91c6ef80-27c8-41aa-93b7-87f160674a8d.png)</br>

#### 执行明细

自动化测试支持查看单个场景的执行明细， 包含：执行详情、执行历史、步骤接口以及步骤日志</br>
![](https://terminus-paas.oss-cn-hangzhou.aliyuncs.com/paas-doc/2021/08/23/dded10f3-5019-42dd-8d2e-37e7809fa969.png)</br>

### 引用场景

场景集支持引用其他场景集，可以实现跨场景集的参数续传。执行该场景集时，被引用的场景集也会被全部执行。可以进入测试管理-测试用例目录，选择一个场景集后，点击”引用场景集“按钮完成操作</br>
![](https://terminus-paas.oss-cn-hangzhou.aliyuncs.com/paas-doc/2021/08/23/fb0cbfc4-87b6-43ab-8d4b-1a783d907a9f.png)</br>

## 数据银行

**进入 DevOps 平台 > 我的项目 > 项目详情 > 测试管理 > 数据银行**。

### 数据源

目前平台支持添加 MySQL、Redis 以及 Custom 服务三种数据源。</br>
![](https://terminus-paas.oss-cn-hangzhou.aliyuncs.com/paas-doc/2021/08/23/d1fa5c56-72a3-4c5d-8e7b-859bdcc93e04.png)</br>

### 配置单

配置单配置的是执行脚本，例如MySQL脚本、Redis脚本、shell脚本</br>
配置单支持配置入参</br>

##### 配置单管理

进入数据银行页面后，选择”配置单“TAB页，该页面可以进行配置单目录的增删改查、配置单的增删改查操作</br>
![](https://terminus-paas.oss-cn-hangzhou.aliyuncs.com/paas-doc/2021/08/23/de5830f6-d138-495b-9795-d1604586872d.png)</br>

##### 配置信息

选择具体的配置单后，可以对配置单的流水线进行修改，可以修改的信息包含：入参配置、节点信息</br>
![](https://terminus-paas.oss-cn-hangzhou.aliyuncs.com/paas-doc/2021/08/23/8628da1a-61cd-4b2f-8a78-047a1670df26.png)</br>
示例MYSQL配置单：</br>
点击配置信息-流水线的”编辑“按钮后，选中MYSQL配置单节点，可以对该配置单的任务名称、版本、执行条件、任务参数(datasource/database/sql)、运行资源(cpu/mem)以及循环策略进行配置</br>
![](https://terminus-paas.oss-cn-hangzhou.aliyuncs.com/paas-doc/2021/08/23/fadc9dcf-ea76-4818-8023-21f383a20407.png)</br>

##### 执行明细

配置单支持查看每个配置单的执行明细，明细包含：构建详情、执行记录。点击配置单节点右上方的”...“按钮可以查看配置单的执行日志</br>
![](https://terminus-paas.oss-cn-hangzhou.aliyuncs.com/paas-doc/2021/08/23/c74ffc12-2d78-4b1f-828b-8ec6dba4318b.png)</br>

## 执行计划

进入 **DevOps 平台 > 我的项目 > 项目详情 > 测试管理 > 执行计划**。
### 新建执行计划

进入执行计划目录后，选择”自动化测试“TAB页，点击右上方的”新建计划“按钮即可完成执行计划的新建</br>
![](https://terminus-paas.oss-cn-hangzhou.aliyuncs.com/paas-doc/2021/08/23/18930565-5f4f-4cb6-8e29-28ec4449158d.png)</br>

进入执行计划详情页，执行计划支持场景级的添加、删除以及执行集顺序的编排</br>
![](https://terminus-paas.oss-cn-hangzhou.aliyuncs.com/paas-doc/2021/08/23/facef535-4ec2-44e3-9560-86bc3cd168dd.png)</br>

### 执行

执行计划支持手动触发执行，执行时支持选择不同的环境，具体的环境配置参考[参数配置](#参数配置)</br>

### 执行明细

执行完成后，平台支持执行明细的查看，主要包含：执行详情、执行步骤以及执行历史，其中执行步骤支持点击查看具体的执行结果和日志</br>
![](https://terminus-paas.oss-cn-hangzhou.aliyuncs.com/paas-doc/2021/08/23/63ab2c51-248c-4afb-aa54-9e32144f9801.png)

## 参数配置

进入 **DevOps 平台 > 我的项目 > 项目详情 > 测试管理 > 参数配置**。
### 添加配置

进入参数配置页面后，选择”自动化测试“TAB页，点击右上角的”添加配置“按钮，即可进入参数配置的页面</br>
![](https://terminus-paas.oss-cn-hangzhou.aliyuncs.com/paas-doc/2021/08/23/bcfe8703-83b6-45e7-9fbf-6f6878064635.png)</br>

配置主要分为三类：环境域名、header以及global</br>

##### 环境域名

1. 当接口步骤中定义了域名，则选择该环境执行时，仍使用接口步骤中定义的域名
2. 当接口步骤中未定义域名，则选择该环境执行时，默认使用当前配置的环境域名执行

##### Header

1. 用户后续选择该执行环境时，若接口中没有同名的header信息，会自动传该环境配置中的header信息到请求接口中
2. 用户后续选择该执行环境时，若接口中有同名的header信息，会优先用接口中已定义的header信息传到请求接口中

##### Global

全局参数配置，引用表达式：
```
${{ configs.autotest.xxxx }}
```
可以在场景入参、接口入参以及配置单配置中使用


## 断言说明

添加断言的前置条件：设置出参以及出参表达式，用例必须设置断言以进行有效测试，用例如果没有断言，任何情况下该用例都将通过。

### 出参表达式

场景步骤的出参支持三种类型的参数解析，分为：Status，Header:K/V，Body:JSON(body) ，解析的表达式遵循Linux jq表达式规范，具体参考：https://stedolan.github.io/jq/manual/</br>
举例如下：</br>
假设response结果如下： { "data":[ { "id":185, "ss":"aa1" }, { "id":186, "ss":"aa2" }, { "id":187, "ss":"aa3" } ] }</br>
1. 获取data下list中所有ID</br>
   表达式：[.data[] | try .id] </br>
   结果为:[185,186,187]
2. 获取data下ss="aa2"的ID</br>
   表达式：.data[] | select(.ss=="aa2").id</br>
   结果为：186
3. 获取data下ss="aa1"的ID，和data下ss="aa2"的ID，拼接成list[]</br>
   表达式：[(.data[] | select(.ss=="aa1").id),(.data[] | select(.ss=="aa2").id)]</br>
   结果为：[185,186]


### 断言类型

断言支持形式如下：
* 大于、大于等于、小于、小于等于: 支持整数，小数。
* 等于、不等于: 支持整数，小数，字符串，对象(数组，Map)。
* 包含、不包含: 支持字符串和正则匹配。
* 为空、不为空: 支持判断数组，Map，字符串是否为空。
* 存在、不存在: 判断出参是否存在。出参为 Response 的 Key。
* 属于、不属于: 支持正负整数、0、字符串。
    + 数值：请按照标准的数学表达式规范填写。示例如下： 区间支持开区间和闭区间、示例闭区间：[-20,20]
      表示集合：{[-200,200],-1,2}
    + 字符串仅支持集合、示例：{“abc”,”bcd”,”200”,”-200”,”已报名”,”报名成功”}

## mock参数

mock参数支持的类型如下：
* string: 所有字符串，如: Abc,
* integer: 整型，如: 100
* float: 浮点型，如: 13.14
* boolean: 布尔型，如: true/false
* upper: 大写字母，如: ABC
* lower: 小写字母，如: abc
* mobile: 11位手机号，如: 18888888888
* digital_letters: 数字和大小写字母，如: Abc123
* letters: 大小写字母，如: Abc
* character: 单个字符，如: a
* timestamp: 当前时间戳格式：1586917254，单位是s
* timestamp_hour: 1小时前时间戳格式：1583317290，单位是s
* timestamp_ns: 当前时间戳ns格式：1586917325230422166，单位是ns
* timestamp_ns_hour: 1小时前时间戳格式：1586913750801408626，单位是ns
* date：当前日期、格式：2020-01-01
* date_day：1天前日期、格式：2020-01-01
* datetime：当前时间、格式：2020-01-01 15:04:05
* datetime_hour：1小时前时间、格式：2020-01-01 14:04:05

## Cookie保持

当前场景下，若有登录接口，登录接口访问成功后，接口返回的Header中如果有Set-Cookie参数，平台会将该参数值自动传到当前场景之后的接口的请求Header-Cookie中</br>
注意：
1. 仅限同一场景中Cookie续传，不支持跨场景的Cookie续传
2. 登录接口返回的Header中要有Set-Cookie参数才会续传
3. 如果同一场景有2个登录接口，向上取最近的登录接口返回的Set-Cookie参数为准
