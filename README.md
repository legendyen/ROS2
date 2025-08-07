# ROS2

1. Setup turtlesim and  view publisher/subscriber topic info
<img width="3024" height="1816" alt="image" src="https://github.com/user-attachments/assets/9fe874a4-9221-4a8f-83a2-5611d06a8b5e" />

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


