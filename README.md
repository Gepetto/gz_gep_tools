This repository was motivated by the need to show that it was possible to make fast control loop with gazebo (gz) without restarting complex launch files over and over.
Gazebo as a system simulator is allowing to test a full control software stack. While it is well motivated for integrators it is however quite time consuming when one
wants to test quickly a new motion generation scheme.
At the same time gz since Harmonic offers the possibility to test various dynamical simulators such as bullet, bullet feathersone or DART which is of high interest for people interested in new dynamical simulators.


# Installation:

```
git clone
mkdir build
cd build
source /opt/ros/jazzy/setup.bash
cmake ..
make
```
# Test on TALOS

You need to have the repository https://gitlab.laas.fr/ostasse/gz_gepetto_humanoids_models.git

For efficiency concerns you can put:
```
export GZ_IP=127.0.0.1
```

To start the demonstration with the ballon:
```
gz sim ./worlds/ball_talos/ball_talos.sdf
```

For some reason (probably some race conditions due to the numerous contact collision similated),
we need to listen to the cmd_forces Gazebo topic in order to make sure that Gazebo is listening to it:
```
gz topic -e -t /model/Pyrene/joints/cmd_forces
```

Then you can send the control in the build directory of gz_gep_tools:
```
./control_loop t
```
The 't' argument is to use the configuration informations for TALOS.
They are located in ./src/robots_data.cc
