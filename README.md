# ROS 2 Tasks – Publisher/Subscriber and TurtleSim Square
!(figure_3.png)
## Overview

This project contains two ROS 2 tasks implemented and tested on Ubuntu using ROS 2 Humble.

### Task 1: Publisher and Subscriber

The Publisher sends the message:

    Good morning

The Subscriber receives and displays the same message:

    I heard: "Good morning"

### Task 2: TurtleSim Square

A Python ROS 2 node controls the TurtleSim turtle and makes it move in a square by moving forward and turning left by 90 degrees.

---



# 2. Task 1 – Publisher and Subscriber

## Objective

The objective of this task is to create a ROS 2 Publisher and Subscriber.

The Publisher continuously sends the message:

    Good morning

The Subscriber receives the message and displays:

    I heard: "Good morning"

---



## 2.2 Build the Package

First, move to the ROS 2 workspace:

    cd ~/ros2_ws

Build the package:

    colcon build --packages-select ros2_publisher_subscriber

After the build is completed successfully, source the workspace:

    source ~/ros2_ws/install/setup.bash

---



---


---

## 2.5 Publisher and Subscriber Communication

Both terminals run simultaneously.

The Publisher sends:

    Good morning

The Subscriber receives:

    I heard: "Good morning"

### Communication Flow

    +----------------+
    |    Publisher   |
    +----------------+
            |
            | "Good morning"
            v
    +----------------+
    |    ROS 2 Topic |
    +----------------+
            |
            v
    +----------------+
    |   Subscriber   |
    +----------------+
            |
            | "I heard: Good morning"
            v
    +---------------------------+
    | Successful Communication |
    +---------------------------+



# 3. Task 2 – TurtleSim Square

## Objective

The objective of this task is to create a ROS 2 Python node that controls the TurtleSim turtle and makes it move in a square.

The package created for this task is:

    turtlesim_square

---

## 3.1 Create the Package

Move to the ROS 2 source directory:

    cd ~/ros2_ws/src


---

# 4. TurtleSim Package Configuration

## 4.1 package.xml

The TurtleSim node uses the `Pose` message.

The following dependency is included in `package.xml`:

    <exec_depend>turtlesim</exec_depend>

---

## 4.2 setup.py

The executable is registered in `setup.py` using:

    entry_points={
        'console_scripts': [
            'square = turtlesim_square.square:main',
        ],
    },

This allows the program to be executed using:

    ros2 run turtlesim_square square

---

# 5. TurtleSim Control Program

The TurtleSim program uses the following ROS 2 messages:

    from geometry_msgs.msg import Twist
    from turtlesim.msg import Pose

### Twist

`Twist` is used to control the turtle's movement.

The program publishes velocity commands to:

    /turtle1/cmd_vel

### Pose

`Pose` is used to monitor the turtle's position and orientation.

The program subscribes to:

    /turtle1/pose

---

# 6. Square Movement Logic

The turtle draws the square using four sides.

The movement sequence is:

    Side 1 → Turn 90°
    Side 2 → Turn 90°
    Side 3 → Turn 90°
    Side 4 → Complete

The target directions are:

    0°
    90°
    180°
    270°

The program moves the turtle forward for each side and then turns left to prepare for the next side.

The turtle's position and orientation are monitored using the `Pose` message.

---

# 7. Build the TurtleSim Package

Move to the workspace root:

    cd ~/ros2_ws

Build the package:

    colcon build --packages-select turtlesim_square

After the build is completed successfully, source the workspace:

    source ~/ros2_ws/install/setup.bash

---

# 8. Run TurtleSim

First, start the TurtleSim simulator:

    ros2 run turtlesim turtlesim_node

A TurtleSim window will appear.

Then open another terminal.

Source the workspace:

    source ~/ros2_ws/install/setup.bash

Run the square program:

    ros2 run turtlesim_square square

---

# 9. TurtleSim Execution

During execution, the terminal displays the target directions used by the turtle.

For example:

    Moving forward, target direction: 0.0 degrees

The program then changes the target direction to:

    90.0 degrees
    180.0 degrees
    270.0 degrees

After completing all four sides, the program displays:

    Square completed successfully

---

# 10. TurtleSim Results

The TurtleSim program successfully controls the turtle and makes it move according to the programmed square movement.



The turtle moves forward and changes its direction according to the programmed movement.

## Completed Square

The final result shows the turtle completing the four sides of the square.



The terminal also confirms:

    Square completed successfully

This confirms that the TurtleSim square task was completed successfully.

---


# 12. Verification

## Publisher and Subscriber Verification

The Publisher successfully sends:

    Good morning

The Subscriber successfully receives:

    I heard: "Good morning"

Therefore, communication between the Publisher and Subscriber was successfully verified.

---

## TurtleSim Verification

The TurtleSim node successfully controls the turtle.

The turtle:

- Moves forward.
- Changes direction by 90 degrees.
- Completes four sides.
- Draws a square.

The program finally displays:

    Square completed successfully

Therefore, the TurtleSim square task was successfully verified.

---

# 13. Final Results

### Task 1

    Publisher
        ↓
    "Good morning"
        ↓
    ROS 2 Topic
        ↓
    Subscriber
        ↓
    "I heard: Good morning"

**Result: Successfully Completed**

### Task 2

    TurtleSim
        ↓
    Move Forward
        ↓
    Turn 90°
        ↓
    Move Forward
        ↓
    Turn 90°
        ↓
    Move Forward
        ↓
    Turn 90°
        ↓
    Move Forward
        ↓
    Square Completed

**Result: Successfully Completed**

---

# 14. Conclusion

Both required ROS 2 tasks were successfully implemented, built, executed, and tested on Ubuntu using ROS 2 Humble.

The first task demonstrated ROS 2 topic communication between a Publisher and Subscriber using the message:

    Good morning

The second task demonstrated robot movement using TurtleSim. The turtle was controlled using ROS 2 velocity commands and pose information to complete a square.

The screenshots included in this README provide visual evidence of the successful execution of both tasks.
