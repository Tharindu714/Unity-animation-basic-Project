# Unity Animation Basics Project

> **Learn and experiment** with Unity’s animation system through practical examples—covering Animation Clips, Animator Controllers, Blend Trees, and script-driven triggers.

---

## 🎯 Project Overview

This project demonstrates core Unity animation features:

1. **Animation Clips & Keyframes**: Creating and importing basic clips (idle, walk, run, jump).
2. **Animator Controller**: State machines, parameters, and transitions.
3. **Blend Trees**: Smooth blending between movement animations based on float parameters.
4. **Triggers & Script Control**: Firing animation events and controlling states via C# scripts.
5. **Root Motion vs In-place**: Managing motion through animation vs code-driven movement.
6. **Animation Events**: Synchronizing sound effects and gameplay logic with keyframe events.

---

## 📁 Project Structure

```
Unity-animation-basic-Project/
├── Assets/
│   ├── Animations/           # .anim clips and Blend Tree assets
│   │   ├── Idle.anim         # Idle animation clip
│   │   ├── Walk.anim
│   │   ├── Run.anim
│   │   └── Jump.anim
│   ├── AnimatorControllers/  # Animator Controller assets
│   │   └── CharacterController.controller
│   ├── Prefabs/              # Prefab with Animator component attached
│   │   └── Character.prefab
│   ├── Scenes/               # Sample demo scenes
│   │   ├── AnimationDemo.unity
│   │   └── BlendTreeDemo.unity
│   ├── Scripts/              # C# scripts for controlling animations
│   │   ├── AnimationTrigger.cs
│   │   ├── BlendTreeController.cs
│   │   └── RootMotionController.cs
│   └── UI/                   # Optional UI elements for buttons and sliders
├── ProjectSettings/          # Unity project configuration
├── Packages/                 # Unity package manifest
├── .gitignore
├── LICENSE                   # Apache-2.0
└── README.md                 # (this file)
```

---

## 🛠️ Prerequisites & Setup

1. **Unity 2021.3 LTS** or newer.
2. **Visual Studio 2019+** or **Rider** with Unity plugin.
3. **Git** client for cloning the repository.

**Clone & Open**:

```bash
git clone https://github.com/Tharindu714/Unity-animation-basic-Project.git
# In Unity Hub: Add the project folder and click "Open".
```

---

## 🚀 Animation Workflow

### 1. Animation Clips & Import

* **Idle, Walk, Run, Jump**: Created in Unity or imported from external tools.
* **Settings**: Ensure correct loop time for continuous animations (e.g., Idle, Walk, Run).

### 2. Animator Controller

* **States**: Add each clip as a state in the Animator window.
* **Parameters**:

  * **Float** `Speed` for blend tree control.
  * **Trigger** `Jump` for one-off jump animation.
* **Transitions**:

  * From `Any State` to `Jump` on `Jump` trigger.
  * Blend Tree state transitions based on `Speed` thresholds.

### 3. Blend Tree Setup

* **Blend Tree** decision type: `1D` using `Speed` parameter.
* **Motion Fields**: Map Idle at `0`, Walk at `0.5`, Run at `1.0`.

### 4. Root Motion vs In-Place

* **Root Motion**: Enabled on Animator if animation drives object position.
* **In-Place**: Disable root motion and move character via script for precise control.

### 5. Animation Events

* **Adding Events**: In Animation window, define event at specific keyframe.
* **Handling in Code**: Corresponding method in script (e.g., `PlayFootstepSound`).

---

## 🎮 Controlling Animations via Script

### `AnimationTrigger.cs`

```csharp
public class AnimationTrigger : MonoBehaviour {
    private Animator anim;
    void Awake() => anim = GetComponent<Animator>();
    void Update() {
        if (Input.GetKeyDown(KeyCode.Space))
            anim.SetTrigger("Jump");
    }
}
```

### `BlendTreeController.cs`

```csharp
public class BlendTreeController : MonoBehaviour {
    private Animator anim;
    void Awake() => anim = GetComponent<Animator>();
    void Update() {
        float h = Input.GetAxis("Horizontal");
        float v = Input.GetAxis("Vertical");
        float speed = new Vector2(h, v).magnitude;
        anim.SetFloat("Speed", speed);
    }
}
```

### `RootMotionController.cs`

```csharp
public class RootMotionController : MonoBehaviour {
    private Animator anim;
    void Awake() => anim = GetComponent<Animator>();
    void OnAnimatorMove() {
        transform.position += anim.deltaPosition;
    }
}
```

---

## 🖥️ Demo Scenes

| Scene           | Description                                         |
| --------------- | --------------------------------------------------- |
| `AnimationDemo` | Trigger jump using `AnimationTrigger` script.       |
| `BlendTreeDemo` | Control movement speed to see blend tree in action. |

**Run the Demo**:

* Open the desired scene.
* Press **Play** in Unity Editor.
* Use **WASD** or arrow keys to move.
* Hit **Space** to jump.

---

## 📸 Screenshots

<p align="center">
  <img src="Assets/Images/AnimatorSetup.png" width="45%" />
  &nbsp;
  <img src="Assets/Images/BlendTreeGraph.png" width="45%" />
</p>

---

## 📈 Performance & Best Practices

* **Optimize Clip Settings**: Use `Compression` on imported animations.
* **Limit Parameters**: Avoid too many Animator parameters for performance.
* **Profiling**: Use **Profiler** to monitor **Animator** CPU usage.

---

## 🚀 Next Steps

* **Advanced State Machines**: Layered animation controllers.
* **Inverse Kinematics**: Apply IK for foot placement.
* **Motion Capture**: Import and retarget mocap data.
* **Procedural Animation**: Combine runtime-generated motion with keyframe clips.

---

## 🤝 Contributing

Contributions welcome! Fork, create a feature branch, and submit a pull request.

---

## 📄 License

Apache-2.0 © 2025 Tharindu714

