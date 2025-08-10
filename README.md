# ROS2

1. Setup turtlesim and  view publisher/subscriber topic info

<img width="3024" height="1964" alt="image" src="https://github.com/user-attachments/assets/7cfacffd-2188-4e28-9611-c48f82d1559f" />

2. Create a package space to control our turtle
<img width="3024" height="1832" alt="image" src="https://github.com/user-attachments/assets/2c444e5d-57bc-4ec9-a426-f00237ce1c3a" />

`Pub_Sub Package` for turtle bot position nodes
- Subscribing to the /turtle1/pose topic (read the turtle's current position)
- Publishing to the /turtle1/cmd_vel topic (control the turtle's movement)
<img width="3022" height="1822" alt="image" src="https://github.com/user-attachments/assets/cd82a23b-5f99-4c1c-8c53-6b095c03445f" />

---

#### 📁 Folder Structure

<img width="1566" height="646" alt="image" src="https://github.com/user-attachments/assets/df1dfcb8-6827-4a44-b349-aa71a10a4623" />

---

3. Publisher Sending Int64 Msg

<img width="3024" height="1826" alt="image" src="https://github.com/user-attachments/assets/386d9b04-e1cb-48b2-afa4-98d3ade88aa0" />


we can also check from live toppic list to ensure our data type fit our setting
<img width="3024" height="1824" alt="image" src="https://github.com/user-attachments/assets/82a1dd6a-2bfd-4031-8e9b-4aa22a103931" />


5. Subscriber Receiving Int64 Msg

<img width="3024" height="1828" alt="image" src="https://github.com/user-attachments/assets/3a1cf46f-4a17-43c2-b68e-031f4c9be7be" />

6. Use the launch file to launch the whole pub/sub package (both publosher and subscriber node)

<img width="3024" height="1964" alt="image" src="https://github.com/user-attachments/assets/00cd37b8-62cb-44cf-ac77-e9b0a0ef56b4" />

we can also view how our noeds are conncted in rqt (a GUI interface that provides a modular, plugin-based interface to visualize and interact with your ROS nodes, topics, services, parameters)

<img width="3024" height="1964" alt="image" src="https://github.com/user-attachments/assets/ca78618c-ffb2-486f-ae4b-6d9748b930a0" />

# Turtlesim Keyboard Teleoperation vs Python Script Control

This document explains the message flow and control differences between using `turtle_teleop_key` and a Python script to control Turtlesim in ROS 2.

---

## 🐢 In `turtle_teleop_key`
- **Publisher:** `turtle_teleop_key` node
- **Message type:** `geometry_msgs/Twist`
- **Topic:** `/turtle1/cmd_vel`

**How it works:**
- Every time you press a key, `turtle_teleop_key` creates a `Twist` message (with linear & angular velocities) and publishes it to `/turtle1/cmd_vel`.
- It’s essentially saying:  
  > "Hey turtle, here’s your velocity command."
  > <img width="2836" height="1062" alt="image" src="https://github.com/user-attachments/assets/fede559a-5a92-4b3c-aacf-8cdd12709acf" />


---

## 🖥️ In `turtlesim_node`
- **Subscriber:** `turtlesim_node`
- **Subscribed topic:** `/turtle1/cmd_vel`

**What it does:**
- Listens for incoming `Twist` messages.
- Updates the turtle’s position & orientation based on those commands.

---

## 🔄 Order of Events
1. You press an arrow key.
2. `turtle_teleop_key` **publishes** a `Twist` message → `/turtle1/cmd_vel`.
3. `turtlesim_node` **receives** that message and moves the turtle.

---

## 📜 Using a Python Script
If you later write a Python script:
- It will also act as a **publisher** to `/turtle1/cmd_vel`.
- If both run, both will send velocity commands.
- The **last message** received by `turtlesim_node` at any moment wins.

---

## 📊 Summary Table

| Control Method        | Role       | Topic              | Publishes Messages? | Requires Manual Input? |
|-----------------------|-----------|--------------------|----------------------|------------------------|
| `turtle_teleop_key`   | Publisher | `/turtle1/cmd_vel` | Yes (`Twist`)        | Yes                    |
| Python Script         | Publisher | `/turtle1/cmd_vel` | Yes (`Twist`)        | No (automated)         |
| `turtlesim_node`      | Subscriber| `/turtle1/cmd_vel` | No                   | N/A                    |

---

## 📝 Notes
- `turtle_teleop_key` is always the **publisher**.
- `turtlesim_node` is always the **subscriber**.
- Multiple publishers can send commands to the same topic — the most recent message determines the turtle's movement.





## 📦 Understanding `colcon build` in ROS 2

### 🛠 What `colcon build` Does

ROS 2 will:

- 🔍 Search your `src/` folder for ROS 2 packages
- 🧱 Build Python (`setup.py`) or C++ (`CMakeLists.txt`) packages
- 📦 Place the installed files into the `install/` folder
- 📚 Register nodes, launch files, and other assets so `ros2 run` and `ros2 topic` can access them

---

### 📌 When to Run `colcon build`

You should run `colcon build`:

- After creating a new package
- After changing source code
- After editing `setup.py` or `CMakeLists.txt`
- After adding new dependencies or launch files

---

### ⚠️ If You Skip This Step

If you don’t run `colcon build`:

- `ros2 run` may return **"No executable found"**
- ROS 2 won’t recognize your package
- Custom messages/services won’t be available

---

### 🧠 Simple Analogy

Running `colcon build` is like:

- 🛠 Compiling C++ code
- 📦 Installing a local Python package
- 🧹 Organizing your code so ROS 2 knows how to use it

---

### ✅ Example

```bash
cd ~/ros2_ws
colcon build
source install/setup.bash





