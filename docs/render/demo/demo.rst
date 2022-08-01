空三重建生产自动脚本 demo
-----------

 ::

    from rayvision_api.core import RayvisionAPI
    from analyze_contextcapture import AnalyzeContextCapture
    from rayvision_sync.upload import RayvisionUpload
    from rayvision_sync.download import RayvisionDownload
    from rayvision_api.task.check import RayvisionCheck
    from rayvision_api.utils import update_task_info, append_to_task, append_to_upload
    import os

    # pos info
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
        "domain": "task.renderbus.com",
        "platform": "54",
        "access_id": "xxxx",
        "access_key": "xxxx",
    }

    api = RayvisionAPI(access_id=render_para['access_id'],
                       access_key=render_para['access_key'],
                       domain=render_para['domain'],
                       platform=render_para['platform'])

    # Step1:Analyze CG File
    analyze_info = {
        "cg_file": r"G:\cg_file",
        "xml_file": r"",
        "is_submit_pos": "1",
        "pos_info": {
            "field_order": FIELD_ORDER["longitude_latitude"],
            "file_path": r"H:\file\111_1.csv",
            "ignore_lines": "1",
            "splite_char": SPLIT_CHAR['space'],
            "coord_system": "EPSG:32645"
        },
        "pos_scope": {
            "is_all": "0",
            "scope": [r"G:\luotuohe\Images"]
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
        "is_set_origin_coord": "1",
        "origin_coord": {
            "coord_z": "111",
            "coord_y": "222",
            "coord_x": "333"
        },
        "is_set_offset_coord": "1",
        "offset_coord": {
            "coord_z": "444",
            "coord_y": "555",
            "coord_x": "666"
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
    api.submit(int(task_id))

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


重建 demo
-------------
 ::

    from rayvision_api.core import RayvisionAPI
    from analyze_contextcapture import AnalyzeContextCapture
    from rayvision_sync.upload import RayvisionUpload
    from rayvision_sync.download import RayvisionDownload
    from rayvision_api.task.check import RayvisionCheck
    from rayvision_api.utils import update_task_info, append_to_task, append_to_upload

    # API Parameter
    render_para = {
        "domain": "task.renderbus.com",
        "platform": "2",
        "access_id": "xxxx",
        "access_key": "xxxx",
    }

    api = RayvisionAPI(access_id=render_para['access_id'],
                       access_key=render_para['access_key'],
                       domain=render_para['domain'],
                       platform=render_para['platform'])

    # Step1:Analyze CG File
    analyze_info = {
        "cg_file": r"G:\cg_file",
        "workspace": "c:/workspace",
        "xml_file": r"G:\luotuohe\Block_6 - AT - export.xml",
        "software_version": "17.5.293",
        "world_coord_sys": "EPSG:4546",
        "output_type": ["OSGB"],
        "kml_file": r"",
        "photo_group_path": [r"G:\luotuohe\Images"],
        "project_name": "Project1",
        "sensor_size": "",
        "tile_mode": "0",
        "is_set_origin_coord": "0",
        "origin_coord": {
            "coord_z": "111",
            "coord_y": "222",
            "coord_x": "333"
        },
        "is_set_offset_coord": "0",
        "offset_coord": {
            "coord_z": "444",
            "coord_y": "555",
            "coord_x": "666"
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

