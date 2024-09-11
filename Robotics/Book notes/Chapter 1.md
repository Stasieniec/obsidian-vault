# 1.1 Mathematical Modelling of robots
## Symbolic representation of Robots

Robot manipulators:
- Composed of links
- Connected by joints
- Form kinematic chain

Joints
- rotary (revolute): R
- linear (prismatic): P

## The configuration Space

Configuration - a complete specification of the location of every point on the manipulator

**Configuration space** - set of all possible configurations

A robot is in configuration $q$, when the joint variables take on the values $q_1 ... q_n$ with $q_i = \theta_i$ for a revolute joint and $q_i$ = $d_i$ for a prismatic joint. 

An object has $n$ degrees-of-freedom (DOF) if its configuration can be minimally specified by n parameters - the dimension of the configuration space.

A rigid object in three-dimensional space has six DOF:
- Three for positioning
- Three for orientation

A manipulator with more than six DOF is **kinematically redundant**

## The State Space

**State of the manipulator** - set of variables that, together with a description of the manipulator's dynamics and input, are sufficient to determine any future state of the manipulator.

**State space** - set of all possible states

State of the manipulator can be specified by giving the values for the joint variables $q$ and for joint velocities $q'$ 

Representation of a state as a vector $x = (q, q')^T$
The dimension of the state space is $2n$ if the system has $n$ DOF.

## The Workspace

**Workspace** of a manipulator - total volume swept out by the end-effector as the manipulator executes all possible motions.

**Reachable workspace** - set of points reachable by the manipulator

**Dexterous workspace** - set of points that the manipulator can reach with an arbitrary orientation of the end-effector.
