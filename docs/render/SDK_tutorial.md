# SDK 入门教程

### 一. 登陆认证

```
render_para = {
    "domain": "task.dayancloud.com",
    "platform": "54",
    "access_id": "xxxx",
    "access_key": "xxxx",
}

api = RayvisionAPI(
        access_id=render_para['access_id'],
        access_key=render_para['access_key'],
        domain=render_para['domain'],
        platform=render_para['platform']
    )
```

RayvisionAPI 参数说明:

| 参数       | 类型   | 是否必须 | 默认值             | 说明                                                         |
| ---------- | ------ | -------- | ------------------ | ------------------------------------------------------------ |
| domain     | string | 是       | task.dayancloud.com | 国内用户：task.dayancloud.com|
| platform   | string | 是       | 54                  | 平台ID          |
| access_id  | string | 是       |                    | 授权id，用于标识API调用者身份                                |
| access_key | string | 是       |                    | 授权密钥，用于加密签名字符串和服务器端验证签名字符串         |



### 二. 重建分析场景

```
from analyze_contextcapture import AnalyzeContextCapture

analyze_info = {
    "xml_file": r"G:\local\Block_1 - AT - export.xml",
    "world_coord_sys": "EPSG:4544",
    "output_type": ["OSGB"],
    "kml_file": r"",
    "photo_group_path": [r"G:\local\Images"],
    "workspace": "G:/workspace",
    "project_name": "SDK_TEST_failed",
    "platform": render_para['platform'],
    "sensor_size": "",
    "tile_mode": "0",
    "is_set_origin_coord": "0",
    "origin_coord": {
        "coord_z": "",
        "coord_y": "",
        "coord_x": ""
    },
    "is_set_offset_coord": "0",
    "offset_coord": {
        "coord_z": "",
        "coord_y": "",
        "coord_x": ""
    }
}

analyze_obj = AnalyzeContextCapture(**analyze_info)
analyze_obj.analyse()
```

说明：

- "workspace"用来控制生成json文件位置,如果不设置workspace,默认生成位置:
  
   ```
   windows : os.environ["USERPROFILE"] + "renderfarm_sdk"  
   Linux：os.environ["HOME"] + “renderfarm_sdk”
   ```
   
- 分析生成的task.json中“task_id”、“user_id”、"project_id"为空，用户可以选择自己写   入这三个参数 ,或者在check的时候自动写入此3个参数。


AnalyzeContextCapture 参数说明:

| 参数             | 类型   | 是否必须 | 默认值 | 说明                                                     |
| ---------------- | ------ | -------- | ------ | -------------------------------------------------------- |
| xml_file | string | 是       |        | 区块路径                                       |
| world_coord_sys     | string | 是       |        | 坐标系                                                   |
| output_type    | list   | 是       |        | 生产类型                       |
| kml_file        | string | 否       |    | 范围文件路径 |
| photo_group_path        | string | 是       |    | 照片组 |
| workspace        | string | 是       |    | 存放配置文件路径 |
| project_name        | string | 是       |    | 项目名 |
| platform        | string | 是       | 54   | 平台ID |
| sensor_size        | string | 否       |    | 传感器尺寸 |
| tile_mode        | string | 是       | 0   | 切块方式；0为规则水平切块，1为自适应切块 |
| is_set_origin_coord        | string | 否       |   | 是否设置重建偏移坐标  |
| origin_coord        | dict | is_set_origin_coord为1是必填  |    |重建偏移坐标  |
| is_set_offset_coord        | string | 否       |    | 是否设置生产原点坐标 |
| offset_coord        | dict | is_set_offset_coord为1时必填    |    | 设置生产原点坐标 |


### 三. 校验json文件

```
check_obj = RayvisionCheck(api, analyze_obj)
task_id = check_obj.execute(hardware_config, analyze_obj.task_json, analyze_obj.upload_json)
```


### 五. 上传

##### 1.先上传json文件再根据“upload.json”上传资源文件:

先上传四个json文件，然后传输引擎自动根据upload.json文件开始上传场景、资源等文件

`upload(self,task_id,task_json_path,tips_json_path,asset_json_path,upload_json_path, max_speed=None)`

```
CONFIG_PATH = [
    r"C:\workspace\work\tips.json",
    r"C:\workspace\work\task.json",
    r"C:\workspace\work\asset.json",
    r"C:\workspace\work\upload.json",
]
upload_obj = RayvisionUpload(api)
upload_obj.upload(str(task_id), *CONFIG_PATH)
```


### 六. 提交任务

```
api.submit_cc(int(task_id))
```


### 七. 下载

##### 1. 任务所有帧渲染完成才开始下载

`auto_download_cc_after_task_completed(self, task_id_list=None,download_filename_format="true",local_path=None,download_type='render'):`

```
download = RayvisionDownload(api)
download.auto_download_cc_after_task_completed([int(task_id)], local_path=r"G:\sdk_result", download_type='render')
```
说明: 此方法任务ID不能为空

### 八. 附加: 传输配置文件


**1. 传输配置设置包括:**

选择数据库类型，数据库文件路径设置，传输日志路径设置

**2. 默认使用的传输配置文件：db_config.ini， 如下图**

   ![db_config.ini](https://blog-tao625.oss-cn-shenzhen.aliyuncs.com/izone/blog/20200415114705.png)

   

db_config.ini 样例:

```ini
[TRANSFER_LOG_PATH]
transfer_log_path =

[DATABASE_CONFIG]
on = true
type = sqlite
db_path =D:\test\upload

[REDIS]
host = 127.0.0.1
port = 6379
password =
table_index = 0
timeout = 5000

[SQLITE]
temporary = false
```

用户也可根据默认配置为模板修改配置并指定数据库配置文件位置,指定自定义配置文件方法如下

```
from rayvision_sync.upload import RayvisionUpload

UPLOAD = RayvisionUpload(api, db_config_path=r"D:\test\upload\db_config.ini")
```

**3. db_config.ini 参数说明:**

| 参数              | 说明                                                         | 默认值    |
| ----------------- | ------------------------------------------------------------ | --------- |
| transfer_log_path | 传输引擎日志文件路径                                         | 无        |
| on                | 是否使用本地数据库, true / false: 是 / 否                    | true      |
| type              | 选择数据库, 目前仅支持"redis" 和 "sqlite"                    | sqlite    |
| db_path           | 数据库文件保存路径                                           | 无        |
| host              | redis数据库host                                              | 127.0.0.1 |
| port              | redis数据库port                                              | 6379      |
| password          | redis数据库password                                          | 无        |
| table_index       | redis数据库保存文件的仓库名，选择redis数据库则不能为空       | 无        |
| timeout           | redis客户端连接超时时间,客户端在这段时间内没有发出任何指令，那么关闭该连接,单位ms | 5000      |
| temporary         | 使用sqlite数据库时，上传的记录数据是否在完成上传后删除, 默认"false"不删除 | false     |


**4. transfer_log_path 和 db_path 取值的优先级规则如下：**

- db_config.ini有设置自定义路径则优先使用自定义路径；

- 无自定义路径则如下:

  transfer_log_path

  > - 优先使用环境变量'RAYVISION_LOG'
  >
  > - 次之使用:  
  >
  >     window: 环境变量"USERPROFILE"位置/<renderfarm_sdk>  
  >     Linux：环境变量"HOME"位置/<renderfarm_sdk>  

  db_path

  > - 优先使用环境变量'RAYVISION_LOG'
  >
  > - 次之使用:  
  >
  >     window: 环境变量"USERPROFILE"位置/<renderfarm_sdk>  
  >     Linux：环境变量"HOME"位置/<renderfarm_sdk> 

