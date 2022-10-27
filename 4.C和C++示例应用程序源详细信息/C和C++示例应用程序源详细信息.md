# C和C++示例应用程序源详细信息

DeepStream SDK 包包括包含插件、库、应用程序和源代码的档案。 对于 Debian 安装（在 Jetson 或 dGPU 上）和 SDK Manager 安装，源目录位于 `/opt/nvidia/deepstream/deepstream-6.1/sources`。 对于 tar 包，源文件位于提取的 deepstream 包中。 DeepStream Python 绑定和示例应用程序可作为单独的包提供。 有关更多信息，请参阅 https://github.com/NVIDIA-AI-IOT/deepstream_python_apps。

使用 Graph Composer 创建的 DeepStream 图列在[参考图部分](https://docs.nvidia.com/metropolis/deepstream/dev-guide/text/DS_Zero_Coding_Sample_Graphs.html)下。 有关详细信息，请参阅 [Graph Composer 简介](https://docs.nvidia.com/metropolis/deepstream/dev-guide/text/DS_Zero_Coding_Introduction.html)。


<div><table class="colwidths-given docutils align-default" id="id2">
<caption><span class="caption-text">Sample source details</span><a class="headerlink" href="#id2" title="Permalink to this table">¶</a></caption>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="row-odd"><th class="head"><p>参考测试应用</p></th>
<th class="head"><p>源目录中的路径</p></th>
<th class="head"><p>描述</p></th>
</tr>
</thead>
<tbody>
<tr class="row-even"><td><p>Sample test application 1</p></td>
<td><p>apps/sample_apps/deepstream-test1</p></td>
<td><p>如何将 DeepStream 元素用于单个 H.264 流的示例：filesrc → decode → nvstreammux → nvinfer（primary detector） → nvdsosd → renderer。 这个应用程序使用 resnet10.caffemodel 进行检测。</p></td>
</tr>
<tr class="row-odd"><td><p>Sample test application 2</p></td>
<td><p>apps/sample_apps/deepstream-test2</p></td>
<td><p>如何将 DeepStream 元素用于单个 H.264 流的示例： filesrc → decode → nvstreammux → nvinfer (primary detector) → nvtracker → nvinfer (secondary classifier) → nvdsosd → renderer. 这个应用程序使用 resnet10.caffemodel 进行检测和 3 个分类器模型（即 Car Color、Make 和 Model）.</p></td>
</tr>
<tr class="row-even"><td><p>Sample test application 3</p></td>
<td><p>apps/sample_apps/deepstream-test3</p></td>
<td><p>基于 deepstream-test1（简单测试应用程序 1）构建，演示如何：</p>
<blockquote>
<div><ul class="simple">
<li><p>在流程中使用多个来源。</p></li>
<li><p>使用 uridecodebin 接受任何类型的输入（例如 RTSP/文件）、任何 GStreamer 支持的容器格式和任何编解码器。</p></li>
<li><p>配置 Gst-nvstreammux 以生成一批帧并对其进行推断以更好地利用资源。</p></li>
<li><p>提取流元数据，其中包含有关批处理缓冲区中帧的有用信息。</p></li>
</ul>
</div></blockquote>
<p>这个应用程序使用 resnet10.caffemodel 进行检测。</p>
</td>
</tr>
<tr class="row-odd"><td><p>Sample test application 4</p></td>
<td><p>apps/sample_apps/­deepstream-test4</p></td>
<td><p>基于 deepstream-test1 构建单个 H.264 流：filesrc、decode、nvstreammux、nvinfer、nvdsosd、renderer 以演示如何：</p>
<blockquote>
<div><ul class="simple">
<li><p>在流程中使用 Gst-nvmsgconv 和 Gst-nvmsgbroker 插件。</p></li>
<li><p>创建 NVDS_META_EVENT_MSG 类型元数据并将其附加到缓冲区。</p></li>
<li><p>将 NVDS_META_EVENT_MSG 用于不同类型的对象，例如 车辆和人。</p></li>
<li><p>如果元数据通过 extMsg 字段扩展，则实现“复制”和“释放”功能以供使用。</p></li>
</ul>
</div></blockquote>
<p>这个应用程序使用 resnet10.caffemodel 进行检测。</p>
</td>
</tr>
<tr class="row-even"><td><p>Sample test application 5</p></td>
<td><p>apps/sample_apps/­deepstream-test5</p></td>
<td><p>构建在 deepstream-app 之上。 证明：</p>
<blockquote>
<div><ul class="simple">
<li><p>在多流流程中使用 Gst-nvmsgconv 和 Gst-nvmsgbroker 插件。</p></li>
<li><p>如何将配置文件中的 Gst-nvmsgbroker 插件配置为接收器插件（用于 KAFKA、Azure 等）。</p></li>
<li><p>如何处理来自 RTSP 服务器或摄像头的 RTCP 发送方报告，并将 Gst Buffer PTS 转换为 UTC 时间戳。</p></li>
</ul>
</div></blockquote>
<p>有关详细信息，请参阅 deepstream_test5_app_main.c 中的 RTCP Sender Report 回调函数 test5_rtcp_sender_report_callback() 注册和使用。 使用 rtpmanager 元素的“handle-sync”信号注册 GStreamer 回调记录在 apps-common/src/deepstream_source_bin.c 中。</p>
<p>这个应用程序使用 resnet10.caffemodel 进行检测。</p>
</td>
</tr>
<tr class="row-odd"><td><p>AMQP protocol test application</p></td>
<td><p>libs/amqp_­protocol_adaptor</p></td>
<td><p>用于测试 AMQP 协议的应用程序。 这个应用程序使用 resnet10.caffemodel 进行检测。</p></td>
</tr>
<tr class="row-even"><td><p>Azure MQTT test application</p></td>
<td><p>libs/azure_protocol_adaptor</p></td>
<td><p>测试应用程序以使用 MQTT 显示 Azure IoT device2edge 消息传递和 device2cloud 消息传递。 这个应用程序使用 resnet10.caffemodel 进行检测。</p></td>
</tr>
<tr class="row-odd"><td><p>DeepStream reference application</p></td>
<td><p>apps/sample_apps/­deepstream-app</p></td>
<td><p>DeepStream 参考应用程序的源代码。 这个应用程序使用 resnet10.caffemodel 进行检测和 3 个分类器模型（即 Car Color、Make 和 Model）。</p></td>
</tr>
<tr class="row-even"><td><p>UFF SSD detector</p></td>
<td><p>sources/objectDetector_SSD</p></td>
<td><p>SSD 检测器模型的配置文件和自定义库实现。</p></td>
</tr>
<tr class="row-odd"><td><p>Faster RCNN detector</p></td>
<td><p>sources/objectDetector_FasterRCNN</p></td>
<td><p>FasterRCNN 模型的配置文件和自定义库实现。</p></td>
</tr>
<tr class="row-even"><td><p>Yolo detector</p></td>
<td><p>sources/objectDetector_Yolo</p></td>
<td><p>Yolo 模型的配置文件和自定义库实现，目前是 Yolo v2、v2 tiny、v3 和 v3 tiny。</p></td>
</tr>
<tr class="row-odd"><td><p>Dewarper example</p></td>
<td><p>apps/sample_apps/deepstream-dewarper-test</p></td>
<td><p>演示单个或多个 360 度摄像机流的 dewarper 功能。 从 CSV 文件中读取相机校准参数，并在显示屏上渲染通道和光斑表面。</p></td>
</tr>
<tr class="row-even"><td><p>Optical flow example</p></td>
<td><p>apps/sample_apps/deepstream-nvof-test</p></td>
<td><p>演示单个或多个流的光流功能。 此示例使用两个 GStreamer 插件（Gst-nvof 和 Gst-nvofvisual）。 Gst-nvof 元素生成 MV（运动矢量）数据并将其作为用户元数据附加。 Gst-nvofvisual 元素使用预定义的色轮矩阵可视化 MV 数据。</p></td>
</tr>
<tr class="row-odd"><td><p>Custom meta data example</p></td>
<td><p>apps/sample_apps/deepstream-user-metadata-test</p></td>
<td><p>演示如何将自定义或用户特定的元数据添加到 DeepStream 的任何组件。 测试代码将一个填充了用户数据的 16 字节数组附加到所选组件。 数据在另一个组件中检索。 这个应用程序使用 resnet10.caffemodel 进行检测。</p></td>
</tr>
<tr class="row-even"><td><p>MJPEG and JPEG decoder and inferencing example</p></td>
<td><p>apps/sample_apps/deepstream-image-decode-test</p></td>
<td><p>建立在 deepstream-test3 上，以演示图像解码而不是视频。 此示例使用自定义解码箱，因此 MJPEG 编解码器可用作输入。 这个应用程序使用 resnet10.caffemodel 进行检测。</p></td>
</tr>
<tr class="row-odd"><td><p>Image/Video segmentation example</p></td>
<td><p>apps/sample_apps/deepstream-segmentation-test</p></td>
<td><p>演示使用语义或工业神经网络对多流视频或图像进行分割并将输出渲染到显示器。 此应用程序将 unet_output_graph.uff 用于工业用例，将 unetres18_v4_pruned0.65_800_data.uff 用于语义用例。</p></td>
</tr>
<tr class="row-even"><td><p>Handling metadata before Gst-nvstreammux</p></td>
<td><p>apps/sample_apps/deepstream-gst-metadata-test</p></td>
<td><p>演示如何在 DeepStream 流程中的 Gst-nvstreammux 插件之前设置元数据，以及如何在 Gst-nvstreammux 之后访问它。 这个应用程序使用 resnet10.caffemodel 进行检测。</p></td>
</tr>
<tr class="row-odd"><td><p>Gst-nvinfer tensor meta flow example</p></td>
<td><p>apps/sample_apps/deepstream-infer-tensor-meta-app</p></td>
<td><p>演示如何将 nvinfer 张量输出作为元数据进行流动和访问。 注意：由于 OpenCV 已弃用，此二进制文件未打包。 此应用程序需要由用户编译。 这个应用程序使用 resnet10.caffemodel 进行检测和 3 个分类器模型（即 Car Color、Make 和 Model）。</p></td>
</tr>
<tr class="row-even"><td><p>Preprocess example</p></td>
<td><p>apps/sample_apps/deepstream-preprocess-test</p></td>
<td><p>演示对为流配置的预处理 ROI 的推断。 这个应用程序使用 resnet10.caffemodel 进行检测。</p></td>
</tr>
<tr class="row-odd"><td><p>3D action recognition Reference app</p></td>
<td><p>apps/sample_apps/deepstream-3d-action-recognition</p></td>
<td><p>演示用于动作识别的基于序列批处理的 3D 或 2D 模型推理流程。 它还包括一个用于 NCSHW 时间批处理的基于序列的预处理自定义库。 在运行应用程序之前，请参阅 README 中的先决条件。 此应用程序使用 resnet18_2d_rgb_hmdb5_32.etlt 进行 2D 和 resnet18_3d_rgb_hmdb5_32.etlt 进行 3D 动作识别。</p></td>
</tr>
<tr class="row-even"><td><p>Analytics example</p></td>
<td><p>apps/sample_apps/deepstream-nvdsanalytics-test</p></td>
<td><p>演示批量分析，如 ROI 过滤、线交叉、方向检测和过度拥挤。 这个应用程序使用 resnet10.caffemodel 进行检测。</p></td>
</tr>
<tr class="row-odd"><td><p>OpenCV example</p></td>
<td><p>apps/sample_apps/deepstream-opencv-test</p></td>
<td><p>演示在 dsexample 插件中使用 OpenCV。 需要使用 WITH_OPENCV=1 标志编译 dsexample。 这个应用程序使用 resnet10.caffemodel 进行检测。</p></td>
</tr>
<tr class="row-even"><td><p>Image as Metadata example</p></td>
<td><p>Apps/sample_apps / deepstream-image-meta-test</p></td>
<td><p>演示如何将编码图像附加为元数据并将图像保存为 jpeg 格式。 这个应用程序使用 resnet10.caffemodel 进行检测。</p></td>
</tr>
<tr class="row-odd"><td><p>Appsrc and Appsink example</p></td>
<td><p>apps/sample_apps/deepstream-appsrc-test</p></td>
<td><p>演示 AppSrc 和 AppSink 分别用于使用和提供来自非 DeepStream 代码的数据。 这个应用程序使用 resnet10.caffemodel 进行检测。</p></td>
</tr>
<tr class="row-even"><td><p>Transfer learning example</p></td>
<td><p>apps/sample_apps/ deepstream-transfer-learning-app</p></td>
<td><p>演示了一种机制，可以为置信度较低的对象保存图像，并且可以将其用于进一步训练。 这个应用程序使用 resnet10.caffemodel 进行检测。</p></td>
</tr>
<tr class="row-odd"><td><p>Mask-RCNN example</p></td>
<td><p>apps/sample_apps/ deepstream-mrcnn-test</p></td>
<td><p>使用 Mask-RCNN 模型演示实例分割。 注意：由于 OpenCV 已弃用，此二进制文件未打包。 此应用程序需要由用户编译。</p></td>
</tr>
<tr class="row-even"><td><p>DeepStream Audio Reference Application</p></td>
<td><p>apps/sample_apps/deepstream-audio</p></td>
<td><p>演示音频分析流程的 DeepStream 参考应用程序的源代码。 这个应用程序使用 SONYC 音频模型对标签进行分类。</p></td>
</tr>
<tr class="row-odd"><td><p>Smart Record example</p></td>
<td><p>apps/sample_apps/deepstream-testsr</p></td>
<td><p>演示基于事件的智能记录功能。 这个应用程序使用 resnet10.caffemodel 进行检测。</p></td>
</tr>
<tr class="row-even"><td><p>Automatic Speech Recognition</p></td>
<td><p>apps/audio_apps/deepstream-asr-app</p></td>
<td><p>演示自动语音识别功能。 注意：此应用程序需要 Riva ASR 服务可用。 在运行应用程序之前，请参阅 README 中的先决条件。 此应用程序的默认模型是 Jasper，其他选项是 CitriNet 和 QuartzNet。</p></td>
</tr>
<tr class="row-odd"><td><p>Text To Speech Conversion (Alpha)</p></td>
<td><p>apps/audio_apps/deepstream-asr-tts-app</p></td>
<td><p>演示文本到语音的转换功能以及自动语音识别。 注意：此应用程序需要 Riva TTS 和 ASR 服务可用。 在运行应用程序之前，请参阅自述文件中的先决条件。 此应用程序使用 CitriNet 模型进行 ASR 和 FastPitch，HiFi-GAN 模型用于 TTS。</p></td>
</tr>
<tr class="row-even"><td><p>Audio+video+Text Synchronization (Alpha)</p></td>
<td><p>apps/sample_apps/deepstream-avsync-app</p></td>
<td><p>演示 DeepStream 流程中来自 nvdsasr 的音频、视频和文本输出的同步。 注意：此应用程序需要 Riva ASR 服务可用。 在运行应用程序之前，请参阅自述文件中的先决条件。 这个应用程序使用 Jasper 模型进行语音识别。</p></td>
</tr>
<tr class="row-odd"><td><p>DeepStream NMOS Application</p></td>
<td><p>apps/sample_apps/deepstream-nmos</p></td>
<td><p>此应用程序演示了如何将 DeepStream 应用程序创建为 <a class="reference external" href="https://specs.amwa.tv/nmos/">NMOS</a> 节点。 它使用一个库 (NvDsNmos)，该库提供 API 来创建、销毁和内部管理 NMOS 节点。 NMOS 节点可以使用 <a class="reference external" href="https://specs.amwa.tv/is-04/">AMWA IS-04</a> 注册 API 自动发现和注册网络上的 NMOS 注册。

它还展示了如何创建各种视频和音频流程，同时运行它们并根据 NMOS 事件（例如来自 NMOS 控制器的 <a class="reference external" href="https://specs.amwa.tv/is-05/">AMWA IS-05</a> 连接 API 请求）重新配置它们。</p>
</td>
</tr>
<tr class="row-even"><td><p>DeepStream UCX test 1</p></td>
<td><p>apps/sample_apps/deepstream-ucx-test1</p></td>
<td><p>演示如何使用通信插件 gst-nvdsucx 通过 RDMA 发送和接收视频数据，无需任何特殊元数据。</p></td>
</tr>
<tr class="row-odd"><td><p>DeepStream UCX test 2</p></td>
<td><p>apps/sample_apps/deepstream-ucx-test2</p></td>
<td><p>演示如何使用通信插件 gst-nvdsucx 通过 RDMA 发送和接收视频/元数据数据，以及通过 libnvds_video_metadata_serialization.so 库进行自定义序列化和反序列化。</p></td>
</tr>
<tr class="row-even"><td><p>DeepStream UCX test 3</p></td>
<td><p>apps/sample_apps/deepstream-ucx-test3</p></td>
<td><p>演示如何使用通信插件 gst-nvdsucx 通过 libnvds_audio_metadata_serialization.so 库使用自定义音频序列化和反序列化通过 RDMA 发送和接收音频/元数据数据。</p></td>
</tr>
<tr class="row-odd"><td><p>DeepStream 3D Depth Camera Reference App</p></td>
<td><p>apps/sample_apps/deepstream-3d-depth-camera</p></td>
<td><p>演示如何通过 DS3D 接口和 ds3d::dataloader、ds3d::datafilter 和 ds3d::datarender 的自定义库设置深度捕获、深度渲染、3D 点云处理和 3D 点渲染流程。 在 <a class="reference internal" href="DS_3D_Depth_Camera.html"><span class="doc">DeepStream 3D Depth Camera App</span></a>中查看更多详细信息</p></td>
</tr>
</tbody>
</table>
</div></blockquote>
<div class="admonition note">
注意
写入输出文件的应用程序（例如：deepstream-image-meta-test、deepstream-testsr、deepstream-transfer-learning-app）应在 sudo 权限下运行。
</div>
<div class="section" id="plugin-and-library-source-details">
<h2>组件和库细节<a class="headerlink" href="#plugin-and-library-source-details" title="Permalink to this headline">¶</a></h2>
<p>下表描述了除参考测试应用程序之外的源目录的内容：</p>
<blockquote>
<div><table class="colwidths-given docutils align-default" id="id3">
<caption><span class="caption-text">插件和库详细信息</span><a class="headerlink" href="#id3" title="Permalink to this table">¶</a></caption>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="row-odd"><th class="head"><p>插件或库</p></th>
<th class="head"><p>源目录中的路径</p></th>
<th class="head"><p>描述</p></th>
</tr>
</thead>
<tbody>
<tr class="row-even"><td><p>DsExample GStreamer plugin</p></td>
<td><p>gst-plugins/gst-dsexample</p></td>
<td><p>用于将自定义算法集成到 DeepStream SDK 图形中的模板插件。</p></td>
</tr>
<tr class="row-odd"><td><p>GStreamer Gst-nvmsgconv plugin</p></td>
<td><p>gst-plugins/gst-nvmsgconv</p></td>
<td><p>GStreamer Gst-nvmsgconv 插件的源代码，用于将元数据转换为模式格式。</p></td>
</tr>
<tr class="row-even"><td><p>GStreamer Gst-nvmsgbroker plugin</p></td>
<td><p>gst-plugins/gst-nvmsgbroker</p></td>
<td><p>GStreamer Gst-nvmsgbroker 插件的源代码，用于向服务器发送数据。</p></td>
</tr>
<tr class="row-odd"><td><p>GStreamer Gst-nvdspreprocess plugin</p></td>
<td><p>gst-plugins/gst-nvdspreprocess</p></td>
<td><p>GStreamer Gst-nvdspreprocess 插件的源代码，用于对预定义的 ROI 进行预处理。</p></td>
</tr>
<tr class="row-even"><td><p>GStreamer Gst-nvinfer plugin</p></td>
<td><p>gst-plugins/gst-nvinfer</p></td>
<td><p>用于推理的 GStreamer Gst-nvinfer 插件的源代码。</p></td>
</tr>
<tr class="row-odd"><td><p>GStreamer Gst-nvdsosd plugin</p></td>
<td><p>gst-plugins/gst-nvdsosd</p></td>
<td><p>GStreamer Gst-nvdsosd 插件的源代码，用于绘制 bbox、文本和其他对象。</p></td>
</tr>
<tr class="row-even"><td><p>NvDsInfer library</p></td>
<td><p>libs/nvdsinfer</p></td>
<td><p>NvDsInfer 库的源代码，由 Gst-nvinfer GStreamer 插件使用。</p></td>
</tr>
<tr class="row-odd"><td><p>NvDsNmos library</p></td>
<td><p>libs/nvdsnmos</p></td>
<td><p>NvDsNmos 库的源代码，由 DeepStream NMOS 应用程序演示。</p></td>
</tr>
<tr class="row-even"><td><p>NvMsgConv library</p></td>
<td><p>libs/nvmsgsconv</p></td>
<td><p>Gst-nvmsgconv GStreamer 插件所需的 NvMsgConv 库的源代码。</p></td>
</tr>
<tr class="row-odd"><td><p>Kafka protocol adapter</p></td>
<td><p>libs/kafka_protocol_adapter</p></td>
<td><p>Kafka 协议适配器。</p></td>
</tr>
<tr class="row-even"><td><p>nvdsinfer_customparser</p></td>
<td><p>libs/nvdsinfer_customparser</p></td>
<td><p>检测器和分类器的自定义模型输出解析示例。</p></td>
</tr>
<tr class="row-odd"><td><p>Gst-v4l2</p></td>
<td><p>See the note below <a class="footnote-reference brackets" href="#f1" id="id1">1</a></p></td>
<td><p>v4l2 编解码器的源代码。</p></td>
</tr>
<tr class="row-even"><td><p>Gstreamer gst-nvdsvideotemplate plugin</p></td>
<td><p>gst-plugins/gst-nvdsvideotemplate</p></td>
<td><p>用于实现视频自定义算法的模板插件源代码（非基于 Gstreamer）</p></td>
</tr>
<tr class="row-odd"><td><p>NvDsVideoTemplate custom library</p></td>
<td><p>gst-plugins/gst-nvdsvideotemplate/customlib_impl</p></td>
<td><p>自定义库源码实现视频自定义算法</p></td>
</tr>
<tr class="row-even"><td><p>Gstreamer gst-nvdsaudiotemplate plugin</p></td>
<td><p>gst-plugins/gst-nvdsaudiotemplate</p></td>
<td><p>模板插件 tp 的源代码实现音频自定义算法（非基于 Gstreamer）</p></td>
</tr>
<tr class="row-odd"><td><p>NvDsVideoTemplate custom library</p></td>
<td><p>gst-plugins/gst-nvdsaudiotemplate/customlib_impl</p></td>
<td><p>自定义库实现音频自定义算法的源代码</p></td>
</tr>
<tr class="row-even"><td><p>Gstreamer gst-nvdsmetautils</p></td>
<td><p>gst-plugins/gst-nvdsmetautils</p></td>
<td><p>Gstreamer Gst-nvdsmetainsert 和 Gst-nvdsmetaextract 插件处理元数据的源代码</p></td>
</tr>
<tr class="row-odd"><td><p>NvDsMetaUtils SEI serialization library</p></td>
<td><p>gst-plugins/gst-nvdsmetautils/sei_serialization</p></td>
<td><p>Gst-nvdsmetautils 插件所需的自定义元反序列化源代码以作为 SEI 数据嵌入到编码比特流中</p></td>
</tr>
<tr class="row-even"><td><p>NvDsMetaUtils Audio serialization library</p></td>
<td><p>gst-plugins/gst-nvdsmetautils/audio_metadata_serialization</p></td>
<td><p>音频 NvDsFrameMeta 反序列化的源代码，Gst-nvdsmetautils 插件需要</p></td>
</tr>
<tr class="row-odd"><td><p>NvDsMetaUtils Video serialization library</p></td>
<td><p>gst-plugins/gst-nvdsmetautils/video_metadata_serialization</p></td>
<td><p>Video NvDsFrameMeta &amp; 的源代码 Gst-nvdsmetautils 插件需要的 NvDsObjectMeta 反序列化/序列化</p></td>
</tr>
</tbody>
</table>
</div>





































































