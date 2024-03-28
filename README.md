环境：ubuntu20 ROS noetic  
mkdir arms  
mv src arms/  
rm arms/src/CMakelist.txt  
cd arms/src/  
catkin_init_workspace   
cd ..  
catkin_make  
source devel/setup.bash    
roslaunch dofbot_movit_config arm_bringup.launch  
rostopic pub -1 /as_arm/joint1_position_controller/command std_msgs/Float64 "data: -1.54"  
rostopic pub -1 /as_arm/gripper_position_controller/command std_msgs/Float64 "data: -1.54"  
joint1-5是控制5个轴旋转，gripper是控制夹具  

![image](https://github.com/zybing1102/Dofbot-mimic/assets/72898091/7c2ef90f-7dcf-466c-b9e3-87c16f93edac)
![image](https://github.com/zybing1102/Dofbot-mimic/assets/72898091/035807e0-dfc7-431b-ad6e-097759bb6cdb)
![image](https://github.com/zybing1102/Dofbot-mimic/assets/72898091/e5dd6fb8-786d-473e-84e2-134aa2100cc6)

文件目录介绍：  
dofbot_description:urdf xacro stl文件  
dofbot_movit_config:launch config配置文件  
roboticsgroup_gazebo_plugins-master：mimic库，来源：https://github.com/roboticsgroup/roboticsgroup_gazebo_plugins  
tutor：随动系统demo 来源：https://github.com/mintar/mimic_joint_gazebo_tutorial    
       需要安装rqt_joint_trajectory_controller插件  

mimic随动系统关键点：  
1.mimic插件库：arm_bringup.launch->gazebo.launch->dofbot.gazebo.urdf.xacro文件，dofbot.gazebo.urdf.xacro中调用mimicc插件库，写成一个宏  
![image](https://github.com/zybing1102/Dofbot-mimic/assets/72898091/9ee87043-c435-45ca-b20e-c70871a53e5e)
 
2.主动轮：在此example中，夹具分为左右两侧，每侧有三个零件，我使用右下角为主动轮(gripper_joint)，其余五个为从动轮(rlink_joint2,rlin_joint3,llink_joint1,llink_joint2,llink_joint3)  

![image](https://github.com/zybing1102/Dofbot-mimic/assets/72898091/93d0769d-4c10-4409-8bc5-7074ea9a99cb)

![image](https://github.com/zybing1102/Dofbot-mimic/assets/72898091/7af8a188-207b-4199-b52e-b08f60a3f128)
3.主动轮代码：  
![image](https://github.com/zybing1102/Dofbot-mimic/assets/72898091/398de645-d918-4488-88e2-7117a8847861)
473行<xacro:transmission_block joint_name="gripper_joint"/>使用宏形成硬件接口，通过effort_controllers/JointPositionController进行运动  

3.随动代码实现：  
![image](https://github.com/zybing1102/Dofbot-mimic/assets/72898091/694bc7e6-30eb-46f7-908a-66b70e59e072)
