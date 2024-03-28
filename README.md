新增一个相机，并更改相机角度  
dofbot.gazebo.urdf.xacro文件中第271行新增  
<xacro:include filename="$(find dofbot_description)/urdf/camera.xacro"/>  
camera新增后，初始相机角度不正确，如下图所示：  
![image](https://github.com/zybing1102/Dofbot-mimic/assets/72898091/eaf39cb7-d432-4328-ac04-cd1ea7bc3c2f)
相机增加后正常编写link&jiont，模型位置确认无误后，camera.xacro第40行更改角度数据(<pose>0 0 0 0 30 0</pose> )      
  
![image](https://github.com/zybing1102/Dofbot-mimic/assets/72898091/a6a39d65-dd9a-4a93-92cc-fecfc364ec6b)
更改轴位置后  
![image](https://github.com/zybing1102/Dofbot-mimic/assets/72898091/b7686bb2-af55-41bc-ad68-c9a6c2b3135d)
![image](https://github.com/zybing1102/Dofbot-mimic/assets/72898091/cad54d40-2497-4398-a1b8-4c0508f6a59c)

![image](https://github.com/zybing1102/Dofbot-mimic/assets/72898091/875561a6-5243-4b27-90be-d88fe59b64e1)



