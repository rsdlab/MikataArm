# 概要
mikata-armのROSパッケージ
既存のmikata-armの6軸のパッケージ[Mikata-arm Ros パッケージ](https://github.com/ROBOTIS-JAPAN-GIT/open_manipulator/tree/dynamixel_6dof_mikata_arm)は
Gazebo+Moveit!は可能だが、moveit_commanderを用いたプログラムを用いるとうまく動作しないことがわかった

よって、ここのリポジトリを用いることで、シミュレーションでも実機環境でも動作可能にできるようにパッケージを変更した

簡易的ではあるが、サンプルコードも入っているので実際に試してみると動作確認できると思われる

# インストール方法
上記のMikata-arm Ros パッケージを参考にすればよいが、下記までgit clone すること
 ```shell
    $ git clone https://github.com/ROBOTIS-GIT/DynamixelSDK.git
    $ git clone https://github.com/ROBOTIS-GIT/dynamixel-workbench.git
    $ git clone https://github.com/ROBOTIS-GIT/dynamixel-workbench-msgs.git
    $ git clone https://github.com/ROBOTIS-GIT/robotis_manipulator.git
    $ git clone https://github.com/ROBOTIS-GIT/open_manipulator_msgs.git
```


```shell
    $ cd ~/catkin_ws/src
    $ git clone https://github.com/ｒｓｄlab/DYNAMIXEL-MikataArm-
    $ cd ..
    $ catkin build
```
 
これで環境構築は完了する．

# 動作方法

基本的にはOpen_manipulatorと同じなので。e-Manualを参考にするように[e-Manual](https://emanual.robotis.com/docs/en/platform/openmanipulator_x/quick_start_guide/)

これはシミュレーション環境で行う場合のコマンドである
 ``` shell
   $ roslaunch open_manipulator_controller open_manipulator_controller.launch use_gazebo:=true use_moveit:=true
 ```
 
 これは、実機環境で行う場合のコマンドである
  ``` shell
   $ sudo chmod 666 /dev/ttyUSB0
   $ roslaunch open_manipulator_controller open_manipulator_controller.launch use_moveit:=true
 ```
 
 USBの実行権限に関してのPathは適宜変更すること
 
 サンプルコードを動かすと、簡単なPick and Place動作を行う（グリッパー部分は、現状サービスで実装してあるが、本当はplanning nameのところにgripperを用いて、gripper controllerを使って開閉を行うのが普通なはず...?）
シミュレーション環境や実機環境どちらで動かしてもよいので、下記のコマンドで動作確認を行うとよい

 ```shell
   $ rosrun open_manipulator_moveit open_manipulator.py
 ```
