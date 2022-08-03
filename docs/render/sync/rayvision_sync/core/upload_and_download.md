### 上传

#### 1. 先上传配置文件然后自动根据upload文件上传资源(任务号必须)

```
def upload(self, task_id, task_json_path, tips_json_path, asset_json_path,
           upload_json_path, max_speed=None):
    """Run the cmd command to upload the configuration file.

    Args:
        task_id (str, optional): Task id.
        task_json_path (str, optional): task.json file absolute path.
        tips_json_path (str, optional): tips.json file absolute path.
        asset_json_path (str, optional): asset.json file absolute path.
        upload_json_path (str, optional): upload.json file absolute path.
        max_speed (str): Maximum transmission speed, default value
            is 1048576 KB/S.

    Returns:
        bool: True is success, False is failure.

    """
```

使用样例:

```
from dayan_api import RayvisionAPI
from rayvision_sync.upload import RayvisionUpload

api = RayvisionAPI(access_id="xxxxx",
                   access_key="xxxxx",
                   domain="task.renderbus.com",
                   platform="2")

CONFIG_PATH = [
    r"C:\workspace\work\tips.json",
    r"C:\workspace\work\task.json",
    r"C:\workspace\work\asset.json",
    r"C:\workspace\work\upload.json",
]

upload_obj = RayvisionUpload(api)
upload_obj.upload("5165465", **CONFIG_PATH)
```


#### 2. 上传文件类型(transmit_type)

> 上传文件由参数"transmit_type"控制, 支持传输文件类型: ”upload_json“

- upload_json

  > 这种上传模式指定的“upload_json_path”文件(json文件)内容必须按照固定格式, 且只能上传文件

  例如:

  ```upload.json
  # upload.json
  {
    "asset": [
      {
        "local": "D:/houdini/CG file/local/clarisse_test1.project", 
        "server": "/D/houdini/CG file/local/clarisse_test1.project"
      }
    ]
  }
  ```

### 下载

#### 1. 以任务为粒度，当任务中帧全部渲染完成开始下载(任务号必须)

```python
    def auto_download_after_task_completed(self, task_id_list=None,
                                  max_speed=None, print_log=True,
                                  sleep_time=10,
                                  download_filename_format="true",
                                  local_path=None,
                                  engine_type="aspera", server_ip=None, server_port=None):
        """Auto download after the tasks render completed.

        Args:
            task_id_list(list of int): List of tasks ids that need to be
                downloaded.
            max_speed(str, optional): Download speed limit,
                The unit of 'max_speed' is KB/S,default value is 1048576 KB/S,
                means 1 GB/S.
            print_log(bool, optional): Print log, True: print, False: not
                print.
            sleep_time(int, optional): Sleep time between download,
                unit is second.
            download_filename_format: File download local save style,
                "true": tape task ID and scene name,
                "false" : download directly without doing processing.
            local_path (str): Download file locally save path,
                default Window system is "USERPROFILE" environment variable address splicing "renderfarm_sdk",
                Linux system is "HOME" environment variable address splicing "renderfarm_sdk".
            engine_type (str, optional): set engine type, support "aspera" and "raysync", Default "aspera".
            server_ip (str, optional): transmit server host,
                if not set, it is obtained from the default transport profile.
            server_port (str, optional): transmit server port,
                if not set, it is obtained from the default transport profile.

        Returns:
            bool: True is success.

        """
```

使用样例

```python
from dayan_api import RayvisionAPI
from rayvision_sync.download import RayvisionDownload

api = RayvisionAPI(access_id="xxx",
                   access_key="xxx",
                   domain="task.renderbus.com",
                   platform="2")

download = RayvisionDownload(api)
download.auto_download_after_task_completed([int(task_id)], download_filename_format="false",local_path=r"G:\sdk_result", download_type='render')
```


### 自动获取传输线路、指定网络提供商

#### 1.开启自动获取传输线路(默认关闭)， 设置 automatic_line = True， 例如:

- 上传自动获取传输线路:

  `RayvisionUpload(api, automatic_line=True)`

- 下载自动获取传输线路:

  `RayvisionDownload(api, automatic_line=True)`

#### 2.开启自动获取传输线路并选择网络提供商

网络商名称可以通过接口`get_transfer_config`获取)

- 上传自动获取传输线路并自定义网络商

  `RayvisionUpload(api, automatic_line=True, internet_provider="移动")`

- 下载自动获取传输线路并自定义网络商

  `RayvisionDownload(api, automatic_line=True, internet_provider="移动")`

### 选择传输模式:tcp or udp

network_mode: 控制网络传输模式
     0: 自动选择(默认值为0)
     1: tcp 传输
     2：udp 传输

```
# 以下载为例:
download.auto_download([49240085], network_mode=2)
```



### 自定义传输服务地址和传输引擎选择

> 上传服务地址一般是不需要修改，如果线路不佳也支持自定义修改

#####    1. 上传自定义传输地址和自定义传输引擎设置

> 传输引擎支持：raysync

- upload_asset

  > ```python
  > UPLOAD.upload_asset(r"D:\test\upload.json", engine_type='raysync', server_ip="45.251.92.16", server_port="12121")
  > ```

- upload_config

  ```python
  CONFIG_PATH = [
      r"C:\workspace\work\tips.json",
      r"C:\workspace\work\task.json",
      r"C:\workspace\work\asset.json",
      r"C:\workspace\work\upload.json",
  ]
  UPLOAD.upload_config(task_id="5165465",
                       config_file_list=config_list,
                       server_ip="45.251.92.16",
                       server_port="12121")
  ```

- upload

  ```python
  UPLOAD.upload(task_id="41235091",
                    engine_type='raysync',
                    server_ip="45.251.92.16",
                    server_port="12121",
                    task_json_path=r"C:\workspace\work\task.json",
                    tips_json_path=r"C:\workspace\work\tips.json",
                    asset_json_path=r"C:\workspace\work\asset.json",
                    upload_json_path=r"C:\workspace\work\upload.json")
  ```

##### 2. 下载空三区块和生产成果

- download block
  ```
  download.download_block(task_id_list=[int(task_id)], local_path=local_path, download_type='block')
  ```


- auto_download_after_task_completed
  ```
  download.auto_download_after_task_completed([49228557], local_path=r"G:\sdk_result", download_type='render')
  ```

  

