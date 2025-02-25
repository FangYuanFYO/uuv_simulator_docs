Start an empty underwater environment using either 

```bash
roslaunch uuv_gazebo_worlds empty_underwater_world.launch
```

or 

```bash
roslaunch uuv_gazebo_worlds ocean_waves.launch
```

Spawn the remotely operated vehicle RexROV (find the robot description files in [`uuv_descriptions`](https://github.com/uuvsimulator/uuv_simulator/tree/master/uuv_descriptions)) as follows

```bash
roslaunch uuv_descriptions upload_rexrov.launch mode:=default x:=0 y:=0 z:=-20 namespace:=rexrov
```

for which `mode` stands for the configuration of the vehicle to be used. It is important to create the vehicles under a unique `namespace` to allow simulation of multiple vehicles in the same scenario.

You can start a velocity controller with a joystick teleoperation node as 

```bash
roslaunch uuv_control_cascaded_pid joy_velocity.launch uuv_name:=rexrov model_name:=rexrov joy_id:=0
```

In this case `model_name` refers to the vehicle model, which can be different from the `namespace`. It is a necessary parameter to load the correct controller and thruster allocation matrix coefficients. The joystick ID is already set zero as default. To find the correct joystick index, you can install and run `jstest-gtk`.

!!! info

    The mapping of the joystick teleoperation node is set as default for the XBox 360 controller. Remapping is possible by passing the correct indexes of the desired axes in the launch file located in the [`uuv_teleop`](https://github.com/uuvsimulator/uuv_simulator/tree/master/uuv_teleop).

!!! tip

    Sometimes Gazebo takes a while to close. Try
    
    ```bash
    killall -9 gzserver gzclient
    ```
    
    in case that happens.

