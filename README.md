# 🐢 ROS 2 Growing-Square Turtle Controller

## 📖 Overview
This project creates a **ROS 2 package** that controls a [Turtlesim](https://docs.ros.org/en/foxy/Tutorials/Understanding-Topics/Understanding-Topics.html) turtle to move in a **perfect square** pattern, automatically **increasing the side length by 1 meter** each time a square is completed, until it reaches the edge of the map.

The project demonstrates:
- **Publisher / Subscriber** basics
- **Custom ROS 2 package creation**
- Using `geometry_msgs/Twist` to control movement
- Reading `/turtle1/pose` to check position
- Automating a navigation pattern with Python

[Watch Demo](https://drive.google.com/file/d/1M_AJ7Sn6wv7JMguiNfQONg4498JTFVk4/view?usp=sharing)



# 🚀 Getting Started

## 1️⃣ Setup Turtlesim & View Topics
Launch `turtlesim_node` and check available topics.

<img width="3024" height="1964" alt="image" src="https://github.com/user-attachments/assets/7cfacffd-2188-4e28-9611-c48f82d1559f" />


## 2️⃣ Create a Custom Control Package
Create a ROS 2 package to control the turtle:

- **Subscribes** to `/turtle1/pose` (read turtle's current position)
- **Publishes** to `/turtle1/cmd_vel` (control movement)

<img width="3024" height="1832" alt="image" src="https://github.com/user-attachments/assets/2c444e5d-57bc-4ec9-a426-f00237ce1c3a" />  
<img width="3022" height="1822" alt="image" src="https://github.com/user-attachments/assets/cd82a23b-5f99-4c1c-8c53-6b095c03445f" />


### 📁 Package Folder Layout
<img width="1566" height="646" alt="image" src="https://github.com/user-attachments/assets/df1dfcb8-6827-4a44-b349-aa71a10a4623" />


## 3️⃣ Publisher Example — Sending `Int64` Messages
Publisher node output:  
<img width="3024" height="1826" alt="image" src="https://github.com/user-attachments/assets/386d9b04-e1cb-48b2-afa4-98d3ade88aa0" />

Check data types with live topic inspection:  
<img width="3024" height="1824" alt="image" src="https://github.com/user-attachments/assets/82a1dd6a-2bfd-4031-8e9b-4aa22a103931" />


## 4️⃣ Subscriber Example — Receiving `Int64` Messages
<img width="3024" height="1828" alt="image" src="https://github.com/user-attachments/assets/3a1cf46f-4a17-43c2-b68e-031f4c9be7be" />


## 5️⃣ Launching the Whole Package
Use a **launch file** to start both publisher and subscriber nodes together:  
<img width="3024" height="1964" alt="image" src="https://github.com/user-attachments/assets/00cd37b8-62cb-44cf-ac77-e9b0a0ef56b4" />


## 6️⃣ Visualizing in `rqt`
Use `rqt_graph` to see topic connections:  
<img width="3024" height="1964" alt="image" src="https://github.com/user-attachments/assets/ca78618c-ffb2-486f-ae4b-6d9748b930a0" />


# 🎮 Keyboard vs Python Script Control

## **In `turtle_teleop_key`**
- **Publisher:** `turtle_teleop_key`
- **Message Type:** `geometry_msgs/Twist`
- **Topic:** `/turtle1/cmd_vel`

**How it works:**  
Pressing a key sends a velocity command to the turtle.

<img width="2836" height="1062" alt="image" src="https://github.com/user-attachments/assets/fede559a-5a92-4b3c-aacf-8cdd12709acf" />


## **In `turtlesim_node`**
- **Subscriber:** `turtlesim_node`
- **Subscribed Topic:** `/turtle1/cmd_vel`
- **What it does:** Updates position/orientation based on received commands.


## 🔄 Message Flow
1. Press key in `turtle_teleop_key`.
2. Publishes `Twist` → `/turtle1/cmd_vel`.
3. `turtlesim_node` moves turtle.


## 🖥 Using a Python Script
- Acts as a **publisher** to `/turtle1/cmd_vel`.
- Can run alongside teleop, but **last message wins**.


## 📊 Comparison Table

| Control Method        | Role       | Topic              | Publishes Messages? | Requires Manual Input? |
|-----------------------|-----------|--------------------|----------------------|------------------------|
| `turtle_teleop_key`   | Publisher | `/turtle1/cmd_vel` | Yes (`Twist`)        | Yes                    |
| Python Script         | Publisher | `/turtle1/cmd_vel` | Yes (`Twist`)        | No (automated)         |
| `turtlesim_node`      | Subscriber| `/turtle1/cmd_vel` | No                   | N/A                    |

---

# ⚙️ Understanding `colcon build`

## 📌 What it Does
- Searches `src/` for packages
- Builds Python (`setup.py`) or C++ (`CMakeLists.txt`) packages
- Installs files into `install/`
- Registers nodes, launch files, and assets

---

## 📌 When to Run
- After creating a package
- After code changes
- After editing `setup.py` or `CMakeLists.txt`
- After adding dependencies/launch files

---

## ⚠️ If You Skip It
- `ros2 run` may fail
- ROS 2 won’t see your package
- Custom messages won’t be available

---

## 🧠 Analogy
`colcon build` = compiling + installing your code so ROS 2 can use it.
