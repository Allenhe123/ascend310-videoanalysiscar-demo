EN|[CN](README_cn.md)

# Vehicle Detection<a name="EN-US_TOPIC_0167573211"></a>

Developers can deploy the application on the Atlas 200 DK or the AI acceleration cloud server to decode the local MP4 file or RTSP video streams, detect vehicles in video frames, predict their attributes, generate structured information, and send the structured information to the server for storage and display.

## Prerequisites<a name="en-us_topic_0182554635_section137245294533"></a>

Before using an open source application, ensure that:

-   Mind Studio  has been installed.
-   The Atlas 200 DK developer board has been connected to  Mind Studio, the cross compiler has been installed, the SD card has been prepared, and basic information has been configured.

## Software Preparation<a name="en-us_topic_0182554635_section8534138124114"></a>

Before running the application, obtain the source code package and configure the environment as follows.

1.  Obtain the source code package.

    Download all the code in the sample-videoanalysiscar repository at  [https://gitee.com/Atlas200DK/sample-videoanalysiscar](https://gitee.com/Atlas200DK/sample-videoanalysiscar)  to any directory on Ubuntu Server where  Mind Studio  is located as the  Mind Studio  installation user, for example,  $HOME/sample-videoanalysiscar.

2.  <a name="en-us_topic_0182554635_li8221184418455"></a>Obtain the source network model required by the application.

    Obtain the source network model and its weight file used in the application by referring to  [Table 1](#en-us_topic_0182554635_table117203103464), and save them to any directory on the Ubuntu server where  Mind Studio  is located (for example,  **$HOME/ascend/models/videoanalysiscar**).

    **Table  1**  Models used in the vehicle detection application

    <a name="en-us_topic_0182554635_table117203103464"></a>
    <table><thead align="left"><tr id="en-us_topic_0182554635_row4859191074617"><th class="cellrowborder" valign="top" width="17.32173217321732%" id="mcps1.2.4.1.1"><p id="en-us_topic_0182554635_p18859111074613"><a name="en-us_topic_0182554635_p18859111074613"></a><a name="en-us_topic_0182554635_p18859111074613"></a>Model Name</p>
    </th>
    <th class="cellrowborder" valign="top" width="9.68096809680968%" id="mcps1.2.4.1.2"><p id="en-us_topic_0182554635_p17859171013469"><a name="en-us_topic_0182554635_p17859171013469"></a><a name="en-us_topic_0182554635_p17859171013469"></a>Model Description</p>
    </th>
    <th class="cellrowborder" valign="top" width="72.997299729973%" id="mcps1.2.4.1.3"><p id="en-us_topic_0182554635_p1385991094614"><a name="en-us_topic_0182554635_p1385991094614"></a><a name="en-us_topic_0182554635_p1385991094614"></a>Model Download Path</p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="en-us_topic_0182554635_row1085921012469"><td class="cellrowborder" valign="top" width="17.32173217321732%" headers="mcps1.2.4.1.1 "><p id="en-us_topic_0182554635_p168591710184613"><a name="en-us_topic_0182554635_p168591710184613"></a><a name="en-us_topic_0182554635_p168591710184613"></a>car_color</p>
    </td>
    <td class="cellrowborder" valign="top" width="9.68096809680968%" headers="mcps1.2.4.1.2 "><p id="en-us_topic_0182554635_p118591410204619"><a name="en-us_topic_0182554635_p118591410204619"></a><a name="en-us_topic_0182554635_p118591410204619"></a>Network model for identifying the vehicle color.</p>
    </td>
    <td class="cellrowborder" valign="top" width="72.997299729973%" headers="mcps1.2.4.1.3 "><p id="en-us_topic_0182554635_p11859310174613"><a name="en-us_topic_0182554635_p11859310174613"></a><a name="en-us_topic_0182554635_p11859310174613"></a>Download the source network model file and its weight file by referring to<strong id="en-us_topic_0182554635_b204745114127"><a name="en-us_topic_0182554635_b204745114127"></a><a name="en-us_topic_0182554635_b204745114127"></a> README.md</strong> in <a href="https://gitee.com/HuaweiAscend/models/tree/master/computer_vision/classification/car_color" target="_blank" rel="noopener noreferrer">https://gitee.com/HuaweiAscend/models/tree/master/computer_vision/classification/car_color</a>.</p>
    </td>
    </tr>
    <tr id="en-us_topic_0182554635_row78596105463"><td class="cellrowborder" valign="top" width="17.32173217321732%" headers="mcps1.2.4.1.1 "><p id="en-us_topic_0182554635_p118591910104615"><a name="en-us_topic_0182554635_p118591910104615"></a><a name="en-us_topic_0182554635_p118591910104615"></a>car_type</p>
    </td>
    <td class="cellrowborder" valign="top" width="9.68096809680968%" headers="mcps1.2.4.1.2 "><p id="en-us_topic_0182554635_p1685991044614"><a name="en-us_topic_0182554635_p1685991044614"></a><a name="en-us_topic_0182554635_p1685991044614"></a>Network model for identifying the vehicle brand.</p>
    <p id="en-us_topic_0182554635_p13859410184613"><a name="en-us_topic_0182554635_p13859410184613"></a><a name="en-us_topic_0182554635_p13859410184613"></a>It is a GoogLeNet model based on Caffe.</p>
    </td>
    <td class="cellrowborder" valign="top" width="72.997299729973%" headers="mcps1.2.4.1.3 "><p id="en-us_topic_0182554635_p1985915105461"><a name="en-us_topic_0182554635_p1985915105461"></a><a name="en-us_topic_0182554635_p1985915105461"></a>Download the source network model file and its weight file by referring to<strong id="en-us_topic_0182554635_b135035181216"><a name="en-us_topic_0182554635_b135035181216"></a><a name="en-us_topic_0182554635_b135035181216"></a> README.md</strong> in <a href="https://gitee.com/HuaweiAscend/models/tree/master/computer_vision/classification/car_type" target="_blank" rel="noopener noreferrer">https://gitee.com/HuaweiAscend/models/tree/master/computer_vision/classification/car_type</a>.</p>
    </td>
    </tr>
    <tr id="en-us_topic_0182554635_row1985913103461"><td class="cellrowborder" valign="top" width="17.32173217321732%" headers="mcps1.2.4.1.1 "><p id="en-us_topic_0182554635_p14859151016464"><a name="en-us_topic_0182554635_p14859151016464"></a><a name="en-us_topic_0182554635_p14859151016464"></a>car_plate_detection</p>
    </td>
    <td class="cellrowborder" valign="top" width="9.68096809680968%" headers="mcps1.2.4.1.2 "><p id="en-us_topic_0182554635_p108593100461"><a name="en-us_topic_0182554635_p108593100461"></a><a name="en-us_topic_0182554635_p108593100461"></a>Network model for identifying the license plate.</p>
    <p id="en-us_topic_0182554635_p1785921024614"><a name="en-us_topic_0182554635_p1785921024614"></a><a name="en-us_topic_0182554635_p1785921024614"></a>It is a MobileNet-SSD model based on Caffe.</p>
    </td>
    <td class="cellrowborder" valign="top" width="72.997299729973%" headers="mcps1.2.4.1.3 "><p id="en-us_topic_0182554635_p158596106460"><a name="en-us_topic_0182554635_p158596106460"></a><a name="en-us_topic_0182554635_p158596106460"></a>Download the source network model file and its weight file by referring to<strong id="en-us_topic_0182554635_b65410511129"><a name="en-us_topic_0182554635_b65410511129"></a><a name="en-us_topic_0182554635_b65410511129"></a> README.md</strong> in <a href="hhttps://gitee.com/HuaweiAscend/models/tree/master/computer_vision/object_detect/car_plate_detection" target="_blank" rel="noopener noreferrer">https://gitee.com/HuaweiAscend/models/tree/master/computer_vision/object_detect/car_plate_detection</a>.</p>
    </td>
    </tr>
    <tr id="en-us_topic_0182554635_row08596101464"><td class="cellrowborder" valign="top" width="17.32173217321732%" headers="mcps1.2.4.1.1 "><p id="en-us_topic_0182554635_p178591510164619"><a name="en-us_topic_0182554635_p178591510164619"></a><a name="en-us_topic_0182554635_p178591510164619"></a>car_plate_recognition</p>
    </td>
    <td class="cellrowborder" valign="top" width="9.68096809680968%" headers="mcps1.2.4.1.2 "><p id="en-us_topic_0182554635_p1485911105469"><a name="en-us_topic_0182554635_p1485911105469"></a><a name="en-us_topic_0182554635_p1485911105469"></a>Network model for identifying the license plate number.</p>
    <p id="en-us_topic_0182554635_p17859191018468"><a name="en-us_topic_0182554635_p17859191018468"></a><a name="en-us_topic_0182554635_p17859191018468"></a>It is a CNN model based on Caffe.</p>
    </td>
    <td class="cellrowborder" valign="top" width="72.997299729973%" headers="mcps1.2.4.1.3 "><p id="en-us_topic_0182554635_p7859181094619"><a name="en-us_topic_0182554635_p7859181094619"></a><a name="en-us_topic_0182554635_p7859181094619"></a>Download the source network model file and its weight file by referring to<strong id="en-us_topic_0182554635_b1955185112127"><a name="en-us_topic_0182554635_b1955185112127"></a><a name="en-us_topic_0182554635_b1955185112127"></a> README.md</strong> in <a href="https://gitee.com/HuaweiAscend/models/tree/master/computer_vision/classification/car_plate_recognition" target="_blank" rel="noopener noreferrer">https://gitee.com/HuaweiAscend/models/tree/master/computer_vision/classification/car_plate_recognition</a>.</p>
    </td>
    </tr>
    <tr id="en-us_topic_0182554635_row88591310124617"><td class="cellrowborder" valign="top" width="17.32173217321732%" headers="mcps1.2.4.1.1 "><p id="en-us_topic_0182554635_p685911013465"><a name="en-us_topic_0182554635_p685911013465"></a><a name="en-us_topic_0182554635_p685911013465"></a>vgg_ssd</p>
    </td>
    <td class="cellrowborder" valign="top" width="9.68096809680968%" headers="mcps1.2.4.1.2 "><p id="en-us_topic_0182554635_p1786011016461"><a name="en-us_topic_0182554635_p1786011016461"></a><a name="en-us_topic_0182554635_p1786011016461"></a>Network model for object detection.</p>
    <p id="en-us_topic_0182554635_p086018109465"><a name="en-us_topic_0182554635_p086018109465"></a><a name="en-us_topic_0182554635_p086018109465"></a>It is an SSD512 model based on Caffe.</p>
    </td>
    <td class="cellrowborder" valign="top" width="72.997299729973%" headers="mcps1.2.4.1.3 "><p id="en-us_topic_0182554635_p1186071044613"><a name="en-us_topic_0182554635_p1186071044613"></a><a name="en-us_topic_0182554635_p1186071044613"></a>Download the source network model file and its weight file by referring to<strong id="en-us_topic_0182554635_b1856165117121"><a name="en-us_topic_0182554635_b1856165117121"></a><a name="en-us_topic_0182554635_b1856165117121"></a> README.md</strong> in <a href="https://gitee.com/HuaweiAscend/models/tree/master/computer_vision/object_detect/vgg_ssd" target="_blank" rel="noopener noreferrer">https://gitee.com/HuaweiAscend/models/tree/master/computer_vision/object_detect/vgg_ssd</a>.</p>
    </td>
    </tr>
    </tbody>
    </table>

3.  Convert the source network model to a Da Vinci model.
    1.  Choose  **Tool \> Convert Model**  from the main menu of  Mind Studio. The  **Convert Model**  page is displayed.
    2.  On the  **Convert Model**  page, set  **Model File**  and  **Weight File** to the model file and weight file downloaded in  [2](#en-us_topic_0182554635_li8221184418455), respectively.

        -   Set  **Model Name**  to the model name in  [Table 1](#en-us_topic_0182554635_table117203103464).
        -   For the  **car\_color**  model,  **car\_color\_inference** processes 10 images at a time. Therefore,  **N**  of  **Input Shape** must be set to  **10**  during conversion.

            For the  **car\_type**  model,  **car\_type\_inference** processes 10 images at a time. Therefore,  **N**  of  **Input Shape** must be set to  **10**  during conversion.

        -   Retain default values for other parameters.

        **Figure  1**  Input Shape configuration reference<a name="en-us_topic_0182554635_fig09711548135116"></a>  
        ![](doc/source/img/input-shape-configuration-reference.png "input-shape-configuration-reference")

    3.  Click  **OK**  to start model conversion.

        During the conversion of the  **car\_plate\_detection**  and **vgg\_ssd**  models, the following error will be reported.

        **Figure  2**  Model conversion error<a name="en-us_topic_0182554635_fig1842765585311"></a>  
        ![](doc/source/img/model-conversion-error.jpg "model-conversion-error")

        Select  **SSDDetectionOutput**  from the  **Suggestion**  drop-down list box at the  **DetectionOutput**  layer and click  **Retry**.

        After successful conversion, a .om Da Vinci model is generated in the  **$HOME/tools/che/model-zoo/my-model/xxx**  directory.

4.  Upload the converted .om model file to the  **sample-videoanalysiscar/script** directory
5.  Log in to Ubuntu Server where  Mind Studio  is located as the  Mind Studio  installation user and set the environment variable  **DDK\_HOME**.

    **vim \~/.bashrc**

    Run the following commands to add the environment variables  **DDK\_HOME**  and  **LD\_LIBRARY\_PATH**  to the last line:

    **export DDK\_HOME=$HOME/tools/che/ddk/ddk**

    **export LD\_LIBRARY\_PATH=$DDK\_HOME/uihost/lib**

    >![](public_sys-resources/icon-note.gif) **NOTE:**   
    >-   If the environment variables have been added, skip this step.  

    Enter  **:wq!**  to save and exit.

    Run the following command for the environment variable to take effect:

    **source \~/.bashrc**


## Deployment<a name="en-us_topic_0182554635_section1759513564117"></a>

1.  Access the root directory where the vehicle detection application code is located as the  Mind Studio  installation user, for example,  **$HOME/sample-videoanalysiscar**.
2.  <a name="en-us_topic_0182554635_li08019112542"></a>Run the deployment script to prepare the project environment, including compiling and deploying the ascenddk public library and configuring Presenter Server. The Presenter Server is used to receive the data sent by the application and display the result through the browser.

    **bash deploy.sh** _host\_ip_ _model\_mode_

    -   _host\_ip_: For the Atlas 200 DK developer board, this parameter indicates the IP address of the developer board. For the AI acceleration cloud server, this parameter indicates the IP address of the host.

    -   _model\_mode_  indicates the deployment mode of the model file. The value can be  **local**  or  **internet**. The default setting is  **internet**.
        -   **local**: If the Ubuntu system where  Mind Studio  is located is not connected to the network, use the local mode. In this case, you need to have downloaded the dependent common code library to the  **sample-videoanalysiscar/script**  directory by referring to  [Downloading Dependent Code Library](#en-us_topic_0182554635_section13807155164319).
        -   **internet**: If the Ubuntu system where  Mind Studio  is located is connected to the network, use the Internet mode. In this case, download dependent code library online.


    Example command:

    **bash deploy.sh 192.168.1.2 internet**

    -   When the message  **Please choose one to show the presenter in browser\(default: 127.0.0.1\):**  is displayed, enter the IP address used for accessing the Presenter Server service in the browser. Generally, the IP address is the IP address for accessing the  Mind Studio  service.
    -   When the message  **Please input an absolute path to storage video analysis data:**  is displayed, enter the absolute path for storing video analysis data in  Mind Studio. The  Mind Studio  user must have the read and write permissions. If the path does not exist, the script is automatically created.

    Select the IP address used by the browser to access the Presenter Server service in  **Current environment valid ip list**  and enter the path for storing video analysis data, as shown in  [Figure 3](#en-us_topic_0182554635_fig184321447181017).

    **Figure  3**  Project deployment<a name="en-us_topic_0182554635_fig184321447181017"></a>  
    ![](doc/source/img/project-deployment.png "project-deployment")

3.  <a name="en-us_topic_0182554635_li499911453439"></a>Start Presenter Server.

    Run the following command to start the Presenter Server program of the video analysis application in the background:

    **python3 presenterserver/presenter\_server.py --app video\_analysis\_car &**

    >![](public_sys-resources/icon-note.gif) **NOTE:**   
    >**presenter\_server.py**  is located in the  **presenterserver**  directory. You can run the  **python3 presenter\_server.py -h**  or  **python3 presenter\_server.py --help**  command in this directory to view the usage method of  **presenter\_server.py**.  

    [Figure 4](#en-us_topic_0182554635_fig69531305324)  shows that the presenter\_server service is started successfully.

    **Figure  4**  Starting the Presenter Server process<a name="en-us_topic_0182554635_fig69531305324"></a>  
    ![](doc/source/img/starting-the-presenter-server-process.png "starting-the-presenter-server-process")

    Use the URL shown in the preceding figure to log in to Presenter Server \(only the Chrome browser is supported\). The IP address is that entered in  [2](#en-us_topic_0182554635_li08019112542)  and the default port number is  **7005**. The following figure indicates that Presenter Server is started successfully.

    **Figure  5**  Home page<a name="en-us_topic_0182554635_fig64391558352"></a>  
    ![](doc/source/img/home-page.png "home-page")

    The following figure shows the IP address used by the Presenter Server and  Mind Studio  to communicate with the Atlas 200 DK.

    **Figure  6**  Example IP Address<a name="en-us_topic_0182554635_fig1881532172010"></a>  
    ![](doc/source/img/example-ip-address.png "example-ip-address")

    Where:

    -   The IP address of the Atlas 200 DK developer board is 192.168.1.2 \(connected in USB mode\).
    -   The IP address used by the Presenter Server to communicate with the Atlas 200 DK is in the same network segment as the IP address of the Atlas 200 DK on the UI Host server. For example: 192.168.1.223.
    -   The following is an example of accessing the IP address of the Presenter Server using a browser: 10.10.0.1, because the Presenter Server and  Mind Studio  are deployed on the same server, the IP address is also the IP address for accessing the  Mind Studio  through the browser.

4.  The video structured application can parse local videos and RTSP video streams.
    -   To parse a local video, upload the video file to the Host.

        For example, upload the video file  **car.mp4**  to the  **/home/HwHiAiUser/sample**  directory on the host.

        >![](public_sys-resources/icon-note.gif) **NOTE:**   
        >H.264 and H.265 MP4 files are supported. If an MP4 file needs to be edited, you are advised to use FFmpeg. If a video file is edited by other tools, FFmpeg may fail to parse the file.  

    -   If only RTSP video streams need to be parsed, skip this step.


## Running<a name="en-us_topic_0182554635_section6245151616426"></a>

1.  Run the video analysis application.

    Run the following command in the  **$HOME/sample-videoanalysiscar**  directory to start the video analysis application:

    **bash run\_videoanalysiscarapp.sh** _host\_ip_ _presenter\_view\_appname_ _channel1_ _[channel2]_  &

    -   _host\_ip_: For the Atlas 200 DK developer board, this parameter indicates the IP address of the developer board. For the AI acceleration cloud server, this parameter indicates the IP address of the host.
    -   _presenter\_view\_app\_name_: Indicates  **View Name**  displayed on the Presenter Server page, which is user-defined. The value of this parameter must be unique on the Presenter Server page, which contains only case-senstive leters, digits, and underscores(_). The number of characters should be 3-20.
    -   _channel1_: absolute path of a video file on the host, need to add double quotes when there is only a video file. Channel2 can be omitted
    -   _channel2_: URL of an RTSP video stream. need to add double quotes, when there is only RTSP video stream, you need to use " " to occupy channel1

    Example command of video file:

    **bash run\_videoanalysiscarapp.sh 192.168.1.2 video "/home/HwHiAiUser/sample/car.mp4" &**

    Example command of RTSP video stream:

    **bash run\_videoanalysiscarapp.sh 192.168.1.2 video " " "rtsp://192.168.2.37:554/cam/realmonitor?channel=1&subtype=0" &**

    >![](public_sys-resources/icon-note.gif) **NOTE:**  
    >The current RTSP video stream only supports the rtsp://ip:port/path format. If you need to use other format urls, you need to remove the IsValidRtsp function in video_decode.cpp, or return true directly, skipping the regular expression matching.

2.  Use the URL that is displayed when you start the Presenter Server service to log in to the Presenter Server website (only the Chrome browser is supported). For details, see  [3](#en-us_topic_0182554635_li499911453439).

    >![](public_sys-resources/icon-note.gif) **NOTE:**   
    >The Presenter Server of the video analysis application supports the display of a maximum of two  _presenter\_view\_app\_name_  at the same time.  

    The navigation tree on the left displays the app name and channel name of the video. The large image of the extracted video frame and the detected target small image are displayed in the middle. After you click the small image, the detailed inference result and score are displayed on the right.

    Vehicle attribute detection supports the identification of vehicle brands, vehicle colors, and license plates.

    >![](public_sys-resources/icon-note.gif) **NOTE:**   
    >In the network model of license plate recognition, the license plate images automatically generated by the program are trained as the training set, instead of using real license plate images. Therefore, this model has low accuracy in identifying real license plate numbers. If a high-accuracy model is required, collect real license plate images as the training set and train them.  


## Follow-up Operations<a name="en-us_topic_0182554635_section1092612277429"></a>

-   **Stopping the Video Structured Analysis Application**

    To stop the video analysis application, perform the following operations:

    Run the following command in the  **sample-videoanalysiscar**  directory as the  Mind Studio  installation user:

    **bash stop\_videoanalysiscarapp.sh** _host\_ip_

    _host\_ip_: For the Atlas 200 DK developer board, this parameter indicates the IP address of the developer board. For the AI acceleration cloud server, this parameter indicates the IP address of the host.

    Example command:

    **bash stop\_videoanalysiscarapp.sh** _192.168.1.2_

-   **Stopping the Presenter Server Service**

    The Presenter Server service is always in the running state after being started. To stop the Presenter Server service of the video structured analysis application, perform the following operations:

    Run the following command to check the process of the Presenter Server service corresponding to the video structured analysis application as the  Mind Studio  installation user:

    **ps -ef | grep presenter | grep video\_analysis\_car**

    ```
    ascend@ascend-HP-ProDesk-600-G4-PCI-MT:~/sample-videoanalysiscar$ ps -ef | grep presenter | grep video_analysis_car 
    ascend 3655 20313 0 15:10 pts/24?? 00:00:00 python3 presenterserver/presenter_server.py --app video_analysis_car
    ```

    In the preceding information,  _3655_  indicates the process ID of the Presenter Server service corresponding to the facial recognition application.

    To stop the service, run the following command:

    **kill -9** _3655_


## Downloading Dependent Code Library<a name="en-us_topic_0182554635_section13807155164319"></a>

Download the dependent software libraries to the  **sample-videoanalysiscar/script**  directory.

**Table  2**  Download the dependent software library

<a name="en-us_topic_0182554635_table6332142412"></a>
<table><thead align="left"><tr id="en-us_topic_0182554635_row203322042016"><th class="cellrowborder" valign="top" width="33.33333333333333%" id="mcps1.2.4.1.1"><p id="en-us_topic_0182554635_p73321742118"><a name="en-us_topic_0182554635_p73321742118"></a><a name="en-us_topic_0182554635_p73321742118"></a>Module Name</p>
</th>
<th class="cellrowborder" valign="top" width="33.33333333333333%" id="mcps1.2.4.1.2"><p id="en-us_topic_0182554635_p83324426119"><a name="en-us_topic_0182554635_p83324426119"></a><a name="en-us_topic_0182554635_p83324426119"></a>Module Description</p>
</th>
<th class="cellrowborder" valign="top" width="33.33333333333333%" id="mcps1.2.4.1.3"><p id="en-us_topic_0182554635_p203321342311"><a name="en-us_topic_0182554635_p203321342311"></a><a name="en-us_topic_0182554635_p203321342311"></a>Download Address</p>
</th>
</tr>
</thead>
<tbody><tr id="en-us_topic_0182554635_row1633213424119"><td class="cellrowborder" valign="top" width="33.33333333333333%" headers="mcps1.2.4.1.1 "><p id="en-us_topic_0182554635_p633219421011"><a name="en-us_topic_0182554635_p633219421011"></a><a name="en-us_topic_0182554635_p633219421011"></a>EZDVPP</p>
</td>
<td class="cellrowborder" valign="top" width="33.33333333333333%" headers="mcps1.2.4.1.2 "><p id="en-us_topic_0182554635_p12332542618"><a name="en-us_topic_0182554635_p12332542618"></a><a name="en-us_topic_0182554635_p12332542618"></a>Encapsulates the DVPP interface and provides image and video processing capabilities, such as color gamut conversion and image / video conversion</p>
</td>
<td class="cellrowborder" valign="top" width="33.33333333333333%" headers="mcps1.2.4.1.3 "><p id="en-us_topic_0182554635_p8332124216110"><a name="en-us_topic_0182554635_p8332124216110"></a><a name="en-us_topic_0182554635_p8332124216110"></a><a href="https://gitee.com/Atlas200DK/sdk-ezdvpp" target="_blank" rel="noopener noreferrer">https://gitee.com/Atlas200DK/sdk-ezdvpp</a></p>
<p id="en-us_topic_0182554635_p53321742918"><a name="en-us_topic_0182554635_p53321742918"></a><a name="en-us_topic_0182554635_p53321742918"></a>After the download, keep the folder name <span class="filepath" id="en-us_topic_0182554635_filepath1333174215117"><a name="en-us_topic_0182554635_filepath1333174215117"></a><a name="en-us_topic_0182554635_filepath1333174215117"></a><b>ezdvpp</b></span>.</p>
</td>
</tr>
<tr id="en-us_topic_0182554635_row193336423119"><td class="cellrowborder" valign="top" width="33.33333333333333%" headers="mcps1.2.4.1.1 "><p id="en-us_topic_0182554635_p933374214117"><a name="en-us_topic_0182554635_p933374214117"></a><a name="en-us_topic_0182554635_p933374214117"></a>Presenter Agent</p>
</td>
<td class="cellrowborder" valign="top" width="33.33333333333333%" headers="mcps1.2.4.1.2 "><p id="en-us_topic_0182554635_p433318421415"><a name="en-us_topic_0182554635_p433318421415"></a><a name="en-us_topic_0182554635_p433318421415"></a><span>API for interacting with the Presenter Server</span>.</p>
</td>
<td class="cellrowborder" valign="top" width="33.33333333333333%" headers="mcps1.2.4.1.3 "><p id="en-us_topic_0182554635_p163331342914"><a name="en-us_topic_0182554635_p163331342914"></a><a name="en-us_topic_0182554635_p163331342914"></a><a href="https://gitee.com/Atlas200DK/sdk-presenter/tree/master" target="_blank" rel="noopener noreferrer">https://gitee.com/Atlas200DK/sdk-presenter/tree/master</a></p>
<p id="en-us_topic_0182554635_p16333124217112"><a name="en-us_topic_0182554635_p16333124217112"></a><a name="en-us_topic_0182554635_p16333124217112"></a>Obtain the presenteragent folder in this path, after the download, keep the folder name <span class="filepath" id="en-us_topic_0182554635_filepath143335423119"><a name="en-us_topic_0182554635_filepath143335423119"></a><a name="en-us_topic_0182554635_filepath143335423119"></a><b>presenteragent</b></span>.</p>
</td>
</tr>
<tr id="en-us_topic_0182554635_row733316421318"><td class="cellrowborder" valign="top" width="33.33333333333333%" headers="mcps1.2.4.1.1 "><p id="en-us_topic_0182554635_p133311421019"><a name="en-us_topic_0182554635_p133311421019"></a><a name="en-us_topic_0182554635_p133311421019"></a>FFmpeg code</p>
</td>
<td class="cellrowborder" valign="top" width="33.33333333333333%" headers="mcps1.2.4.1.2 "><p id="en-us_topic_0182554635_p13333042818"><a name="en-us_topic_0182554635_p13333042818"></a><a name="en-us_topic_0182554635_p13333042818"></a>The current application uses FFmpeg to decapsulate video files.</p>
</td>
<td class="cellrowborder" valign="top" width="33.33333333333333%" headers="mcps1.2.4.1.3 "><p id="en-us_topic_0182554635_p1233354214115"><a name="en-us_topic_0182554635_p1233354214115"></a><a name="en-us_topic_0182554635_p1233354214115"></a>The URL for downloading the FFmpeg 4.0 code is <a href="https://gitee.com/mirrors/ffmpeg/tree/release%2F4.0/" target="_blank" rel="noopener noreferrer">https://gitee.com/mirrors/ffmpeg/tree/release%2F4.0/</a>.</p>
<p id="en-us_topic_0182554635_p20333134213110"><a name="en-us_topic_0182554635_p20333134213110"></a><a name="en-us_topic_0182554635_p20333134213110"></a>After the download, keep the folder name <span class="filepath" id="en-us_topic_0182554635_filepath03332042716"><a name="en-us_topic_0182554635_filepath03332042716"></a><a name="en-us_topic_0182554635_filepath03332042716"></a><b>ffmpeg.</b></span></p>
</td>
</tr>
<tr id="en-us_topic_0182554635_row3333242119"><td class="cellrowborder" valign="top" width="33.33333333333333%" headers="mcps1.2.4.1.1 "><p id="en-us_topic_0182554635_p1333194212116"><a name="en-us_topic_0182554635_p1333194212116"></a><a name="en-us_topic_0182554635_p1333194212116"></a>tornado (5.1.0)</p>
<p id="en-us_topic_0182554635_p133336427112"><a name="en-us_topic_0182554635_p133336427112"></a><a name="en-us_topic_0182554635_p133336427112"></a>protobuf (3.5.1)</p>
<p id="en-us_topic_0182554635_p433304218118"><a name="en-us_topic_0182554635_p433304218118"></a><a name="en-us_topic_0182554635_p433304218118"></a>numpy (1.14.2)</p>
</td>
<td class="cellrowborder" valign="top" width="33.33333333333333%" headers="mcps1.2.4.1.2 "><p id="en-us_topic_0182554635_p16333154218110"><a name="en-us_topic_0182554635_p16333154218110"></a><a name="en-us_topic_0182554635_p16333154218110"></a>Python libraries that Presenter Server depends on.</p>
</td>
<td class="cellrowborder" valign="top" width="33.33333333333333%" headers="mcps1.2.4.1.3 "><p id="en-us_topic_0182554635_p43332042717"><a name="en-us_topic_0182554635_p43332042717"></a><a name="en-us_topic_0182554635_p43332042717"></a>You can search for related packages on the Python official website <a href="https://pypi.org/" target="_blank" rel="noopener noreferrer">https://pypi.org/</a> for installation. If you run the pip3 install command to download the file online, you can run the following command to specify the version to be downloaded: <strong id="en-us_topic_0182554635_b1033313422111"><a name="en-us_topic_0182554635_b1033313422111"></a><a name="en-us_topic_0182554635_b1033313422111"></a>pip3 install tornado==5.1.0 -i <em id="en-us_topic_0182554635_i1433312422116"><a name="en-us_topic_0182554635_i1433312422116"></a><a name="en-us_topic_0182554635_i1433312422116"></a>Installation source of the specified library</em> --trusted-host <em id="en-us_topic_0182554635_i9333144213116"><a name="en-us_topic_0182554635_i9333144213116"></a><a name="en-us_topic_0182554635_i9333144213116"></a>Host name of the installation sourc</em>e</strong></p>
</td>
</tr>
</tbody>
</table>

