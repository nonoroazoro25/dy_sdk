CC 配置文件文档
======

> 分析：我们将场景中需要的信息分析出来并保存到task.json, asset.json, upload.json, tips.json中，以便进一步解析和处理


### 1.task.json解析


> 说明: 存放场景分析结果、渲染设置等信息


**task.json示例**


```json
{
  "user_setting": {
    "user_key": "rsat:4MIiDYdYSwsTnCaRKFVy4ghNrGv",
    "user_id": 100572091,
    "user_name": "hai15130920706",
    "acount_type": 1,
    "parent_id": 0,
    "shareMainCapital": false,
    "zone": 1
  },
  "many_at": {
    "block_merge": 1,
    "kmls": [
      {
        "kml_name": "F:/hubei/KML/1.kml",
        "kml_id": "0",
        "total_pixel": "",
        "content": "PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0iVVRGLTgiPz4KPGttbD4KICA8RG9jdW1lbnQ+CiAgICA8UGxhY2VtYXJrPgogICAgICA8bmFtZT5RSzE8L25hbWU+CiAgICAgIDx2aXNpYmlsaXR5PjE8L3Zpc2liaWxpdHk+CiAgICAgIDxQb2x5Z29uPgogICAgICAgIDxhbHRpdHVkZU1vZGU+Y2xhbXBUb0dyb3VuZDwvYWx0aXR1ZGVNb2RlPgogICAgICAgIDxvdXRlckJvdW5kYXJ5SXM+CiAgICAgICAgICA8TGluZWFyUmluZz4KICAgICAgICAgICAgPGNvb3JkaW5hdGVzPgogICAgICAgICAgICAgIDExNC42NzQ1MjE0MDU0LDI5LjY3Mjk3NjIxNiwwCiAgICAgICAgICAgICAgMTE0LjY3NDg5Njc5NDMsMjkuNzAyOTAzMDU4NywwCiAgICAgICAgICAgICAgMTE0LjY5MTE4OTQwNTgsMjkuNzAwNDc2OTk2MSwwCiAgICAgICAgICAgICAgMTE0LjY5NzU4Njg2MDMsMjkuNjkxMzYxMjQ5OCwwCiAgICAgICAgICAgICAgMTE0LjY5MTMxMzQzMSwyOS42Nzg1MzQ4NzQ5LDAKICAgICAgICAgICAgICAxMTQuNjg3MDIwMTYwMywyOS42NzI2MTc3MTA5LDAKICAgICAgICAgICAgICAxMTQuNjc0NTIxNDA1NCwyOS42NzI5NzYyMTYsMAogICAgICAgICAgICA8L2Nvb3JkaW5hdGVzPgogICAgICAgICAgPC9MaW5lYXJSaW5nPgogICAgICAgIDwvb3V0ZXJCb3VuZGFyeUlzPgogICAgICA8L1BvbHlnb24+CiAgICA8L1BsYWNlbWFyaz4KICA8L0RvY3VtZW50Pgo8L2ttbD4KDQo=",
        "fileSize": "1255"
      },
      {
        "kml_name": "F:/hubei/KML/2.kml",
        "kml_id": "1",
        "total_pixel": "",
        "content": "PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0iVVRGLTgiPz4KPGttbD4KICA8RG9jdW1lbnQ+CiAgICA8UGxhY2VtYXJrPgogICAgICA8bmFtZT5RSzM8L25hbWU+CiAgICAgIDx2aXNpYmlsaXR5PjE8L3Zpc2liaWxpdHk+CiAgICAgIDxQb2x5Z29uPgogICAgICAgIDxhbHRpdHVkZU1vZGU+Y2xhbXBUb0dyb3VuZDwvYWx0aXR1ZGVNb2RlPgogICAgICAgIDxvdXRlckJvdW5kYXJ5SXM+CiAgICAgICAgICA8TGluZWFyUmluZz4KICAgICAgICAgICAgPGNvb3JkaW5hdGVzPgogICAgICAgICAgICAgIDExNC42NzQ3OTQzNTAxLDI5LjcwNDYyNTY3NTYsMAogICAgICAgICAgICAgIDExNC42Nzk3MjA5MTg1LDI5LjcwMzg4MDIxODMsMAogICAgICAgICAgICAgIDExNC42NzkzMTAwMTU2LDI5LjY4NDIyMzk4OTIsMAogICAgICAgICAgICAgIDExNC42Nzc0NzA4OTQyLDI5LjY4Mzc3Nzg3MTQsMAogICAgICAgICAgICAgIDExNC42Njg5NTYxNTcyLDI5LjY4NDQ2MTQwMiwwCiAgICAgICAgICAgICAgMTE0LjY2MjgxNzIwMTEsMjkuNjgxNTkwMjU0NSwwCiAgICAgICAgICAgICAgMTE0LjY1MTQzMjkxMTMsMjkuNjgwMTI0OTIzMywwCiAgICAgICAgICAgICAgMTE0LjY1MTUwMzkzMzksMjkuNjkwODc0NTYwMywwCiAgICAgICAgICAgICAgMTE0LjY1NzUwOTQ2NTksMjkuNzAwNzE4NjAzNCwwCiAgICAgICAgICAgICAgMTE0LjY3NDc5NDM1MDEsMjkuNzA0NjI1Njc1NiwwCiAgICAgICAgICAgIDwvY29vcmRpbmF0ZXM+CiAgICAgICAgICA8L0xpbmVhclJpbmc+CiAgICAgICAgPC9vdXRlckJvdW5kYXJ5SXM+CiAgICAgIDwvUG9seWdvbj4KICAgIDwvUGxhY2VtYXJrPgogIDwvRG9jdW1lbnQ+Cjwva21sPgoNCg==",
        "fileSize": "1256"
      },
      {
        "kml_name": "F:/hubei/KML/3.kml",
        "kml_id": "2",
        "total_pixel": "",
        "content": "PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0iVVRGLTgiPz4KPGttbD4KICA8RG9jdW1lbnQ+CiAgICA8UGxhY2VtYXJrPgogICAgICA8bmFtZT5RSzQ8L25hbWU+CiAgICAgIDx2aXNpYmlsaXR5PjE8L3Zpc2liaWxpdHk+CiAgICAgIDxQb2x5Z29uPgogICAgICAgIDxhbHRpdHVkZU1vZGU+Y2xhbXBUb0dyb3VuZDwvYWx0aXR1ZGVNb2RlPgogICAgICAgIDxvdXRlckJvdW5kYXJ5SXM+CiAgICAgICAgICA8TGluZWFyUmluZz4KICAgICAgICAgICAgPGNvb3JkaW5hdGVzPgogICAgICAgICAgICAgIDExNC42NTA1ODk2NzIzLDI5LjY4MDkwOTY4NTUsMAogICAgICAgICAgICAgIDExNC42NjMzMDIxMTQ0LDI5LjY4MjgyNzQ1MDQsMAogICAgICAgICAgICAgIDExNC42NjkzMjAxNTMzLDI5LjY4NTk3MTI3MSwwCiAgICAgICAgICAgICAgMTE0LjY3OTE5NTEyMjcsMjkuNjg0OTI1MTc1MSwwCiAgICAgICAgICAgICAgMTE0LjY3OTMzNjMwMzEsMjkuNjcxNTM3MTkwMiwwCiAgICAgICAgICAgICAgMTE0LjY2NDE1MjAxMDc3NCwyOS42NjU0MDQ1NTk5ODU4LDAKICAgICAgICAgICAgICAxMTQuNjU1MzM3NTc1OSwyOS42Njk2NDI0MjI5LDAKICAgICAgICAgICAgICAxMTQuNjUwMDU1OTc4NSwyOS42NzM4NDg3MTgzLDAKICAgICAgICAgICAgICAxMTQuNjUwNTg5NjcyMywyOS42ODA5MDk2ODU1LDAKICAgICAgICAgICAgPC9jb29yZGluYXRlcz4KICAgICAgICAgIDwvTGluZWFyUmluZz4KICAgICAgICA8L291dGVyQm91bmRhcnlJcz4KICAgICAgPC9Qb2x5Z29uPgogICAgPC9QbGFjZW1hcms+CiAgPC9Eb2N1bWVudD4KPC9rbWw+Cg0K",
        "fileSize": "1136"
      }
    ]
  },
  "plugin_setting": {
    "render_layer_type": "0",
    "cg_name": "",
    "cg_version": "",
    "software_config": {
      "plugins": {},
      "os_name": "1",
      "cg_inst_dir": "",
      "cg_name": "ContextCapture",
      "cg_version": ""
    },
    "project_dir": "",
    "os_name": "1",
    "project_id": 0,
    "language": 0,
    "config_name": "",
    "project_name": "",
    "project_output": "C:/DayanCloud/Download",
    "edit_name": ""
  },
  "client_setting": {
    "login_name": "Administrator",
    "build": "Build 2022-6-30",
    "client_cmd": "rendercmd.exe",
    "date_time": "2022-07-30 10:45:56",
    "status": "1",
    "language": 0,
    "version": "5.0.4.9",
    "ip": "192.168.2.124",
    "client_inst_path": "D:/ProgramData/Rayvision/DayanCloud5.0",
    "auto_download": false,
    "mac": "7C:10:C9:43:DF:E0",
    "client_project_dir": "C:/DayanCloud/Project/192929",
    "transmit_line": "电信",
    "system_locale": "zh_CN",
    "mode": "",
    "client": "Renderbus",
    "param_set_enabled": true,
    "os": "Windows 10 (10.0)",
    "transmit_engine": "RaySync"
  },
  "scene_info_render": {
    "param": {
      "tileSize": "",
      "outputType": [
        "OSGB"
      ],
      "rangeFile": {},
      "lockRange": 1,
      "tileMode": "0",
      "worldCoordSys": "EPSG:4547"
    },
    "run_model": "normal",
    "group": {
      "groups": [
        {
          "pic_height": 5304,
          "pic_count": 560,
          "group_name": "6",
          "focal_length": "56",
          "pic_width": 7952,
          "group_path": "F:/hubei/0615/6",
          "total_pixel": "23619348480",
          "group_id": "{582af9e3-0e85-4bc7-8fb4-ad9e0eda7c3b}",
          "pos_info": {},
          "camera_producter": "SONY",
          "camera_model": "ILCE-7RM2",
          "sensor_size": "35.9"
        },
        {
          "pic_height": 5304,
          "pic_count": 673,
          "group_name": "1",
          "focal_length": "56",
          "pic_width": 7952,
          "group_path": "F:/hubei/0616/1",
          "total_pixel": "28385395584",
          "group_id": "{1fb70bc0-e937-4efe-98d5-9f59cf7bfdfa}",
          "pos_info": {},
          "camera_producter": "SONY",
          "camera_model": "ILCE-7RM2",
          "sensor_size": "35.9"
        }
      ],
      "total_pixel": "899656349952",
      "project_name": "XK1",
      "pic_count": 28553,
      "job_type": 0
    },
    "blocks_info": [
      {
        "file_path": ""
      }
    ],
    "contrl_point": {},
    "blocks": [
      "1"
    ]
  },
  "driver_mnt_map": {
    "F:": "\\\\10.117.144.100\\d\\inputdata5\\100572000\\100572091\\F"
  },
  "software_config": {
    "plugins": {},
    "os_name": "1",
    "cg_inst_dir": "",
    "cg_name": "ContextCapture",
    "cg_version": ""
  },
  "scene_info": {
    "group": {
      "groups": [
        {
          "pic_height": 5304,
          "pic_count": 560,
          "group_name": "6",
          "focal_length": "56",
          "pic_width": 7952,
          "group_path": "F:/hubei/0615/6",
          "total_pixel": "23619348480",
          "group_id": "{582af9e3-0e85-4bc7-8fb4-ad9e0eda7c3b}",
          "pos_info": {},
          "camera_producter": "SONY",
          "camera_model": "ILCE-7RM2",
          "sensor_size": "35.9"
        },
        {
          "pic_height": 4000,
          "pic_count": 907,
          "group_name": "4",
          "focal_length": "35",
          "pic_width": 6000,
          "group_path": "F:/hubei/0712/2/zp/4",
          "total_pixel": "21768000000",
          "group_id": "{7a982170-5c72-41e1-ac8c-6cf90453f8a1}",
          "pos_info": {},
          "camera_producter": "SONY",
          "camera_model": "ILCE-5100",
          "sensor_size": "23.5"
        }
      ],
      "total_pixel": "899656349952",
      "project_name": "XK1",
      "pic_count": 28553,
      "job_type": 0
    },
    "blocks_info": [
      {
        "file_path": ""
      }
    ],
    "param": {
      "tileSize": "",
      "outputType": [
        "OSGB"
      ],
      "rangeFile": {},
      "lockRange": 1,
      "tileMode": "0",
      "worldCoordSys": "EPSG:4547"
    },
    "contrl_point": {},
    "blocks": [
      "1"
    ]
  },
  "task_info": {
    "job_id_alias": "192929",
    "edit_name": "",
    "stop_after_test": "1",
    "platform": "54",
    "distribute_node": "1",
    "input_project_path": "",
    "channel": "9",
    "is_picture": "1",
    "time_out": "43200",
    "task_id": "192929",
    "project_id": "0",
    "config_name": "",
    "project_name": "XK1",
    "render_layer_type": "0",
    "job_id": "192929",
    "tiles_type": "strip",
    "job_stop_time": "259200",
    "pre_frames": "",
    "display_common_tiles": "1",
    "cg_id": "2017",
    "locationoutput": "C:/DayanCloud/Download",
    "graphics_cards_num": "2",
    "input_cg_file": "F:/hubei/0615/6",
    "tiles": "1",
    "is_distribute_render": "0",
    "frames_per_task": "1",
    "task_stop_time": "259200",
    "ram": "32"
  },
  "render_setting": {
    "ignoreAnalyseWarn": 0,
    "ignoreMapFlag": 0,
    "manuallyStartAnalysisFlag": 0
  },
  "small_task_id": "202551"
}
```


**task.json参数解析**


参数 | 类型 | 是否必须 | 说明 | 示例
---|---|---|---|---
software_config | object | Y | 渲染环境（软件类型、版本和用到的插件等） | [见software_config对象解析](#software_config)
task_info | object | Y | 渲染设置（优先帧、渲染帧数、超时时间等） | [见task_info对象解析](#task_info)
scene_info_render | object | Y | 场景的分析结果（场景中的渲染节点、输出路径等） | [见scene_info_render对象解析](#scene_info_render)
layers | list | Y | 所有层信息，值是“scene_info_render”中的层名称 | "layers": [<br/>        "defaultRenderLayer",<br/>        "mut",<br/>    ] 

**<span id="software_config">software_config对象解析</span>**


参数 | 类型 | 是否必须 | 说明 | 示例
---|---|---|---|---
cg_name | string | Y | 软件名称 | "Maya"
cg_version | string | Y | 软件版本 | "2016"
plugins | object | Y | 插件对象。<br> 为插件名称，value为插件版本 | {}

**<span id="task_info">task_info对象解析</span>**

| 参数                   | 类型   | 是否必须 | 说明                                                         | 默认值   | 示例                                                         |
| ---------------------- | ------ | -------- | ------------------------------------------------------------ | -------- | ------------------------------------------------------------ |
| graphics_cards_num     | string | Y        | 1: 开启单卡渲染 2: 开启双卡渲染                              | "2"      | “2”                                                          |
| enable_layered         | string | Y        | 是否开启分层提交, "0":关闭 "1":开启                          | "0"      | "0"                                                          |
| cg_id                  | string | Y        | 渲染软件id."2000": Maya                                  |          | "2013"                                                       |
| ram                    | string | Y        | 内存要求: 64 / 128                                           | “64”     | "64"                                                         |
| os_name                | string | Y        | 渲染操作系统:  "0":Linux; "1": Windows                       | “1”      | "1"                                                          |
| render_layer_type      | string | Y        | 渲染层方式选择:  "0"：renderlayer方式 "1"：rendersetup方式   | “0”      | "0"                                                          |
| is_distribute_render   | string | N        | 是否开启分布式渲染:  "0":关闭 "1":开启                       | “0”      | "0"                                                          |
| input_cg_file          | string | Y        | 渲染场景本地路径                                             |          | "E:/copy/DHGB_sc05_zhuta_610-1570_v0102.project"             |
| input_project_path     | string | Y        | 项目路径，如用户未设置传空字符串                             | " "      |                                                              |
| job_stop_time          | string | Y        | 设置帧的超时时间，只会影响当前帧, 单位秒                     | “259200” | "28800"                                                      |
| user_id                | string | Y        | 用户ID                                                       |          |                                                              |
| pre_frames             | string | Y        | 优先渲染(优先帧不建议自定义多个单独帧)                       | “000”    | "000:1,3-4[1]" 表示： 优先渲染首帧：否 优先渲染中间帧：否 优先渲染末帧：否 优先渲染自定义帧：1,3-4[1] |
| platform               | string | Y        | 提交平台: "2": "www2", "3": "www3", "6": "www4", "21": "gpu", |          | "2"                                                          |
| is_picture             | string | Y        | “0: 效果图 "1": 动画图                                       | “0”      | "0"                                                          |
| channel                | string | Y        | 1:web本地分析(动画扣费); 2:web云端分析; 3:效果图插件提交； 4：API/SDK提交; 8：动画插件提交 | “4”      | "4"                                                          |
| tiles_type             | string | Y        | "block(分块),strip(分条)"                                    | “block”  | "block"                                                      |
| tiles                  | string | Y        | 分块数量，大于1就分块或者分条，等于1 就是单机                | "1"      | "1"                                                          |
| project_id             | string | Y        | 项目id                                                       |          | "200953"                                                     |
| project_name           | string | Y        | 项目名称                                                     | " "      | "Project1"                                                   |
| distribute_render_node | string | N        | 分布式渲染机器数                                             | "3"      | "3"                                                          |
| frames_per_task        | string | Y        | 一机渲多帧的帧数量                                           | "1"      | "1"                                                          |
| stop_after_test        | string | Y        | 优先渲染完成后是否暂停任务 "1":优先渲染完成后暂停任务 "2".优先渲染完成后不暂停任务 | "2"      | “2”                                                          |
| task_id                | string | Y        | 任务号                                                       |          |                                                              |
| task_stop_time         | string | Y        | 大任务超时停止 单位秒,"0"表示不限制                          | "0"      | "86400"                                                      |
| time_out               | string | Y        | 超时时间 单位秒                                              | “43200”  | "43200"                                                      |

> **注意**:
> -

**<span id="scene_info_render">scene_info_render对象解析</span>**


**参数** | **类型** | **是否必须** | **说明** | **示例** 
---|---|---|---|---
**layer** | **object** | **Y** | **层信息** | **[见scene_info_render.layer对象解析](#scene_info_render.layer)** 

**<span id="scene_info_render.layer">scene_info_render.layer对象解析</span>**


参数 | 类型 |  | 说明 | 示例
---|---|---|---|---
renderable | string | Y | 渲染层开关 | "1"
env | object | N | 环境信息 | {}
is_default_camera | string | N | 是否使用默认相机，默认值为‘1’(使用默认相机) | "1" 
option | string | N | 渲染器对应信息 | ""
common | object | Y | 场景普通信息 | [见scene_info_render.layer.common对象解析](#scene_info_render.layer.common)


**<span id="scene_info_render.layer.common">scene_info_render.layer.common对象解析</span>**


参数 | 类型 | 是否必须 | 说明 | 示例
---|---|---|---|---
image_format | string | Y | 渲染元素输出文件类型 | "jpg"
end | string | Y | 结束帧 | "100"
width | string | Y | 分辨率，宽 | "1920"
image_file_prefix | string | Y | 输出文件名设置，"<RenderLayer>/<Scence>" | ""
all_camera | array<string> | Y | 所有相机列表 | ["stereoCameraRightShape", "cameraShape1"]
render_camera | array<string> | Y | 待渲染相机列表 | ["stereoCameraRightShape"]
start | string | Y | 起始帧 | "1"
animation | string | N | 动画开关 | "False"
renderer | string | Y | 渲染器名称 | “arnold“
frames | string | Y | 渲染帧 | "1-10[1]"
height | string | Y | 分辨率，高 | "1080"
renumber_frames | string | N | 帧覆盖 | "False" 
by_frame | string | Y | 帧间隔 | "1"


### 2.upload.json解析


> 说明: 存放需要上传的资产路径信息


**upload.json示例**
```json
{
  "asset": [
    {
      "local": "F:/test_data/0801/6/DJ00001.JPG",
      "server": "/F/test_data/0801/6/DJ00001.JPG"
    }
  ]
}
```


**upload.json参数解析**


参数 | 类型 | 说明 | 示例
---|---|---|---
asset | object | 需要上传的资产路径信息 | [见asset对象解析](#asset)


**<span id="asset">asset对象解析</span>**


参数 | 类型 | 说明 | 示例
---|---|---|---
local | string | 资产本地路径 | "F:/test_data/0801/6/DJ00001.JPG"
server | string | 服务器端相对路径，一般与local保持一致 | "/F/test_data/0801/6/DJ00001.JPG"


### 3.tips.json解析


> 说明: 存放分析出的错误、警告信息


```json
{}
```

