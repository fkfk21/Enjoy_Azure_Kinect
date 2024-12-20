# Execution

```bash
cd ~/rogy_ws/azure_ws/src/Enjoy_Azure_Kinect_Viewer && docker compose up -d
bass source ~/rogy_ws/azure_ws/install/local_setup.bash
ros2 launch azure_kinect_ros_driver driver.launch.py depth_mode:=NFOV_UNBINNED color_resolution:=720P fps:=15 point_cloud:=false  rgb_point_cloud:=false
```

```bash
bass source ~/rogy_ws/azure_ws/install/local_setup.bash
ros2 run enjoy_azure_kinect image.launch.py
```

```bash
ros2 launch rosbridge_server rosbridge_websocket_launch.xml
```

```bash
bass source ~/rogy_ws/azure_ws/install/local_setup.bash
ros2 run microphone_processor sound.launch.sh
```



# Setup

## install azure kinect sdk

[reference](https://github.com/microsoft/Azure-Kinect-Sensor-SDK/issues/1263)

```
curl -sSL https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
# sudo apt-add-repository https://packages.microsoft.com/ubuntu/18.04/prod
curl -sSL https://packages.microsoft.com/config/ubuntu/18.04/prod.list | sudo tee /etc/apt/sources.list.d/microsoft-prod.list
curl -sSL https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
sudo apt-get update
# sudo apt install libk4a1.4-dev
# sudo apt install libk4abt1.1-dev
# sudo apt install k4a-tools=1.4.1
sudo apt install libk4a1.4-dev libk4abt1.1-dev k4a-tools=1.4.1
```
exec
```
sudo k4aviewer
```

## exec sample code
### Azure-Kinect-Samples
```
git clone git@github.com:microsoft/Azure-Kinect-Samples.git
sudo apt install libxi-dev
sudo apt install ninja-build
cd Azure-Kinect-Samples
mkdir build
cd build
cmake .. -GNinja
ninja
```
exec
```
sudo bin/simple_3d_viewer
```
[usage](https://github.com/microsoft/Azure-Kinect-Samples/tree/master/body-tracking-samples/simple_3d_viewer)

### SDK examples
```
git clone -b release/1.4.x git@github.com:microsoft/Azure-Kinect-Sensor-SDK.git
```
build examples

[examples](https://github.com/microsoft/Azure-Kinect-Sensor-SDK/tree/release/1.4.x/examples)


## access without root permission
[reference](https://github.com/microsoft/Azure-Kinect-Sensor-SDK/blob/develop/docs/usage.md#linux-device-setup)

```
curl -sSL https://raw.githubusercontent.com/microsoft/Azure-Kinect-Sensor-SDK/develop/scripts/99-k4a.rules | sudo tee /etc/udev/rules.d/99-k4a.rules > /dev/null
```
Deattach and attach



## clone repository
```
git clone -b foxy-devel git@github.com:microsoft/Azure_Kinect_ROS_Driver.git
```
## install dependencies
```
# rosdep install --from-paths src --ignore-src -r -y
```

## check microphone array


```
pacmd list-sources 

```
Azure Kinect Microphone Array
- sample spec: s32le 7ch 48000Hz
- channel map: front-left,front-right,rear-left,rear-right,front-center,lfe,aux0






## install hark

### deb package
[reference](https://hark.jp/install/linux/)


### install nodejs

install nodejs through n
```bash
sudo apt install nodejs npm
sudo npm install n -g
sudo n lts
sudo n 16
sudo apt purge nodejs npm
```

check version
```bash
npm -v
node -v
```


### install hark

[reference](https://hark.jp/install/linux/)
```bash
sudo curl -sSL http://archive.hark.jp/harkrepos/public.gpg -o /usr/share/keyrings/hark-archive-keyring.asc
sudo bash -c 'echo -e "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/hark-archive-keyring.asc] http://archive.hark.jp/harkrepos $(lsb_release -cs) non-free\ndeb-src [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/hark-archive-keyring.asc] http://archive.hark.jp/harkrepos $(lsb_release -cs) non-free" > /etc/apt/sources.list.d/hark.list'
```


```
sudo apt install hark-base harkmw hark-core hark-designer harktool5 harktool5-gui kaldidecoder-hark
```
-> version 3.4.0

```
sudo apt install hark-linux hark-gtkplot
```

### how to use hark designer
[slides](https://www.hark.jp/document/HARK_Guide_jp_HowToUse-HarkDesigner.pdf)


microphone array
```
arecord -l
```
```
** List of CAPTURE Hardware Devices **
card 1: C960 [HD Webcam eMeet C960], device 0: USB Audio [USB Audio]
  Subdevices: 1/1
  Subdevice #0: subdevice #0
card 2: Generic [HD-Audio Generic], device 0: ALC1220 Analog [ALC1220 Analog]
  Subdevices: 1/1
  Subdevice #0: subdevice #0
card 2: Generic [HD-Audio Generic], device 2: ALC1220 Alt Analog [ALC1220 Alt Analog]
  Subdevices: 1/1
  Subdevice #0: subdevice #0
card 3: Array [Azure Kinect Microphone Array], device 0: USB Audio [USB Audio]
  Subdevices: 1/1
  Subdevice #0: subdevice #0

```
-> manage device as "plughw:3,0"


### install hark-lib (PyHark)

[reference](https://hark.jp/packages/hark-acoustic-library-hark-lib/hark-lib-package-installation/)

source buildでinstall

[reference](https://hark.jp/packages/hark-acoustic-library-hark-lib/hark-lib-source-compilation-v1/)

```bash
cd Enjoy_Azure_Kinect
sudo apt install libhark-lib
apt source libhark-lib && rm libhark-lib-1.1.1.dsc libhark-lib-1.1.1.tar.xz  # libhark-lib-${HARK_VERSION} フォルダできる

# poetryに追加する場合
# poetry add ${PATH_TO_TMP}/libhark-lib-${HARK_VERSION}
# or
# pyproject.tomlに入っている場合
poetry install --no-root

poetry run pip install kivy_garden.graph --extra-index-url https://kivy-garden.github.io/simple/

```



### 
