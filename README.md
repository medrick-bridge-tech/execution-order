# Execution Order

## Table of Contents

- [Introduction](#Introduction)
    - [Script lifecycle flowchart](#Script-lifecycle-flowchart)
- [First Scene Load](#First-Scene-Load)
- [Editor](#Editor)
- [Before The First Frame Update](#Before-The-First-Frame-Update)
- [In between frames](#in-between-frames)
- [Update order](#update-order)
- [Animation update loop]
- [Rendering](#rendering)
- [Coroutines]
- [When The Object Is Destroyed](#when-the-object-is-destroyed)
- [When quitting](#when-quitting)
---
## Introduction
**When a Unity script runs, number of events & functions executes in order. In this repository we will learn about those execution orders.**
- ### Script lifecycle flowchart
- <img src="images/execution-order-flowchart.png" width="800px" height="1800px">
---
## First Scene Load

**These functions get called when a scene starts**

- **Awake:** Before any start functions and just after prefab is instantiated, it is called.
    - If a GameObject is inactive during start up, Awake is not called until it is made active.
- **OnEnable:** Only called just after the object is enabled.
---
## Editor

**These functions get called after script set**

- **Reset:** When script is attached to game object, Reset function is called to initialize the script’s properties.
- **OnValidate:** It is called when the script is loaded or a value changes in the Inspector. Use OnValidate function to perform an action after a value changes in the Inspector; for example, making sure that data stays within a certain range.
    - [Example](https://www.youtube.com/watch?v=G4jVTBA49Rc)
---
## Before The First Frame Update

**For all objects that are part of a scene asset, this function is called before Update**

- **Start:** Start is called before the first frame update whenever the script instance is enabled.
---
## In Between Frames

- **OnApplicationPause:** At the end of the frame is called where the pause is detected.
---
## Update Order

- **FixedUpdate:** It is called before Any update. All physics calculations and updates occur immediately after FixedUpdate. 
- **Update:** Update is called once per frame. It is the main workhorse function for frame updates.
- **LateUpdate:**  LateUpdate is called once per frame, after Update has finished.
    - A common use for LateUpdate would be a following third-person camera. If you make your character move and turn inside Update, you can perform all camera movement and rotation calculations in LateUpdate. This will ensure that the character has moved completely before the camera tracks its position.
---
## Animation Update Loop

---
## Useful Profile Markers

---
## Rendering

**These functions interacts with the screen and inputs**

- **OnPreCull:** Called before the camera culls the scene. Culling determines which objects are visible to the camera. OnPreCull is called just before culling takes place.
- **OnBecameVisible/OnBecameInvisible:** Called when an object becomes visible/invisible to any camera.
- **OnWillRenderObject:** Called once for each camera if the object is visible.
- **OnPreRender:** Called before the camera starts rendering the scene.
- **OnRenderObject:** Called after all regular scene rendering is done. You can use GL class or Graphics.DrawMeshNow to draw custom geometry at this point.
- **OnPostRender:** Called after a camera finishes rendering the scene.
- **OnRenderImage:** Called after scene rendering is complete to allow post-processing of the image, see Post-processing Effects.
- **OnGUI:** Called multiple times per frame in response to GUI events. The Layout and Repaint events are processed first, followed by a Layout and keyboard/mouse event for each input event.
- **OnDrawGizmos:** Used for drawing Gizmos in the scene view for visualisation purposes.

---
## Coroutines

**Coroutine updates are run after the Update function returns. A coroutine is a function that can suspend its execution until the given 'yield' instruction finishes.**

- **yield:** The coroutine will continue after all Update functions have been called on the next frame.
- **yield WaitForSeconds:** Continue after a specified time delay, after all Update functions have been called for the frame.
- **yield WaitForFixedUpdate:** Continue after all FixedUpdate has been called on all scripts. If the coroutine yielded before FixedUpdate, then it resumes after FixedUpdate in the current frame.
- **yield WWW:** Continue after a WWW download has completed.
- **yield StartCoroutine:** Chains the coroutine, and will wait for the MyFunc coroutine to complete first.
---
## When The Object Is Destroyed

- **OnDestroy:** This function is called on the last frame of object before destroying.
---
## When Quitting

- **OnApplicationQuit:** Before the application is quit called. In the editor it is called when the user stops playmode.
- **OnDisable:** When object becomes disabled or inactive is called.
---