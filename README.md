# Cocos2d-x Deconstruction

<img src="http://www.cocos2d-x.org/attachments/801/cocos2dx_portrait.png" width=200>

Emma Bobola & Janna Shaftan

Northeastern University, EECE4850 - Game Engines

Professor: Nik Bear Brown

Spring 2017

## Introduction

This code deconstruction was written for the purpose of learning how game engines are architected. 'Cocos2d-x' and 'Cocos' will be used interchangeably to refer to the game engine. Cocos is an extensive code base with hundreds of thousands of lines of code. Therefore, we will review the capabilities and overall architecture of the engine, followed by in depth analyses of five main components: the game loop, game objects, physics, graphics, and rendering. 

## Table of Contents

1. [About the Engine](#about-the-engine)
2. [External Dependencies/Libraries](#external-dependencies)
3. [Architecture of Engine Framework](#framework-architecture)
4. [Engine Components](#game-engine-components)

    * [Overview](#component-overview)
    * [Time and the Game Loop](#time-and-game-loop)
    * [Game Objects and Core Classes](#game-objects)
    * [Physics](#physics)
    * [Graphics and Rendering](#graphics-and-rendering)

5. [Conclusion](#conclusion)

## About the Engine

* Release Date: TODO
* Company: Managed by Chukong Technologies Inc.
* MIT License
* History: The concept of Cocos2d-x was created in Los Cocos, Argentina by a team led by developer Ricardo Quesada [3]. In 2010, it was branched by Zhe Wang and rewritten from Python into C++. After a brief acquisition by online gaming giant Zynga Inc., Cocos is now managed by Chukong Technologies Inc. Since then, versions of the Cocos2D family written in Objective-C, Lua and JavaScript have come to exist and be maintained by an open-source community. This allows game development in many languages which are then transformed to and compiled in native C++. The Cocos2D game engine design is notable for it’s emphasis on cross-platform support. 
* Focus: Cross-platform support
* Platform compatibilities:

    * MacOS X
    * Linux
    * Windows 8
    * iOS
    * Android
    * Tizen


## External Dependencies

* Physics ~~~ [Box2D](http://box2d.org/) and [Chipmunk](http://chipmunk-physics.net/)
* Skeleton Animations ~~~ [Spine](http://esotericsoftware.com/) and [Armature](http://www.armaturestudio.com/)
* Sound ~~~ [OpenAL](https://www.openal.org/) based [CocosDenshion library](https://github.com/victorBaro/cocos2d-V2.x-ARC-UIKit/tree/master/cocos2d-2.x-ARC-iOS/libs/CocosDenshion)
* Graphics ~~~ [OpenGL](https://www.opengl.org/)


## Framework Architecture

The Cocos2d Games Architecture:

<img src="https://raw.githubusercontent.com/cocos2d/cocos2d-x/v3/docs/framework_architecture.jpg" width = 600>


[https://raw.githubusercontent.com/cocos2d/cocos2d-x/v3/docs/framework_architecture.jpg](https://raw.githubusercontent.com/cocos2d/cocos2d-x/v3/docs/framework_architecture.jpg)

The 'Cocos2d C++ Engine' is the focus of this analysis. We have created a diagram of the C++ Engine sub-component's architecture:

TODO (create image)

## Game Engine Components

Because of the extensive code base, not all components will be covered in this analysis. The Component Overview provides links to where all key components can be found in the Cocos git repository.

### Component Overview
=

|  |Module|Class or File|Ext. Dependencies|Analyzed|
| ----|----|----|----|----- |
|**Time and Game Loop** | [base](https://github.com/cocos2d/cocos2d-x/tree/v3/cocos/base) | [Director](https://github.com/cocos2d/cocos2d-x/blob/v3/cocos/base/CCDirector.h#L97) - ([mainLoop()](https://github.com/cocos2d/cocos2d-x/blob/v3/cocos/base/CCDirector.cpp#L1429)) | - |**<font color='green'>yes</font>**|
|**Human Interface Devices** | [base](https://github.com/cocos2d/cocos2d-x/tree/v3/cocos/base) | [Controller](https://github.com/cocos2d/cocos2d-x/blob/v3/cocos/base/CCController.h#L50) | - | **<font color='red'>no</font>** |
|**Events and Messaging** | [base](https://github.com/cocos2d/cocos2d-x/tree/v3/cocos/base) | [Event](https://github.com/cocos2d/cocos2d-x/blob/v3/cocos/base/CCEvent.h) | - | **<font color='red'>no</font>** |
|**Graphics and Rendering** | [renderer](https://github.com/cocos2d/cocos2d-x/tree/v3/cocos/renderer) | [Renderer](https://github.com/cocos2d/cocos2d-x/blob/v3/cocos/renderer/CCRenderer.h#L140) | [OpenGL](https://www.opengl.org/) | **<font color='green'>yes</font>** |
|**Game Objects** | [2d](https://github.com/cocos2d/cocos2d-x/tree/v3/cocos/2d) | [Node](https://github.com/cocos2d/cocos2d-x/blob/v3/cocos/2d/CCNode.h#L108) | - | **<font color='green'>yes</font>** |
|**Animation** | [2d](https://github.com/cocos2d/cocos2d-x/tree/v3/cocos/2d) | [Animation](https://github.com/cocos2d/cocos2d-x/blob/v3/cocos/2d/CCAnimation.h#L166) | [Spine](http://esotericsoftware.com/), [Armature](http://www.armaturestudio.com/) | **<font color='red'>no</font>** |
|**Sprites** | [2d](https://github.com/cocos2d/cocos2d-x/tree/v3/cocos/2d) | [Sprite](https://github.com/cocos2d/cocos2d-x/blob/v3/cocos/2d/CCSprite.h#L95) | - | **<font color='red'>yes</font>** |
|**Physics** | [physics](https://github.com/cocos2d/cocos2d-x/tree/v3/cocos/physics), [physics3d](https://github.com/cocos2d/cocos2d-x/tree/v3/cocos/physics3d) | - | [Box2D](http://box2d.org/), [Chipmunk](http://chipmunk-physics.net/) | **<font color='green'>yes</font>** |
|**Rigid Body Dynamics** | [physics](https://github.com/cocos2d/cocos2d-x/tree/v3/cocos/physics) | [PhysicsBody](https://github.com/cocos2d/cocos2d-x/blob/v3/cocos/physics/CCPhysicsBody.h#L63) | - | **<font color='red'>yes</font>** |
|**Collision Detection** | [physics](https://github.com/cocos2d/cocos2d-x/tree/v3/cocos/physics) | [PhysicsContact](https://github.com/cocos2d/cocos2d-x/blob/v3/cocos/physics/CCPhysicsContact.h#L67) | - | **<font color='red'>yes</font>** |
|**Audio** | [audio](https://github.com/cocos2d/cocos2d-x/tree/v3/cocos/audio) | [AudioEngine](https://github.com/cocos2d/cocos2d-x/blob/v3/cocos/audio/AudioEngine.cpp#L70) | [OpenAL](https://www.openal.org/) based [CocosDenshion library](https://github.com/victorBaro/cocos2d-V2.x-ARC-UIKit/tree/master/cocos2d-2.x-ARC-iOS/libs/CocosDenshion) | **<font color='red'>no</font>** |
|**Game Data Management** | [storage/local-storage](https://github.com/cocos2d/cocos2d-x/tree/v3/cocos/storage/local-storage) | [LocalStorage.h](https://github.com/cocos2d/cocos2d-x/blob/v3/cocos/storage/local-storage/LocalStorage.h) | - | **<font color='red'>no</font>** |
|**Platform Resource Management** | [platform](https://github.com/cocos2d/cocos2d-x/tree/v3/cocos/platform) | [FileUtils](https://github.com/cocos2d/cocos2d-x/blob/v3/cocos/platform/CCFileUtils.h#L119) | - | **<font color='red'>no</font>** |
|**Device Hardware** | [platform](https://github.com/cocos2d/cocos2d-x/tree/v3/cocos/platform) | [Device](https://github.com/cocos2d/cocos2d-x/blob/v3/cocos/platform/CCDevice.h#L46), [PlatformConfig.h](https://github.com/cocos2d/cocos2d-x/blob/v3/cocos/platform/CCPlatformConfig.h) | - | **<font color='red'>no</font>** |

* **
### Time and Game Loop
=

The Cocos2d-x game loop is run through an all-powerful manager object called the **Director** which contains initial setup parameters which initialize the OpenGL object, a **CCScene** to start with and takes care of preloading. Here, the control logic for the application lives and reacts to OS interrupts like shut downs and detects running in the background or foreground.

The director’s **mainLoop()** function is triggered by platform-specific **CCApplication** files, which contain slightly different **Application::run()** loops for each supported platform. Each of these loops merely locate the **Director** instance and activate the **Director**’s main loop upon finishing launching. The right platform extension is included in the **CCApplication** header file where *CC_TARGET_PLATFORM* is checked for Mac, iOS, Android, Tizen, Windows or Linux.

[Game Loop Code](https://github.com/cocos2d/cocos2d-x/blob/v3/cocos/base/CCDirector.cpp#L1429):


```c++
void Director::mainLoop()
{
    if (_purgeDirectorInNextLoop)
    {
        _purgeDirectorInNextLoop = false;
        purgeDirector();
    }
    else if (_restartDirectorInNextLoop)
    {
        _restartDirectorInNextLoop = false;
        restartDirector();
    }
    else if (! _invalid)
    {
        drawScene();
     
        // release the objects
        PoolManager::getInstance()->getCurrentPool()->clear();
    }
}
```
**CCDirector** is implemented in *CCDirector.cpp*, in the base directory where core game components live. In Figure II, the initializing function for a Director sheds some light into its responsibilities. 

![](images/init().png "")
*Figure II: CCDirector init() breakdown*

When the **Director** is created, it creates a new associated **Scheduler**, **Action Manager**, **Event Dispatcher** and **Renderer**.  The main loop function in the **Director** class shown in Figure I, checks if the **Director** needs to be purged or restarted and then invokes a call to **drawScene()**. This is actually the physical taskforce of the Cocos2d game loop since it: 
* calculates global time
* updates the Scheduler with current time 
* dispatches Events
* steps forward the Physics
* renders the Scene
* sets the next Scene. 

A brief description of the role of the created components are as follows:
* **Scheduler**: Responsible for triggering scheduled callbacks, for example: ‘update’ which will be called every frame or custom callbacks. 
* **Action Manager**: Singleton responsible for all of a node’s CCActions
* **EventDispatcher**: Manages event listener subscriptions/ dispatches CCEvents. 
* **Renderer**: Sorts and manages the Render Queue, sending RenderCommands to the graphics subsystem.

In Figure III, you can see that the time in Cocos2d is based on real time which is captured by **now**, subtracted from by the **\_lastUpdate** parameter and stored in **\_deltaTime**. At the end of calculating **\_deltaTime**, the **\_lastUpdate** parameter is set to now to continue the cycle.

![](images/drawScene().png "")
*Figure III: Director::drawScene() breakdown*

The director is ultimately responsible for moving from one [scene](https://github.com/cocos2d/cocos2d-x/blob/v3/cocos/2d/CCScene.h) to the next.

* **

### Game Objects
=

Game objects in Cocos are instances of the **Node** class or one of its inheritors. Game objects share several basic qualities given in the **Node** class.

> The **Node** base class contains variables dictating size and position, and methods for several key functionalities:
> * containing other nodes
> * scheduling callbacks for time dependence
> * executing actions

Because of the scope of functionality **Node**'s inheritors encompass, this section will cover only the important aspects of each of the following especially common game objects:

* [**Scene**](#scene-game-object)
* [**Sprite**](#sprite-game-object)

#### Scene Game Object

The [**Scene**](https://github.com/cocos2d/cocos2d-x/blob/d07794052fed5c3edc29d4a60f99399d49271515/cocos/2d/CCScene.h#L69) class is nearly identical to the **Node** ancestor with a few important differences. The **Scene** class is used in Cocos to, ideally, parent all other game objects living in the scene, as such it defaults its anchor to the center of the game world. Additionally, it contains a **Camera** object responsible for view perspective, as well as methods for rendering the Scene.

Objects to be rendered in a scene are attached to the scene object by the following method call:

```c++
scene.addChild(label_node);
```

This code adds a child `label_node` to the scene at index 0. This means that other children at a lower index will be rendered _behind_ the `label_node`, and children at a higher index will be rendered _in front of_ the `label_node`. 

For example the following image:

<img src="http://vignette2.wikia.nocookie.net/adventuretimewithfinnandjake/images/3/38/Islands_Miniseries_Opening.jpg/revision/latest?cb=20161210190503" width=500>

May be organized in the scene by the following code:

```c++
scene.addChild(jakesSail_node, -1);
scene.addChild(title_node);   // defaults to index 0
scene.addChild(finn_node, 1);
```

Any **Node** object with `_isVisible` set `true` will be included when the Scene is rendered. How scenes are rendered will be covered in the [Graphics and Rendering](#graphics-and-rendering) section.

#### Sprite Game Object

The [**Sprite**](https://github.com/cocos2d/cocos2d-x/blob/d07794052fed5c3edc29d4a60f99399d49271515/cocos/2d/CCSprite.h#L95) class is another inheritor of the **Node** class. Important to this class is it's **Texture** member which contains a 2D image used by the sprite object. This class is also limited to containing only other **Sprite** children.

Sprites are created by the following method call, this code uses a constructor that accepts an image for sprite creation: 

```c++
// Create sprite from image directly in constructor:
auto aSprite = Sprite::create("aSprite.png");
```

Sprite images can also be changed at any point:

```c++
// Change image on sprite:
aSprite->setTexture("aDifferentSprite.png");
```

The `aSprite` object can now be manipulated in many ways. The most commonly used properties and their respective method calls are listed below:

* anchor point

>
```c++
mySprite->setAnchorPoint(Vec2(0, 0));
```
>

* position (relative to anchor point)

>
```c++
aSprite->setPosition(Vec2(200, 0));
```
>

* rotation (around the sprite's z axis)

>
```c++
aSprite->setRotation(40);
```
>

* scale

>
```c++
aSprite->setScale(2.0);      // note: this multiplier affects both X and Y axes.
```
>

* **

### Physics
=

Cocos2d comes integrated with a Physics library called [Chipmunk](http://chipmunk-physics.net/), which provides all of the Physics functionalities needed in complex game environment.

##### Rigid Body Dynamics

The fundamental **Physics** structure in Chipmunk involves **PhysicsBody** Nodes, which can be nodes, shapes or constraints which are added to a **PhysicsWorld** container. The developer can create a **Scene** which is governed by a **PhysicsWorld**, complete with gravity, speed and updateRate properties by the following code: 

```c++
auto scene = Scene::createWithPhysics();
```

PhysicsBody Nodes can be static or dynamic and have position and velocity within the World and forces can be applied to manipulate them in the environment. You can associate any Node with a PhysicsBody triggering the following base Node functionality:

```c++
Node::setPhysicsBody();
```
Delving into Cocos2D code responsible for **PhysicsBody** creation, you can see that you are allowed some flexibility to create one with a given mass, a mass and a moment or neither. If you create a body, mass and moment can be automatically computed using the density formula mass = density * area. The default density is *PHYSICSBODY_MATERIAL_DEFAULT* and 0.1f. 

All PhysicsBody creation methods call upon an init() method which create a new \_cpBody and add it to the User’s data. Crucial manipulations of a PhysicsBody include:
* [setGravityEnable()](https://github.com/cocos2d/cocos2d-x/blob/d07794052fed5c3edc29d4a60f99399d49271515/cocos/physics/CCPhysicsBody.cpp#L336)
* [setPosition()](https://github.com/cocos2d/cocos2d-x/blob/d07794052fed5c3edc29d4a60f99399d49271515/cocos/physics/CCPhysicsBody.cpp#L368)
* [applyTorque()](https://github.com/cocos2d/cocos2d-x/blob/d07794052fed5c3edc29d4a60f99399d49271515/cocos/physics/CCPhysicsBody.cpp#L450)
* [applyImpulse()](https://github.com/cocos2d/cocos2d-x/blob/d07794052fed5c3edc29d4a60f99399d49271515/cocos/physics/CCPhysicsBody.cpp#L442)
* [applyForce()](https://github.com/cocos2d/cocos2d-x/blob/d07794052fed5c3edc29d4a60f99399d49271515/cocos/physics/CCPhysicsBody.cpp#L432)
* [setMass()](https://github.com/cocos2d/cocos2d-x/blob/d07794052fed5c3edc29d4a60f99399d49271515/cocos/physics/CCPhysicsBody.cpp#L455)
* [setVelocity()](https://github.com/cocos2d/cocos2d-x/blob/d07794052fed5c3edc29d4a60f99399d49271515/cocos/physics/CCPhysicsBody.cpp#L576)
* [setAngularVelocity()](https://github.com/cocos2d/cocos2d-x/blob/d07794052fed5c3edc29d4a60f99399d49271515/cocos/physics/CCPhysicsBody.cpp#L602)
* [isResting()](https://github.com/cocos2d/cocos2d-x/blob/d07794052fed5c3edc29d4a60f99399d49271515/cocos/physics/CCPhysicsBody.cpp#L754)
* [setCollisionBitmask()](https://github.com/cocos2d/cocos2d-x/blob/d07794052fed5c3edc29d4a60f99399d49271515/cocos/physics/CCPhysicsBody.cpp#L822)

##### Continuous Collision Detection

**[Box2D](http://box2d.org/manual.pdf)** is another library that comes with Cocos and has a variety of functions that simulate 2D rigid body dynamics. This is a more advanced feature for users requiring high performance in physics from their games. 

Box2D supports **continuous collision detection**, which is not present in the built-in Chipmunk Physics engine. CCD is a technique used to prevent dynamic bodies from tunneling through static bodies. When tunneling occurs, a scenario like a bullet moving through a glass wall might simply appear as the bullet moving through the wall and reappearing on the other end, with no collision.
This is done by moving shapes in a sweeping motion from their old coordinates to their new coordinates. During the sweep, Box2D looks for collisions that will take place and computes the time of these collisions. At the (TOI) time of impact, the engine executes the collision response function for each body in contact.

#### Collision Detection

A **Physics Contact** object is created when two shapes come into contact with each other and destroyed when the contact has ended. This **PhysicsContact** object has methods to retrieve the object properties which have collided with each other, as well as their Contact and preContact data. 
There is a **EventListenerPhysicsContact** object which receives all the contact callbacks. This object houses functions which perform the collision processing, such as:

```c++
    /**
     * @brief It will called at two shapes start to contact, and only call it once.
     */
    std::function<bool(PhysicsContact& contact)> onContactBegin;
    /**
     * @brief Two shapes are touching during this step. Return false from the callback to make world ignore the collision this step or true to process it normally. Additionally, you may override collision values, restitution, or surface velocity values.
     */
    std::function<bool(PhysicsContact& contact, PhysicsContactPreSolve& solve)> onContactPreSolve;
    /**
     * @brief Two shapes are touching and their collision response has been processed. You can retrieve the collision impulse or kinetic energy at this time if you want to use it to calculate sound volumes or damage amounts. See cpArbiter for more info
     */
    std::function<void(PhysicsContact& contact, const PhysicsContactPostSolve& solve)> onContactPostSolve;
    /**
     * @brief It will called at two shapes separated, and only call it once.
     * onContactBegin and onContactSeparate will called in pairs.
     */
    std::function<void(PhysicsContact& contact)> onContactSeparate; 
```
EventListenerPhysics vary slightly depending on whether Bodies, Shapes, or Groups collide. They retrieve the objects using different get methods tailored to account for property differences between the three main types of eventful Nodes. 

* **

### Graphics and Rendering
=

At each iteration of the game loop, the states of various objects in the game change. After all changes to a scene and its children are made, rendering can be used to translate the codified game objects into values the graphics can use to display the scene. Cocos does this for the developer by performing these tasks at each iteration of [`mainLoop()`](#time-and-game-loop) when `drawScene()` is called.

1. Clear the renderer
2. Update current scene
3. Update time dependent states in scene's objects (physics and navigation)
4. Clear draw stats on the renderer
5. Render in the graphics object
6. Swap buffers in the graphics object

At each iteration of the game loop, the states of various objects in the game change. After all changes to a scene and its children are made, rendering can be used to translate the codified game objects into values the graphics can use to display the scene. Cocos does this for the developer by performing these tasks at each iteration of [`mainLoop()`](#time-and-game-loop) when [`drawScene()`](https://github.com/cocos2d/cocos2d-x/blob/v3/cocos/base/CCDirector.cpp#L263) is called.

Rendering the next scene makes calls to OpenGL. In addition to the `_openGLView` object used by the **Director** class, Cocos calls OpenGL static methods. These methods are prefixed with 'gl'- for example `glClearColor()`. In total, rendering of the `_runningScene` is handled by two core classes, the **GLView** class, and **Renderer** class. Below is a brief overview of these classes:

**[GLView](https://github.com/cocos2d/cocos2d-x/blob/v3/cocos/platform/CCGLView.h#L100):**

**GLView** is an abstract class that is inherited by the **GLViewImpl** class in each platform with behaviors specific to that platform. This will be discussed later in the [Platform](#platform) section. An example of platform dependent graphics might be the need to check for and accommodate the high pixel density of a retina display on an ios device.

The **GLViewImpl** is set through preprocessor configuration directives. For our purposes we will be referencing the [ios implementation](https://github.com/cocos2d/cocos2d-x/blob/d07794052fed5c3edc29d4a60f99399d49271515/cocos/platform/ios/CCGLViewImpl-ios.h#L41).

**[Renderer](https://github.com/cocos2d/cocos2d-x/blob/v3/cocos/renderer/CCRenderer.h#L140):**

The Renderer performs the work of mapping various game objects rendering needs into a uniform set of instructions for the graphics to display on screen. 
>

For our rendering analysis we will be following the render path made from the Director's game loop. Before the Director can render the next scene, it must first request that the renderer [clears the current display](https://github.com/cocos2d/cocos2d-x/blob/v3/cocos/renderer/CCRenderer.cpp#L666):

```c++
void Renderer::clear()
{
    //Enable Depth mask to make sure glClear clear the depth buffer correctly
    glDepthMask(true);
    glClearColor(_clearColor.r, _clearColor.g, _clearColor.b, _clearColor.a);
    glClear(GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT);
    glDepthMask(false);

    RenderState::StateBlock::_defaultState->setDepthWrite(false);
}
```

The previous `_runningScene` having been cleared from the graphics, the next scene is put into the `_runningScene` variable. It's time dependent attributes, such as physics, are then updated before it is finally rendered.

The rendering call is made to the [`void GLView::renderScene(Scene* scene, Renderer* renderer)`](https://github.com/cocos2d/cocos2d-x/blob/d07794052fed5c3edc29d4a60f99399d49271515/cocos/platform/CCGLView.cpp#L486) method. The path through code taken to execute rendering from `drawScene()` is shown in the below:

```c++
Director::drawScene() {
   _openGLView->renderScene(_runningScene, _renderer);
```
>
```c++
void GLView::renderScene(Scene* scene, Renderer* renderer) {
   scene->render(renderer, Mat4::IDENTITY, nullptr);
```
>
> >
```c++
void Scene::render(Renderer* renderer, const Mat4& eyeTransform, const Mat4* eyeProjection) {
    render(renderer, &eyeTransform, eyeProjection, 1);
```
> >
> > >
```c++
void Scene::render(Renderer* renderer, const Mat4* eyeTransforms, const Mat4* eyeProjections, unsigned int multiViewCount) {
   auto director = Director::getInstance();
```
> > >

Now this seems very confusing but we give the developers some credit and assume that some class somewhere is using the intermediate methods for rendering. Therefore we will ignore the strange circularity of getting the Director instance in the eventual rendering method called from the Director.

This [`Scene::render(...)`]((https://github.com/cocos2d/cocos2d-x/blob/d07794052fed5c3edc29d4a60f99399d49271515/cocos/2d/CCScene.cpp#L192)) method is where much of the scene's rendering actually occurs. The scene’s render method performs camera projection manipulation before rendering the graphics. The camera class is not covered in this deconstruction. After camera projection manipulation, the renderer’s [`render(...)`](https://github.com/cocos2d/cocos2d-x/blob/d07794052fed5c3edc29d4a60f99399d49271515/cocos/renderer/CCRenderer.cpp#L624) method is called for the final transition from code to the graphics buffer. To do this, the renderer processes **RenderCommands** waiting in a queue:

```c++
for (auto &renderqueue : _renderGroups)
     {
         renderqueue.sort();
     }
visitRenderQueue(_renderGroups[0]);
```

`visitRenderQueue(...)` checks for 2D or 3D depth, and processes the game objects that need to be rendered. It does this from back to front. This ordering of objects was mentioned earlier in the [scene game objects](#scene-game-objects) section. Finally, the [render state of the queue is updated](https://github.com/cocos2d/cocos2d-x/blob/d07794052fed5c3edc29d4a60f99399d49271515/cocos/renderer/CCRenderer.cpp#L161) where the processed values in the queue are translated to the waiting graphics buffer.

Finally, the graphics buffers are swapped:

```c++
void GLViewImpl::swapBuffers()
{
    CCEAGLView *eaglview = (CCEAGLView*) _eaglview;
    [eaglview swapBuffers];
}
```

Swapping the graphics buffers is how the last set of pixels are replaced with the next set. This is when the graphics on display are changed and the process starts over in the next game loop.

* **

## Conclusion
Cocos2d-x is an open-source game engine, often used to develop mobile applications, due to it's emphasis on cross-platform support and integration with graphics and physics engines which can be selectively chosen by the programmer by the degree of control and customizability they'd like to have over their creation. 
