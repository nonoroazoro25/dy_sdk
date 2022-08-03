# API接口使用方法

## 准备工作

所有的接口调用都是通过dayan_api模块，在使用前必须先实例化一个api对象：

```python
user_info = {
    "domain_name": "task.dayancloud.com",
    "platform": "54",
    "access_id": "xxxxxxxxxxxxxxxxxxxxxx",
    "access_key": "xxxxxxxxxxxxxxxxxxxxx",
}

api = RayvisionAPI(access_id=user_info['access_id'],
                   access_key=user_info['access_key'],
                   domain=user_info['domain_name'],
                   platform=user_info['platform'])
```


**说明**：

1. 以下接口调用会直接使用以上实例的api进行调用；
2. 返回示例中显示的是原始接口结果，实际在dayan_api中接口返回给用户的只是“data”参数值；


## 获取用户详情

**旧接口路径**：  /api/render/setUp/queryUserProfile

**请求参数**：缺省

**请求示例**：

```python
user_profile = api.user.query_user_profile()
```

**返回示例**：

```json
{
    "version": "1.0.0",
    "result": true,
    "message": "success",
    "code": 200,
    "data": {
        "userId": 10001136,
        "userName": "rayvision",
        "platform": 2,
        "phone": "173333333333",
        "email": "",
        "company": "",
        "name": "",
        "job": "",
        "communicationNumber": "",
        "softType": 2000,
        "softStatus": 1,
        "businessType": 1,
        "status": 1,
        "infoStatus": 0,
        "accountType": 1,
        "userType": 1,
        "mainUserId": 0,
        "level": 49,
        "pictureLever": null,
        "zone": 1,
        "rmbbalance": 0,
        "usdbalance": 0,
        "rmbCumulative": 0,
        "usdCumulative": 0,
        "credit": 0,
        "coupon": 49.93,
        "description": "",
        "country": "中国",
        "city": "广东 中山",
        "address": "",
        "cpuPrice": 0.67,
        "gpuPrice": 20,
        "shareMainCapital": 0,
        "subDeleteTask": 0,
        "useMainBalance": 0,
        "hideBalance": 0,
        "hideJobCharge": 0,
        "useLevelDirectory": 1,
        "downloadDisable": 0,
        "displaySubaccount": 1,
        "subaccountLimits": 5,
        "houdiniFlag": 0,
        "c4dFlag": 0,
        "blenderFlag": 0,
        "keyshotFlag": 0,
        "studentEndTime": null
    },
    "serverTime": 1535953580730
}

```

## 获取用户设置

**接口路径**： /api/rendering/user/client/queryUserSetting

**请求参数**：缺省

**返回参数**：

| **参数**                  | **类型** | **说明**                                | **备注**       |
|---------------------------|----------|-----------------------------------------|----------------|
| infoStatus                | Integer  |                                         |                |
| accountType               | Integer  |                                         |                |
| shareMainCapital          | Integer  | 共用主账号资产 0 不共用 1共用           |                |
| subDeleteTask             | Integer  | 是否允许子账号删除任务 0不允许 1 允许   |                |
| useMainBalance            | Integer  | 是否允许子账号使用主账号余额或信用额度  | 0不允许 1 允许 |
| singleNodeRenderFrames    | String   | 一机渲多帧                              |                |
| maxIgnoreMapFlag          | String   | 是否忽略max错误贴图                     | 0不忽略，1忽略 |
| autoCommit                | String   | 是否启动场景参数渲染                    | 1不启用，2启用 |
| separateAccountFlag       | Integer  | 主子账号分离设置                        |                |
| mifileSwitchFlag          | Integer  | mi文件分析风险开关                      |                |
| assfileSwitchFlag         | Integer  | 不分析ass文件开关标识                   |                |
| manuallyStartAnalysisFlag | Integer  | 手动开启分析开关                        |                |
| downloadDisable           | Integer  | 禁用下载                                | 1禁用，0不禁用 |
| taskOverTime              | Integer  | 超时时间-小时                           |                |
| taskOverTimeSec           | Integer  | 超时时间-秒                             |                |
| ignoreMapFlag             | Integer  | 本地分析忽略贴图丢失                    |                |
| isVrayLicense             | Integer  | 使用付费版vray渲染                      |                |
| justUploadConfigFlag      | Integer  | 本地分析max只上传配置文件               |                |
| justUploadCgFlag          | Integer  | maya渲染只上传cg文件                    |                |
| mandatoryAnalyseAllAgent  | Integer  | 本地分析强制分析所有代理                |                |

**请求示例**：

```python
user_setting = api.user.query_user_setting()
```

**返回示例**：

```json
{
    "version": "1.0.0",
    "result": true,
    "message": "success",
    "code": 200,
    "data": {
        "infoStatus": null,
        "accountType": null,
        "shareMainCapital": 0,
        "subDeleteTask": 0,
        "useMainBalance": 0,
        "singleNodeRenderFrames": "1",
        "maxIgnoreMapFlag": "1",
        "autoCommit": "2",
        "separateAccountFlag": 0,
        "mifileSwitchFlag": 0,
        "assfileSwitchFlag": 0,
        "manuallyStartAnalysisFlag": 0,
        "downloadDisable": 0,
		"taskOverTime": 12,
		"taskOverTimeSec": 3600
    },
    "serverTime": 1535954828406
}
```


## 获取用户传输BID

**接口路径**： /api/rendering/task/plugin/getPluginTransferBid

**请求参数**：缺省

**返回参数**：

| **参数**             | **类型** | **说明**                                                     | **备注** |
| -------------------- | -------- | ------------------------------------------------------------ | -------- |
| config_bid           | String   | 配置文件传输ID                                               |          |
| output_bid           | String   | 下载传输ID                                                   |          |
| parent_input_bid     | String   | 对应主账号Input传输bid                                       |          |
| input_bid            | String   | 资产上传传输ID                                               |          |
| sub_user_output_bids | Object   | 子账号outputbids,如果访问用户是主账号，则有子账号值，否则为空 |          |
| userId               | String   | 子账号ID                                                     |          |
| output_bid           | String   | 子账号outputbid                                              |          |

**请求示例**：

```python
user_transfer_bid = api.user.get_transfer_bid()
```

**返回示例**：

```json
{
    "version": "1.0.0",
    "result": true,
    "message": "success",
    "code": 200,
    "data": {
        "config_bid": "30201",
        "input_bid": "10201",
        "output_bid": "20201",
        "parent_input_bid": "10202",
        "sub_user_output_bids": [{
            userId:"119776",
            outputBid:"10401"
        }]
	},
    "serverTime": 1535957964631
}
```

## 创建任务号

**接口路径**： /api/render/task/createTask

**请求参数**：

| **参数**          | **类型**       | 是否必须 | **说明**               | **备注**                 |
| ----------------- | -------------- | -------- | ---------------------- | ------------------------ |
| count             | Integer        | N        | 非必须，创建任务号数量 | 默认为 1                 |
| out_user_id       | Long           | N        | 非必须，外部用户ID     | 用于区分第三方接入的用户 |
| task_user_level   | Integer        | N        | 非必须，任务用户级别   | 可选50和60,默认为50      |
| labels            | List\<String\> | N        | 非必须，标签列表       |                          |
| clone_original_id | integer        | N        | 克隆原任务id           |                          |
| artist            | String         | N        | 制作人                 |                          |

**返回参数**：

| **参数**        | **类型**        | **说明**   | **备注** |
| --------------- | --------------- | ---------- | -------- |
| aliasTaskIdList | List\<String\>  | 任务ID别名 |          |
| taskIdList      | List\<Integer\> | 任务ID     |          |
| userId          | Long            | 用户id     |          |

**请求示例**：

```Python
create_task_id = api.task.create_task(count=1,
                                      task_user_level=50,
                                      labels=["label_test1", "label_test2"])
```

**返回示例**：

```python
{
    "version": "1.0.0",
    "result": true,
    "message": "success",
    "code": 200,
    "data": {
        "aliasTaskIdList": [
            "2W19097"
        ],
        "taskIdList": [
            19097
        ],
        "userId": 10007893
    },
    "serverTime": 1535959487092
}
```

## 提交任务

**接口路径**： /api/rendering/task/plugin/pluginSubmitTask

**请求参数**：

| **参数** | **类型** | 是否必须 | **说明**   | **备注** |
| -------- | -------- | -------- | ---------- | -------- |
| task_id  | Integer  | Y        | 提交任务ID |          |
| producer | String   | N        | 制作人     |          |

**返回参数**：缺省

**请求示例**：

```python
submit_task = api.task.submit_task(task_id=create_task_id[0])
```

**返回示例**：

```Python
{
    "version": "1.0.0",
    "result": true,
    "message": "success",
    "code": 200,
    "data": null,
    "serverTime": 1535957894211
}
```

 注意：进行提交之前需要先调用传输接口上传相关的分析配置文件


## 停止任务

**接口路径**： /api/rendering/task/renderingTask/stopTask

**请求参数**：

| **参数**        | **类型**        | 是否必须 | **说明**   | **备注** |
| --------------- | --------------- | -------- | ---------- | -------- |
| task_param_list | List\<Integer\> | Y        | 任务号集合 |          |

**返回参数**：缺省

**请求示例**：

```Python
stop_task = api.task.stop_task(task_param_list=[13798105])
```

**返回示例**：

```json
{
    "version": "1.0.0",
    "result": true,
    "message": "success",
    "code": 200,
    "data": null,
    "serverTime": 1535957894211
}
```

## 重提帧

**接口路径**：  /api/rendering/task/renderingTask/recommitFailFrame

**请求参数**：

| **参数**        | **类型**        | 是否必须 | **说明**                                 | **备注** |
| --------------- | --------------- | -------- | ---------------------------------------- | -------- |
| task_param_list | List\<Integer\> | Y        | 任务号集合                               |          |
| status          | List\<Integer>  | Y        | 重提的帧任务状态集合状态码--1 等待;2 开始;3 中止;4 完成;5 失败;11 超时|          |

**返回参数**：缺省

**请求示例**：

```python
restart_failed_frames = api.query.restart_failed_frames(task_param_list=[13788981], status=[1, 2, 3, 4, 5, 11])
```

**返回示例**：

```json
{
    "version": "1.0.0",
    "result": true,
    "message": "success",
    "code": 200,
    "data": null,
    "serverTime": 1535957894211
}
```


## 获取任务详情

**接口路径**： /api/rendering/task/renderingTask/queryTaskInfo

**请求参数**：

| **参数**      | **类型**        | **说明**   | **备注** |
| ------------- | --------------- | ---------- | -------- |
| task_ids_list | List\<Integer\> | 任务ID集合 |          |

**返回参数**：List\<TaskInfo>

| **参数**              | **类型**             | **说明**                   | **备注**                                                                                                      |
|-----------------------|----------------------|----------------------------|---------------------------------------------------------------------------------------------------------------|
| sceneName             | String               | 场景名                     |                                                                                                               |
| id                    | Integer              | 任务id                     |                                                                                                               |
| taskAlias             | String               | 任务别名                   |                                                                                                               |
| taskStatus            | Byte                 | 任务状态                   | 0/等待，5/渲染，10/停止，15/用户停止，20/因欠费停止，25/完成，30/完成包含失败帧，35/放弃，40/测试完成，45/失败，50/分析中，100/状态更新中 ||
| statusText            | String               | 任务状态文本               |                                                                                                               |
| preTaskStatus         | Byte                 | 预处理任务状态             |                                                                                                               |
| preStatusText         | String               | 预处理状态文本             |                                                                                                               |
| totalFrames           | Integer              | 总帧数                     |                                                                                                               |
| abortFrames           | Integer              | 放弃帧数                   |                                                                                                               |
| executingFrames       | Integer              | 正在运行的帧数             |                                                                                                               |
| doneFrames            | Integer              | 完成的帧数                 |                                                                                                               |
| failedFrames          | Integer              | 失败帧数                   |                                                                                                               |
| framesRange           | String               | 帧范围                     |                                                                                                               |
| projectName           | String               | 项目名                     |                                                                                                               |
| renderConsume         | BigDecimal           | 任务渲染消费的总费用       |                                                                                                               |
| taskArrears           | BigDecimal           | 任务欠费金额               |                                                                                                               |
| submitDate            | Date                 | 提交时间                   |                                                                                                               |
| startTime             | Date                 | 开始时间                   |                                                                                                               |
| completedDate         | Date                 | 完成时间                   |                                                                                                               |
| renderDuration        | Long                 | 任务渲染总时长             | 单位：秒                                                                                                      |
| userName              | String               | 用户名                     |                                                                                                               |
| producer              | String               | 制作人                     |                                                                                                               |
| taskLevel             | Byte                 | 任务优先级                 |                                                                                                               |
| taskUserLevel         | Integer              | 用户层面的优先级           |                                                                                                               |
| taskLimit             | Integer              | 任务机器限制               |                                                                                                               |
| taskOverTime          | Long                 | 任务超时提醒               |                                                                                                               |
| outputFileName        | String               | 输出文件名                 |                                                                                                               |
| munuTaskId            | String               | 调度器id                   |                                                                                                               |
| layerParentId         | String               | 针对maya任务，层父id       |                                                                                                               |
| cgId                  | Integer              | 任务类型                   | 2001/maya，2000/max                                                                                           |
| taskKeyValueVo        | Object               | 任务关键字集合             |                                                                                                               |
| userAccountConsume    | Bigdecimal           | 用户账户扣费               |                                                                                                               |
| couponConsume         | Bigdecimal           | 优惠券扣费                 |                                                                                                               |
| isOpen                | Byte                 | 前端的展开按钮是否展开     |                                                                                                               |
| taskType              | String               | 任务类型                   | /预处理,/光子渲染,/渲染主图                                                                                   |
| renderCamera          | String               | 渲染相机                   |                                                                                                               |
| cloneParentId         | Integer              | 克隆任务挂在那个任务下的id |                                                                                                               |
| cloneOriginalId       | Integer              | 从哪个任务克隆的           |                                                                                                               |
| shareMainCapital      | Byte                 | 该任务是否共享主账号资产   | (0 不共享 1共享)                                                                                              |
| taskRam               | Integer              | 任务渲染内存               |                                                                                                               |
| respRenderingTaskList | **List\<TaskInfo\>** | 展开的任务的子任务         | 跟此对象一样                                                                                                  |
| layerName             | String               | 层名                       |                                                                                                               |
| taskTypeText          | String               | 任务类型                   | 光子/主图                                                                                                     |
| isDelete              | Byte                 | 是否删除                   | 0：已删除，1：未删除                                                                                          |

**请求示例**

```
task_info = api.query.task_info(task_ids_list=[14400249])
```

**返回示例**

```json
{
    "version": "1.0.0",
    "result": true,
    "message": "success",
    "code": 200,
    "data": {
        "pageCount": 1,
        "pageNum": 1,
        "total": 1,
        "size": 100,
        "items": [
            {
                "sceneName": "test_no_randerman_175.hip",
                "id": 14400249,
                "taskAlias": "2W14400249",
                "taskStatus": 25,
                "statusText": "render_task_status_25",
                "preTaskStatus": null,
                "preStatusText": null,
                "totalFrames": 1,
                "abortFrames": 0,
                "executingFrames": 0,
                "doneFrames": 1,
                "failedFrames": 0,
                "framesRange": "/out/geometry110-200[1]",
                "projectName": "analysis_multi_project_empty_placeholder",
                "renderConsume": 0.0,
                "taskArrears": 0.0,
                "submitDate": 1577765849000,
                "startTime": 1577765851000,
                "completedDate": 1577766104000,
                "renderDuration": 13,
                "userName": "ding625yutao",
                "producer": "丁玉涛",
                "taskLevel": 81,
                "taskUserLevel": 0,
                "taskLimit": 1,
                "taskOverTime": 43200,
                "overTimeStop": 86400,
                "userId": 100150764,
                "outputFileName": "14400249_test_no_randerman_175",
                "munuTaskId": "2019123100841",
                "munuTaskIds": "2019123100841",
                "layerParentId": 0,
                "cgId": 2004,
                "userAccountConsume": 0.0,
                "couponConsume": 0.039,
                "qyCouponConsume": null,
                "isOpen": 0,
                "taskType": "GopRender",
                "renderCamera": "",
                "cloneParentId": 0,
                "cloneOriginalId": 0,
                "shareMainCapital": 0,
                "taskRam": 64,
                "respRenderingTaskList": null,
                "layerName": "",
                "taskTypeText": null,
                "locationOutput": "C:/RenderFarm/Download",
                "isDelete": 1,
                "channel": 1,
                "remark": "",
                "labels": "{}",
                "isOverTime": 0,
                "taskKeyValueVo": {
                    "tiles": null,
                    "allCamera": null,
                    "renderableCamera": null
                },
                "waitingCount": null,
                "stopType": 0
            }
        ]
    },
    "serverTime": 1578046630345,
    "requestId": "py6RCN-VGFzay1TZXJ2aWNlMDc-1578046630330"
}
```


##  获取传输配置 

**接口地址**：  /api/render/transfer/getConfig

**请求参数**：缺省

**返回参数**：

| **参数**            | **类型** | **说明**                    | **备注** |
| ------------------- | -------- | --------------------------- | -------- |
| inputBid            | String   | Input传输bid                |          |
| outputBid           | String   | output传输bid               |          |
| configBid           | String   | config bid                  |          |
| parentInputBid      | String   | 对应主账号Input传输bid      |          |
| resqEngines         | Object[] | 引擎配置                    |          |
| engineName          | String   | 引擎名                      |          |
| checkServer         | String   | 校验服务器                  |          |
| checkPort           | String   | 校验端口                    |          |
| checkEnable         | String   | 检查是否可用                |          |
| checkExcludType     | String   | 检测例外 文件类型 ,隔开     |          |
| automaticCheck      | number   | 自动检测并切换线路 1是 0:否 |          |
| isDefault           | number   | 默认 1是 0否                |          |
| resqEngineAccounts  | Object[] | aspera账户                  |          |
| bid                 | String   | aspera对应input bid         |          |
| name                | String   | aspera用户名                |          |
| password            | String   | aspera密码                  |          |
| respTaskEngineLines | Object[] | 引擎列表                    |          |
| name                | String   | 线路名                      |          |
| server              | String   | 线路IP                      |          |
| port                | String   | 端口                        |          |
| isDefault           | Number   | 是否默认 1默认              |          |
| lineId              | Number   | 线路表ID                    |          |
| type                | Number   | 线路类型 1.专线 0.通用线路  |          |
| subUserOutputBids   | Object[] | 子账号outputbid集合         |          |
| userId              | String   | 子账号ID                    |          |
| outputBid           | String   | outputBid                   |          |

**请求示例**：

```python
transfer_config = api.transmit.get_transfer_config()
```

返回参数示例：

```json
{
    "version": "1.0.0",
    "result": true,
    "message": "success",
    "code": 200,
    "data": {
        "inputBid": "10202",
        "outputBid": "20202",
        "configBid": "30201",
        "parentInputBid": null,
        "resqEngines": [
            {
                "resqEngineAccounts": [
                    {
                        "bid": "20202",
                        "name": "20202",
                        "password": "xB9CWAML1qd+k1X9prYHheQUAtZ0hcpmJHxe7mfVw9Q="
                    }
                ],
                "respTaskEngineLines": [
                    {
                        "name": "Aspera_main",
                        "server": "10.60.197.79",
                        "port": "10221",
                        "isDefault": 1,
                        "lineId": 123,
                        "type":1
                    }
                ],
                "engineName": "trtt",
                "automaticCheck": 1,
                "checkServer": "677",
                "checkPort": "8888",
                "checkEnable": "1",
                "checkExcludType": "88",
                "isDefault": 0
            },
            {
                "resqEngineAccounts": null,
                "respTaskEngineLines": [
                    {
                        "name": "raysync_main",
                        "server": "10.60.197.79",
                        "port": "10200",
                        "isDefault": 1,
                        "lineId": 121
                    }
                ],
                "engineName": "RaySync",
                "automaticCheck": 0,
                "checkServer": "10.60.196.151",
                "checkPort": "10100",
                "checkEnable": "0",
                "checkExcludType": "tx",
                "isDefault": 1
            },
            {
                "resqEngineAccounts": [
                    {
                        "bid": "30201",
                        "name": "30201",
                        "password": "ACz/0lNMCgyq/7WjR0QGpaXmR0/Xb0//6UaMn/s8QN4="
                    }
                ],
                "respTaskEngineLines": [
                    {
                        "name": "Aspera_main",
                        "server": "10.60.197.79",
                        "port": "10221",
                        "isDefault": 1,
                        "lineId": 123
                    }
                ],
                "engineName": "Aspera",
                "automaticCheck": 0,
                "checkServer": "test2.raysync.cn",
                "checkPort": "8888",
                "checkEnable": "0",
                "checkExcludType": "tx",
                "isDefault": 0
            }
        ],
        "subUserOutputBids": [
            {
                "userId": "119784",
                "outputBid": "10202"
            }
        ]
    },
    "serverTime": 1587380763325,
    "requestId": "K7wW6L-QmV5b25kTGVlZGVNYWNCb29rLVByby5sb2NhbA-1587380762156"
}
```

##  上传任务配置文件 

**接口路径**：  /api/render/submit/taskJsonFile 

**请求参数**：

| **参数**  | **类型** | 是否必须 | **说明** | **备注**        |
| --------- | -------- | -------- | -------- | --------------- |
| task_id   | Integer  | Y        | 任务号   |                 |
| content   | String   | Y        | 文件内容 |                 |
| file_name | String   | N        | 文件名   | 默认“task.json” |

**返回参数**：缺省

**请求示例**：

```Python
start_task = api.task.start_task(task_param_list=[13798105])
```

**返回示例**：

```json
{
    "version": "2.0.0",
    "result": true,
    "message": "success",
    "code": 200,
    "data": null,
    "serverTime": 1589532607599,
    "requestId": null
}
```

##  获取用户存储文件结构 

[^2021/1/18]: Add New Interface

**接口路径**：  /api/render/file/operate/getOutputUserDirFile 

**请求参数**：

| **参数**  | **类型** | 是否必须 | **说明**                                               | **备注**  |
| --------- | -------- | -------- | ------------------------------------------------------ | --------- |
| task_id   | Integer  | N        | 任务号,如果是分层任务则是指的子任务号,即每一层的任务号 |           |
| tree_path | String   | N        | 相对用户存储(output)根的路径                           | 默认为“/” |

**返回参数[data]**：

| 参数       | 类型   | 说明                                            |
| ---------- | ------ | ----------------------------------------------- |
| fileName   | string | 当前文件名或文件夹名                            |
| fileSize   | int    | 文件大小，如果是文件夹则为“null”                |
| iconPath   | string | 图表路径(可忽略此参数)                          |
| lastModify | string | 文件或文件夹更新日期                            |
| fileType   | string | 文件后缀，如果是文件夹则为"null"                |
| filePath   | string | 文件或文件夹相对用户存储output根的相对路径      |
| directory  | bool   | 是否为文件夹, "true":是文件夹，“false”:非文件夹 |
| isArrears  | int    | 是否欠费, 0：未欠费，1：欠费                    |

**请求示例**：

```Python
paths = api.transmit.get_output_files(task_id=1484861)
```

**返回示例**：

```json
[
    {
        "fileName": "1484861_muti_layer_test",
        "fileSize": null,
        "iconPath": null,
        "lastModify": "2021-01-15 12:11:59",
        "fileType": null,
        "filePath": "/1484861_muti_layer_test",
        "directory": true,
        "isArrears": 0
    }
]
```

##  获取任务的所有子任务号 

[^2021/1/18]: Add New Interface

**接口路径**：

**请求参数**：

| **参数** | **类型**          | 是否必须 | **说明**                                                   |
| -------- | ----------------- | -------- | ---------------------------------------------------------- |
| task_id  | Integer or string | Y        | 获取主帐户下的所有子帐户，如果没有子帐户，则返回当前账号ID |



**请求示例**：

```json
ids = api.query.get_small_task_id(task_id=1521323)
```

**返回示例**：

```
[1521325, 1521327, 1521329]
```


