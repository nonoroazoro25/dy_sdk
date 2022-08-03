空三重建生产自动脚本 demo
-----------

 ::

    from dayan_api.core import RayvisionAPI
    from analyze_contextcapture import AnalyzeContextCapture
    from rayvision_sync.upload import RayvisionUpload
    from rayvision_sync.download import RayvisionDownload
    from dayan_api.task.check import RayvisionCheck
    from dayan_api.utils import update_task_info, append_to_task, append_to_upload
    import os

    # pos type
    FIELD_ORDER = {
        "xyz": "name|X|Y|Z",
        "yxz": "name|Y|X|Z",
        "longitude_latitude": "name|longitude|latitude|altitude",
        "latitude_longitude": "name|latitude|longitude|altitude"
    }

    # pos文件分隔符
    SPLIT_CHAR = {
        "point": ".",
        "tab": "\t",
        "space": " ",
        "comma": ",",
        "semicolon": ";"
    }

    # API Parameter
    render_para = {
        "domain": "task.dayancloud.com",
        "platform": "54",
        "access_id": "xxxx",
        "access_key": "xxxx",
    }

    api = RayvisionAPI(access_id=render_para['access_id'],
                       access_key=render_para['access_key'],
                       domain=render_para['domain'],
                       platform=render_para['platform'])


    """
    xml_file：（选填）区块文件路径，不填为提交空三，填了提交区块直接重建
    is_submit_pos:是否提交pos文件(1为是，0为否) - 默认为0
    pos_info：is_submit_pos为1时，此项必填
             field_order：经纬度顺序等
             file_path：文件本地路径
             ignore_lines：忽略行数
             splite_char：分隔符
             coord_system：坐标系
    pos_scope：如果上传pos文件，此项为必填
               is_all：是否应用于全部照片组，1为是，0为否
               scope: is_all为0时必填，填应用的照片组路径，匹配组名
    world_coord_sys：（必填）坐标系
    output_type：（必填）生产类型 可选["OSGB","OBJ","LAS","Cesium 3D Tiles","TIFF","Editable OBJ","3MX","FBX","S3C"]
    kml_file：（选填）范围文件
    photo_group_path：（必填）照片资源路径
    workspace：（必填）本地配置文件存放区
    project_name：（必填）工程名
    platform：平台代号：54
    sensor_size：（选填）传感器尺寸
    tile_mode：瓦片切块方式，0为规则水平切块，1为自适应切块（默认为0）
    is_set_origin_coord:是否自定义瓦片偏移，1为是，默认0
    origin_coord:is_set_origin_coord为1时必填，设置瓦片偏移
    is_set_offset_coord: 是否自定义生产坐标原点，1为是，默认0
    offsetCoord: is_set_offset_coord为1时必填，设置生产坐标原点
    is_many_at：是否分块空三，1为是，0为否;(默认0)
    many_at：is_many_at为1时必填，file_path为kml文件路径，block_merge为1时分块合并，0表示分块不合并
    """

    # Step1:Analyze CG File
    analyze_info = {
        "xml_file": r"",
        "is_submit_pos": "0",
        "pos_info": {
            "field_order": FIELD_ORDER["longitude_latitude"],
            "file_path": r"H:\file\111_1.csv",
            "ignore_lines": "1",
            "splite_char": SPLIT_CHAR['space'],
            "coord_system": "EPSG:32645"
        },
        "pos_scope": {
            "is_all": "1",
            "scope": []
        },
        "world_coord_sys": "EPSG:4546",
        "output_type": ["OSGB"],
        "kml_file": r"",
        "photo_group_path": [r"G:\luotuohe\Images"],
        "workspace": "c:/workspace",
        "software_version": "2019",
        "project_name": "Project1",
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
        },
        "is_many_at": "0",
        "many_at": {
            "kmls": [
                {"file_path": r"G:\luotuohe\fanwei.kml"}
            ],
            "block_merge": 0
        }
        "platform": render_para['platform']
    }

    analyze_obj = AnalyzeMaya(**analyze_info)
    analyze_obj.analyse()


    # Step2: Add some custom parameters, or update the original parameter value
    update_task = {
        "task_id": task_id,
    }
    update_task_info(update_task, analyze_obj.task_json)

    custom_info_to_task = {}
    append_to_task(custom_info_to_task, analyze_obj.task_json)

    custom_info_to_upload = []
    append_to_upload(custom_info_to_upload, analyze_obj.upload_json)

    # Step3: Set platform hardware configuration information
    hardware_config = {
        "model": "Default",  # Platform CPU: Default or Platform GPU: 1080Ti or 2080Ti
        "ram": "128GB",  # memory: 64GB or 128GB
        "gpuNum": None  # GPU platform requires input like 2*GPU, if CPU platform it is None
    }

    # Step4:Check json files
    check_obj = RayvisionCheck(api, analyze_obj)
    task_id = check_obj.execute(hardware_config, analyze_obj.task_json, analyze_obj.upload_json)

    # Step5: Transmission
    """
    Upload_method: 1: upload four json files and upload the resource file according to upload.json;
    """
    CONFIG_PATH = {
        "tips_json_path": analyze_obj.tips_json,
        "task_json_path": analyze_obj.task_json,
        "asset_json_path": analyze_obj.asset_json,
        "upload_json_path": analyze_obj.upload_json,
    }
    upload_obj = RayvisionUpload(api, automatic_line=True)

    upload_obj.upload(str(task_id), **CONFIG_PATH)

    # Step6:Submit Task
    api.submit_cc(int(task_id))

    # Step7:Download
    download = RayvisionDownload(api)

    if not analyze_info['xml_file']:
        # 存放区块文件的本地地址
        local_path = r'G:\sdk_result\at'
        # 下载区块
        rebuild_exe = download.download_block(task_id_list=[int(task_id)], local_path=local_path, download_type='block')
        print('rebuild_exe', rebuild_exe)

        if rebuild_exe is True:
            # 重建准备
            analyze_info['xml_file'] = os.path.join(local_path, 'at_result/block.xml')

            query_task_rep = api.query.task_info(task_ids_list=[task_id])
            small_task_id = query_task_rep['items'][0]['respRenderingTaskList'][1]['id']
            print('small_task_id', small_task_id)
            # 提交重建
            api.submit_cc(int(small_task_id), option='rebuild',
                          param={'outputType': analyze_info['output_type'],
                                 'worldCoordSys': analyze_info['world_coord_sys']})

            # 下载成果（任务所有帧渲染完成才开始下载）
            download.auto_download_after_task_completed([int(task_id)], download_filename_format="false",
                                                        local_path=r"G:\sdk_result", download_type='render')


提交区块重建生产 demo
-------------
 ::

    from dayan_api.core import RayvisionAPI
    from analyze_contextcapture import AnalyzeContextCapture
    from rayvision_sync.upload import RayvisionUpload
    from rayvision_sync.download import RayvisionDownload
    from dayan_api.task.check import RayvisionCheck
    from dayan_api.utils import update_task_info, append_to_task, append_to_upload

    # API Parameter
    render_para = {
        "domain": "task.dayancloud.com",
        "platform": "54",
        "access_id": "xxxx",
        "access_key": "xxxx",
    }

    api = RayvisionAPI(access_id=render_para['access_id'],
                       access_key=render_para['access_key'],
                       domain=render_para['domain'],
                       platform=render_para['platform'])

    """
    xml_file：（选填）区块文件路径，不填为提交空三，填了提交区块直接重建
    world_coord_sys：（必填）坐标系
    output_type：（必填）生产类型 可选["OSGB","OBJ","LAS","Cesium 3D Tiles","TIFF","Editable OBJ","3MX","FBX","S3C"]
    kml_file：（选填）范围文件
    photo_group_path：（必填）照片资源路径
    workspace：（必填）本地配置文件存放区
    project_name：（必填）工程名
    platform：平台代号：54
    sensor_size：（选填）传感器尺寸
    tile_mode：瓦片切块方式，0为规则水平切块，1为自适应切块（默认为0）
    is_set_origin_coord:是否自定义瓦片偏移，1为是，默认0
    origin_coord:is_set_origin_coord为1时必填，设置瓦片偏移
    is_set_offset_coord: 是否自定义生产坐标原点，1为是，默认0
    offsetCoord: is_set_offset_coord为1时必填，设置生产坐标原点
    """
    # Step1:Analyze CG File
    analyze_info = {
        "workspace": "c:/workspace",
        "xml_file": r"G:\luotuohe\Block_6 - AT - export.xml",
        "world_coord_sys": "EPSG:4546",
        "output_type": ["OSGB"],
        "kml_file": r"",
        "photo_group_path": [r"G:\luotuohe\Images"],
        "project_name": "Project1",
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
        "platform": render_para['platform']
        }
    analyze_obj = AnalyzeHoudini(**analyze_info)
    analyze_obj.analyse()


    # Step2: Add some custom parameters, or update the original parameter value
    update_task = {
    "task_id": task_id,
    }
    update_task_info(update_task, analyze_obj.task_json)

    # Step3: Set platform hardware configuration information
    hardware_config = {
        "model": "Default",  # Platform CPU: Default or Platform GPU: 1080Ti or 2080Ti
        "ram": "128GB",  # memory: 64GB or 128GB
        "gpuNum": None  # GPU platform requires input like 2*GPU, if CPU platform it is None
    }

    # Step4:Check json files
    check_obj = RayvisionCheck(api, analyze_obj)
    task_id = check_obj.execute(hardware_config, analyze_obj.task_json, analyze_obj.upload_json)

    # Step5: Transmission
    """
    Upload_method: 1: upload four json files and upload the resource file according to upload.json;
    """
    CONFIG_PATH = {
        "tips_json_path": analyze_obj.tips_json,
        "task_json_path": analyze_obj.task_json,
        "asset_json_path": analyze_obj.asset_json,
        "upload_json_path": analyze_obj.upload_json,
    }
    upload_obj = RayvisionUpload(api, automatic_line=True)

    upload_obj.upload(str(task_id), **CONFIG_PATH)

    # Step6:Submit Task
    api.submit_cc(int(task_id))

    # Step7:Download
    download = RayvisionDownload(api)

    download.auto_download_after_task_completed([int(task_id)], download_filename_format="false",
                                            local_path=r"G:\sdk_result\rebuild", download_type='render')

