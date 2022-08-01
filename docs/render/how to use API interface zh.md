# API接口使用方法

## 准备工作

所有的接口调用都是通过rayvision_api模块，在使用前必须先实例化一个api对象：

```python
user_info = {
    "domain_name": "task.renderbus.com",
    "platform": "2",
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
2. 返回示例中显示的是原始接口结果，实际在rayvision_api中接口返回给用户的只是“data”参数值；


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

## 获取分析错误码

**接口路径:**  /api/render/submit/queryAnalyseErrorDetail 

**请求参数**：

| **参数** | **类型** | 是否必须 | **说明**       | **备注**                    |
| -------- | -------- | -------- | -------------- | --------------------------- |
| code     | String   | N        | 必须值，错误码 | codes和code任一必填         |
| codes    | String   | N        | 错误码列表     | codes和code任一必填         |
| language | String   | N        | 非必须，语言   | “0”：中文（默认） "1"：英文 |

**返回参数**：List\<CodeInfo\>

| **参数**         | **类型** | **说明**         | **备注**                     |
|------------------|----------|------------------|------------------------------|
| id               |          |                  |                              |
| code             | Integer  | 错误码           |                              |
| type             | Integer  | 类型             | 0警告-可忽略，1错误-不可忽略 |
| languageFlag     | Integer  | 语言类型         | 0中文，1英文                 |
| desDescriptionCn | String   | 中文描述         |                              |
| desSolutionCn    | String   | 解决方案         |                              |
| solutionPath     | String   | 解决方案连接     |                              |
| isRepair         | Integer  | 是否可修复       | 1 可修复，0不可修复          |
| isOpen           | Integer  | 错误是否开启拦截 | 0 不开启，1 开启             |
| updateTime       | Date     | 最后更新时间     |                              |

**请求示例**：

```Python
error_detail = api.query.error_detail(code="50001")
```

**返回示例**：

```json
{
    "version": "1.0.0",
    "result": true,
    "message": "success",
    "code": 200,
    "data": [
        {
            "id": 5,
            "code": "15000",
            "type": 1,
            "languageFlag": 0,
            "desDescriptionCn": "启动3ds max卡住或者失败",
            "desSolutionCn": "1.检查启用对应版本的3ds max是否有特殊弹窗，有的话手动关闭；\n2.检查操作系统是否设置了高级别的权限",
            "solutionPath": "http://note.youdao.com/noteshare?id=d8f1ea0c46dfb524af798f6b1d31cf6f",
            "isRepair": 0,
            "isDelete": 1,
            "isOpen": 1,
            "lastModifyAdmin": "",
            "updateTime": 1534387709000
        }
    ],
    "serverTime": 1535962451356
}
```

## 获取任务列表

**接口路径**： /api/render/handle/getTaskList

**请求参数**：

| **参数**       | **类型**        | 是否必须 | **说明**                         | **备注**                 |
| -------------- | --------------- | -------- | -------------------------------- | ------------------------ |
| page_num       | Integer         | N        | 当前页数                         | 默认:1                   |
| page_size      | Integer         | N        | 每页显示数量                     | 默认:100                 |
| status_list    | List\<Integer\> | N        | 状态码列表，查询列表中状态的任务 | 参见任务状态说明         |
| search_keyword | String          | N        | 场景名或者作业ID                 | 模糊搜索                 |
| start_time     | String          | N        | 搜索提交时间下限                 | 格式 yyyy-MM-dd HH:mm:ss |
| end_time       | String          | N        | 搜索提交时间上限                 | 格式 yyyy-MM-dd HH:mm:ss |

**任务状态说明**：

| **状态**            | **状态码** | **说明**       |
|---------------------|------------|----------------|
| WAITING             | 0          | 等待           |
| RENDERING           | 5          | 渲染中         |
| PRE_RENDERING       | 8          | 预处理中       |
| STOP                | 10         | 停止           |
| ARREARAGE_STOP      | 20         | 欠费停止       |
| TIME_OUT_STOP       | 23         | 超时停止       |
| FINISHED            | 25         | 已完成         |
| FINISHED_HAS_FAILED | 30         | 已完成有失败帧 |
| ABANDON             | 35         | 放弃           |
| FINISHED_TEST       | 40         | 测试完成       |
| FAILED              | 45         | 失败           |
| ANALYSE             | 50         | 分析中         |

**返回参数**：List\<TaskInfo\>

| **参数**              | **类型**             | **说明**                   | **备注**                                                     |
| --------------------- | -------------------- | -------------------------- | ------------------------------------------------------------ |
| sceneName             | String               | 场景名                     |                                                              |
| id                    | Integer              | 任务id                     |                                                              |
| taskAlias             | String               | 任务别名                   |                                                              |
| taskStatus            | Byte                 | 任务状态                   | 0/等待，5/渲染，10/停止，15/用户停止，20/因欠费停止，25/完成，30/完成包含失败帧，35/放弃，40/测试完成，45/失败，50/分析中，100/状态更新中 |
| statusText            | String               | 任务状态文本               |                                                              |
| preTaskStatus         | Byte                 | 预处理任务状态             |                                                              |
| preStatusText         | String               | 预处理状态文本             |                                                              |
| totalFrames           | Integer              | 总帧数                     |                                                              |
| abortFrames           | Integer              | 放弃帧数                   |                                                              |
| executingFrames       | Integer              | 正在运行的帧数             |                                                              |
| doneFrames            | Integer              | 完成的帧数                 |                                                              |
| failedFrames          | Integer              | 失败帧数                   |                                                              |
| framesRange           | String               | 帧范围                     |                                                              |
| projectName           | String               | 项目名                     |                                                              |
| renderConsume         | BigDecimal           | 任务渲染消费的总费用       |                                                              |
| taskArrears           | BigDecimal           | 任务欠费金额               |                                                              |
| submitDate            | Date                 | 提交时间                   |                                                              |
| startTime             | Date                 | 开始时间                   |                                                              |
| completedDate         | Date                 | 完成时间                   |                                                              |
| renderDuration        | Long                 | 任务渲染总时长             | 单位：秒                                                     |
| userName              | String               | 用户名                     |                                                              |
| producer              | String               | 制作人                     |                                                              |
| taskLevel             | Byte                 | 任务优先级                 |                                                              |
| taskUserLevel         | Integer              | 用户层面的优先级           |                                                              |
| taskLimit             | Integer              | 任务机器限制               |                                                              |
| taskOverTime          | Long                 | 任务超时提醒               |                                                              |
| outputFileName        | String               | 输出文件名                 |                                                              |
| munuTaskId            | String               | 调度器id                   |                                                              |
| layerParentId         | String               | 针对maya任务，层父id       |                                                              |
| cgId                  | Integer              | 任务类型                   | 2001/maya，2000/max                                          |
| taskKeyValueVo        | Object               | 任务关键字集合             |                                                              |
| userAccountConsume    | Bigdecimal           | 用户账户扣费               |                                                              |
| couponConsume         | Bigdecimal           | 优惠券扣费                 |                                                              |
| isOpen                | Byte                 | 前端的展开按钮是否展开     |                                                              |
| taskType              | String               | 任务类型                   | /预处理,/光子渲染,/渲染主图                                  |
| renderCamera          | String               | 渲染相机                   |                                                              |
| cloneParentId         | Integer              | 克隆任务挂在那个任务下的id |                                                              |
| cloneOriginalId       | Integer              | 从哪个任务克隆的           |                                                              |
| shareMainCapital      | Byte                 | 该任务是否共享主账号资产   | 0 不共享 ,  1 共享                                           |
| taskRam               | Integer              | 任务渲染内存               |                                                              |
| respRenderingTaskList | **List\<TaskInfo\>** | 展开的任务的子任务         | 跟此对象一样                                                 |
| layerName             | String               | 层名                       |                                                              |
| taskTypeText          | String               | 任务类型                   | 光子/主图                                                    |
| isDelete              | Byte                 | 是否删除                   | 0：已删除，1：未删除                                         |

**taskKeyValueVo实体**

| **参数**         | **类型** | **说明** | **备注** |
|------------------|----------|----------|----------|
| tiles            | String   | 分块数   |          |
| allCamera        | String   | 全部相机 |          |
| renderableCamera | String   | 渲染相机 |          |

**请求示例**：

```Python
task_list = api.query.get_task_list(page_num=1, page_size=1)
```

**返回示例**：

```json
{
    "version": "1.0.0",
    "result": true,
    "message": "success",
    "code": 200,
    "data": {
        "pageCount": 32,
        "pageNum": 1,
        "total": 32,
        "size": 1,
        "items": [
            {
                "sceneName": "衣帽间.max",
                "id": 18278,
                "taskAlias": "P18278",
                "taskStatus": 0,
                "statusText": "render_task_status_0",
                "preTaskStatus": 25,
                "preStatusText": "render_task_status_25",
                "totalFrames": 0,
                "abortFrames": null,
                "executingFrames": null,
                "doneFrames": null,
                "failedFrames": 0,
                "framesRange": "0",
                "projectName": "",
                "renderConsume": null,
                "taskArrears": 0,
                "submitDate": 1535602289000,
                "startTime": null,
                "completedDate": null,
                "renderDuration": null,
                "userName": "xiaoguotu_ljian",
                "producer": null,
                "taskLevel": 79,
                "taskUserLevel": 0,
                "taskLimit": 200,
                "taskOverTime": null,
                "userId": 10001520,
                "outputFileName": null,
                "munuTaskId": "",
                "layerParentId": 0,
                "cgId": 2001,
                "taskKeyValueVo": {
                            "tiles": null,
                            "allCamera": null,
                            "renderableCamera": null
                        },
                "userAccountConsume": null,
                "couponConsume": null,
                "isOpen": 1,
                "taskType": "",
                "renderCamera": "VRayCam003",
                "cloneParentId": null,
                "cloneOriginalId": null,
                "shareMainCapital": 0,
                "taskRam": null,
                "respRenderingTaskList": [
                    {
                        "sceneName": "衣帽间.max",
                        "id": 18280,
                        "taskAlias": "P18280",
                        "taskStatus": 25,
                        "statusText": "render_task_status_25",
                        "preTaskStatus": null,
                        "preStatusText": null,
                        "totalFrames": 1,
                        "abortFrames": 0,
                        "executingFrames": 0,
                        "doneFrames": 1,
                        "failedFrames": 0,
                        "framesRange": "0",
                        "projectName": "",
                        "renderConsume": 1.57,
                        "taskArrears": 0,
                        "submitDate": 1535602289000,
                        "startTime": 1535602601000,
                        "completedDate": 1535603874000,
                        "renderDuration": 1176,
                        "userName": "xiaoguotu_ljian",
                        "producer": null,
                        "taskLevel": 79,
                        "taskUserLevel": 0,
                        "taskLimit": 200,
                        "taskOverTime": 86400000,
                        "userId": 10001520,
                        "outputFileName": "18280_衣帽间",
                        "munuTaskId": "2018083000075",
                        "layerParentId": 18278,
                        "cgId": 2001,
                        "taskKeyValueVo": {
                            "tiles": null,
                            "allCamera": null,
                            "renderableCamera": null
                        },
                        "userAccountConsume": 0,
                        "couponConsume": 1.57,
                        "isOpen": 0,
                        "taskType": "RenderPhoton",
                        "renderCamera": "VRayCam003",
                        "cloneParentId": 0,
                        "cloneOriginalId": 0,
                        "shareMainCapital": 0,
                        "taskRam": null,
                        "respRenderingTaskList": null,
                        "layerName": null,
                        "taskTypeText": "render_photons_task",
                        "isDelete": 1
                    },
                    {
                        "sceneName": "衣帽间.max",
                        "id": 18281,
                        "taskAlias": "P18281",
                        "taskStatus": 25,
                        "statusText": "render_task_status_25",
                        "preTaskStatus": null,
                        "preStatusText": null,
                        "totalFrames": 17,
                        "abortFrames": 0,
                        "executingFrames": 0,
                        "doneFrames": 17,
                        "failedFrames": 0,
                        "framesRange": "0",
                        "projectName": "",
                        "renderConsume": 6.7,
                        "taskArrears": 0,
                        "submitDate": 1535602289000,
                        "startTime": 1535603885000,
                        "completedDate": 1535604765000,
                        "renderDuration": 5028,
                        "userName": "xiaoguotu_ljian",
                        "producer": null,
                        "taskLevel": 79,
                        "taskUserLevel": 0,
                        "taskLimit": 200,
                        "taskOverTime": 86400000,
                        "userId": 10001520,
                        "outputFileName": "18281_衣帽间",
                        "munuTaskId": "2018083000079",
                        "layerParentId": 18278,
                        "cgId": 2001,
                        "taskKeyValueVo": {
                            "tiles": null,
                            "allCamera": null,
                            "renderableCamera": null
                        },
                        "userAccountConsume": 0,
                        "couponConsume": 6.7,
                        "isOpen": 0,
                        "taskType": "Render",
                        "renderCamera": "VRayCam003",
                        "cloneParentId": 0,
                        "cloneOriginalId": 0,
                        "shareMainCapital": 0,
                        "taskRam": null,
                        "respRenderingTaskList": null,
                        "layerName": null,
                        "taskTypeText": "render_major_picture_task",
                        "isDelete": 1
                    }
                ],
                "layerName": null,
                "taskTypeText": null,
                "isDelete": 1
            }
        ]
    },
    "serverTime": 1535964116655
}
```

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

## 开始任务

**接口路径**： /api/render/handle/startTask 

**请求参数**：

| **参数**        | **类型**        | 是否必须 | **说明**   | **备注** |
| --------------- | --------------- | -------- | ---------- | -------- |
| task_param_list | List\<Integer\> | Y        | 任务号集合 |          |

**返回参数**：缺省

**请求示例**：

```Python
start_task = api.task.start_task(task_param_list=[13798105])
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

## 获取任务单页渲染帧详情

**接口路径**：  /api/render/handle/queryTaskFrames  

**请求参数**：

| **参数**       | **类型** | 是否必须 | **说明**                 | **备注**                                         |
| -------------- | -------- | -------- | ------------------------ | ------------------------------------------------ |
| task_id        | Integer  | Y        | 任务ID号                 | 任务ID号，是任务的唯一标识，必填字段             |
| search_keyword | String   | N        | 根据一机渲多帧名进行查询 | 是一个字符串，根据一机渲多帧名这个字段名进行查询 |
| page_num       | Integer  | N        | 当前页编号               | 默认1                                            |
| page_size      | Integer  | N        | 每页显示数据大小         | 默认100                                          |

**返回参数**：List\<FrameInfo\>

| **参数**         | **类型** | **说明**            | **备注**                                                                                                                                                           |
|------------------|----------|---------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| id               |          |                     |                                                                                                                                                                    |
| userId           | Long     | 用户ID              |                                                                                                                                                                    |
| framePrice       | Double   | 渲染价格            |                                                                                                                                                                    |
| feeType          | Integer  | 扣费类型            | 0 按量，1 包机，2 包项目                                                                                                                                           |
| platform         | Integer  | 平台                |                                                                                                                                                                    |
| frameIndex       | String   | 帧序列名            |                                                                                                                                                                    |
| frameBlock       | String   | 当前帧块数          |                                                                                                                                                                    |
| frameStatus      | Integer  | 当前帧状态          | 0/等待，5/渲染，10/停止，15/用户停止，20/因欠费停止，25/完成，30/完成包含失败帧，35/放弃，40/测试完成，45/失败，50/分析中，100/状态更新中 |
| feeAmount        | Double   | 余额扣费            |                                                                                                                                                                    |
| couponFee        | Double   | 代金券扣费          |                                                                                                                                                                    |
| startTime        | Long     | 开始时间（毫秒）    |                                                                                                                                                                    |
| endTime          | Long     | 结束时间（毫秒）    |                                                                                                                                                                    |
| frameExecuteTime | Long     | 渲染帧耗时          |                                                                                                                                                                    |
| frameStatusText  | String   | 帧状态描述          |                                                                                                                                                                    |
| arrearsFee       | Double   | 渲染帧欠费金额      |                                                                                                                                                                    |
| taskId           | Long     | 任务ID              |                                                                                                                                                                    |
| frameType        | Integer  | 帧类型              | 1/预渲染(只有一帧,多相机情况也只有一帧),2/光子帧,3/合并光子帧,4/优先帧,5/渲染主图帧,6/maya/max优先渲染合成帧,7/maya/max渲染主图合成帧,8/houdini结算帧，9/max通道帧 |
| recommitFlag     | Integer  | 重提次数            | 重提标识默认是0,按次数递增                                                                                                                                         |
| taskOverTime     | Integer  | 超时时间            | 帧超时时间                                                                                                                                                         |
| gopName          | String   | houdini结算节点名称 |                                                                                                                                                                    |
| frameRam         | Integer  | 帧任务渲染内存      | 如果为空说明没有内存要求                                                                                                                                           |

**请求示例**：

```python
task_frame = api.query.task_frames(task_id=13790691, page_num=1, page_size=1)
```

**返回示例**：

```json
{
    "version": "1.0.0",
    "result": true,
    "message": "success",
    "code": 200,
    "data": {
        "pageCount": 9,
        "pageNum": 1,
        "total": 17,
        "size": 2,
        "items": [
            {
                "id": 1546598,
                "userId": null,
                "framePrice": null,
                "feeType": null,
                "platform": null,
                "frameIndex": "0-1",
                "frameStatus": 4,
                "feeAmount": 0.44,
                "startTime": 1535960273000,
                "endTime": 1535960762000,
                "frameExecuteTime": 489,
                "frameStatusText": "task_frame_status_4",
                "arrearsFee": null,
                "munuJobId": "0",
                "taskId": 19088,
                "munuTaskId": "2018090300040",
                "frameType": 5,
                "couponFee": 0,
                "recommitFlag": 0,
                "isCopy": null,
                "frameBlock": "1",
                "taskOverTime": 86400000,
                "gopName": null,
                "frameRam": null
            },
            {
                "id": 1546599,
                "userId": null,
                "framePrice": null,
                "feeType": null,
                "platform": null,
                "frameIndex": "0-2",
                "frameStatus": 4,
                "feeAmount": 0.43,
                "startTime": 1535960856000,
                "endTime": 1535961338000,
                "frameExecuteTime": 482,
                "frameStatusText": "task_frame_status_4",
                "arrearsFee": null,
                "munuJobId": "1",
                "taskId": 19088,
                "munuTaskId": "2018090300040",
                "frameType": 5,
                "couponFee": 0,
                "recommitFlag": 0,
                "isCopy": null,
                "frameBlock": "2",
                "taskOverTime": 86400000,
                "gopName": null,
                "frameRam": null
            }
        ]
    },
    "serverTime": 1535966967143
}
```

## 重提失败帧

**接口路径**：  /api/rendering/task/renderingTask/recommitFailFrame

**请求参数**：

| **参数**        | **类型**        | 是否必须 | **说明**                                 | **备注** |
| --------------- | --------------- | -------- | ---------------------------------------- | -------- |
| task_param_list | List\<Integer\> | Y        | 任务号集合                               |          |
| status          | List\<Integer>  | N        | 重提的帧任务状态集合，不填表示重提失败帧 |          |

**返回参数**：缺省

**请求示例**：

```python
restart_failed_frames = api.query.restart_failed_frames(task_param_list=[13788981])
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

## 根据帧ID重提任务指定帧

**接口路径**：  /api/render/handle/recommitTaskFrames

**请求参数**：

| **参数**   | **类型**        | 是否必须 | **说明**     | **备注**                                           |
| ---------- | --------------- | -------- | ------------ | -------------------------------------------------- |
| task_id    | Integer         | N        | 任务ID       | task_id和ids_list任选其一必填                      |
| ids_list   | List\<Integer\> | N        | 帧ID集合     | task_id和ids_list任选其一必填, select_all为0时生效 |
| select_all | Integer         | N        | 是否全部重提 | 1全部重提，0指定帧重提                             |
| status     | List\<Integer>  | N        | 帧状态       | 只有传taskId才生效                                 |

**返回参数**：缺省

**请求示例**：

```python
restart_frame = api.query.restart_frame(task_id=14362099, select_all=1)
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

## 根据帧序号重提任务指定的帧

[^api]: Add in v2.4.0 

**请求参数**：

| **参数**      | **类型**  | **说明**             | **备注**                                     |
| ------------- | --------- | -------------------- | -------------------------------------------- |
| task_id       | Integer   | 子任务ID             | 如作业ID为“2W35736251”，task_id即为 35736251 |
| restartframes | List[str] | 需要重提的帧序号列表 | 例如：["6", "7-9[1]"]                        |

**请求示例**：

```python
restart_frame = api.query.get_custome_frames(task_id=37439351, restartframes=["6", "7-9[1]"])
```

**返回参数**：None

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

## 获取镭速传输信息

**接口地址**： /api/render/transfer/getServerInfo

**请求参数**：缺省

**请求示例**：

```python
transfer_server_msg = api.query.get_transfer_server_msg()
```

**返回参数**：

```json
{
    "version": "1.0.0",
    "result": true,
    "message": "success",
    "code": 200,
    "data": {
        "clientVersion": "3.2.8.2",
        "protocolVersion": "3.2.8.2",
        "raysyncTransfer": {
            "serverIp": "127.0.0.1",
            "serverPort": 2121,
            "proxyIp": "42.123.110.38",
            "proxyPort": 32001,
            "sslPort": 2443,
            "port": 2442
        }
    },
    "serverTime": 1565678980735,
    "requestId": "YenJW9-1565678980088"
}
```

## 获取镭速验证key

**接口地址**：/api/render/user/getRaySyncUserKey

**请求参数**：缺省

**请求示例**：

```python
raysync_user_key = api.query.get_raysync_user_key()
```

**返回参数**：

```json
{
	"version": "1.0.0",
	"result": true,
	"message": "success",
	"code": 200,
	"data": {
		"channel": 2,
		"platform": 2,
		"signature": "rayvision2017",
		"version": "1.0.0",
		"userKey": "5394a44e890557d8d937b92086482dab",
		"id": 1868599,
		"userName": "wsh_12345",
		"zone": 1,
		"phone": "183160224171",
		"email": "testwangshunhui@rayvision",
		"loginTime": 1565682011157,
		"infoStatus": 0,
		"accountType": 2,
		"shareMainCapital": 0,
		"subDeleteTask": 0,
		"subDeleteCapital": 1,
		"useMainBalance": 0,
		"downloadDisable": 0,
		"raySyncUserKey": "40d59041f72809ffaa16146a36780595666c681e"
	},
	"serverTime": 1565682019430,
	"requestId": "4lkn0I-1565682010026"
}
```

## 全速渲染

**接口地址**： /api/render/handle/fullSpeedRendering

**请求参数**：

| **参数**     | **类型**        | 是否必须 | **说明** |
| ------------ | --------------- | -------- | -------- |
| task_id_list | List\<Integer\> | Y        | 作业id   |

**请求示例**：

```python
full_speed_render = api.task.full_speed(task_id_list=[13652193])
```

返回参数示例：

```json
{
    "version": "1.0.0",
    "result": true,
    "message": "success",
    "code": 200,
    "data": "成功",
    "serverTime": 1578311448826,
    "requestId": "X81MN5-VGFzay1TZXJ2aWNlMDQ-1578311448620"
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

##  获取平台硬件配置信息 

[^2021/4/12]: add new interface in rayvision_api 2.8.0 

**接口路径**：/api/render/hardwareConfig/list

**请求参数**：

| **参数** | **类型**  | 是否必须 | **说明**                           |
| -------- | --------- | -------- | ---------------------------------- |
| task_ids | List[str] | N        | 任务号集合，查询指定任务的配置参数 |

**返回参数[data]**：

| 参数           | 类型      | 说明                                                         |
| -------------- | --------- | ------------------------------------------------------------ |
| id             | int       | 硬件配置id（hardwareConfigId）                               |
| type           | int       | 1:CPU;<br>2: GPU                                             |
| model          | string    | 硬件型号, 默认"Default"                                      |
| ram            | String    | 内存                                                         |
| gpuNum         | String    | GPU卡数，CPU平台为"null"                                     |
| platform       | int       | 平台号                                                       |
| current        | bool      | false/ true，当传任务号时，查询的是任务当前的硬件配置        |
| notSupportCgId | list[int] | 不支持的cgId,（cgid对应软件可以查询“常用参数设置”-->"DCC软件ID映射"） |
| status         | int       | 状态<br>1: 启用;<br>0: 禁用                                  |

**请求示例**：

```json
hardware_config = api.user.get_hardware_config(task_ids=["6306543"])
```

**返回示例**：

```json
[
    {
        "id": 301,
        "type": 1,
        "model": "Default",
        "gpuNum": null,
        "ram": "64GB",
        "platform": 2,
        "current": false,
        "notSupportCgId": [],
        "status": 1
    },
    {
        "id": 303,
        "type": 1,
        "model": "Default",
        "gpuNum": null,
        "ram": "128GB",
        "platform": 2,
        "current": false,
        "notSupportCgId": [],
        "status": 1
    },
    {
        "id": 337,
        "type": 1,
        "model": "1080Ti",
        "gpuNum": null,
        "ram": "64GB",
        "platform": 2,
        "current": true,
        "notSupportCgId": [
            2005,
            2000
        ],
        "status": 1
    },
    {
        "id": 339,
        "type": 1,
        "model": "2080Ti",
        "gpuNum": null,
        "ram": "64GB",
        "platform": 2,
        "current": false,
        "notSupportCgId": [],
        "status": 1
    },
    {
        "id": 341,
        "type": 1,
        "model": "1080Ti",
        "gpuNum": null,
        "ram": "128GB",
        "platform": 2,
        "current": false,
        "notSupportCgId": [
            2005
        ],
        "status": 1
    }
]
```

