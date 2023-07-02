### create workspace

- source ros2 binary first if ros2 command not found:
```
source /opt/ros/humble/setup.bash
```
- create workspace and src/ inside
```
mkdir -p ros2_ws/src
cd ros2_ws/src
```

- install dependencies if needed, change distro to yours
```
rosdep install -i --from-path src --rosdistro humble -y
```
### create package

- cd into ros2_ws/src/ and create package
```
ros2 pkg create --build-type ament_python package_name --dependencies rclpy example_interfaces
```
### edit package
- update package.xml and setup.py if needed
- write node inside ros2_ws/src/package_name/package_name/mynode_member_function.py
- Add new dependencies as tags e.g. `<exec_depend>rclpy</exec_depend>` after license tag inside package.xml
- add entry point to `console_scripts` list in setup.py:
```
'service = package_name.mynode_member_function:main',
```

### build package

- install dependencies inside root of ros2_ws/:

```
rosdep install -i --from-path src --rosdistro humble -y
```

- build package with colcon

```
colcon build --packages-select package_name
```

### run nodes 

- in new terminal, source inside ros2_ws/:

```
  source install/setup.bash
```
- run each node with

```
ros2 run package_name service   # service = ... was written inside setup.py
```
  
