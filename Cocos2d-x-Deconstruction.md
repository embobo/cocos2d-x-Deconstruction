<img src="http://www.cocos2d-x.org/attachments/801/cocos2dx_portrait.png" width=200>

# Cocos2d-x Deconstruction

Emma Bobola & Janna Shaftan

Northeastern University, EECE4850 - Game Engines

Professor: Nik Bear Brown

Spring 2017

## Introduction

This analysis will cover the game loop, game object, graphics, and rendering of the Cocos2d-x engine version 3+. 'Cocos2d-x' and 'Cocos' will be used interchangeably to refer to the game engine.

## Engine About:

* release date
* company
* history
* what the engine offers as compared to older versions
* MIT License
* Cross-Platform
* * MacOS X
* * Linux
* * Windows 8
* * iOS
* * Android
* * Tizen


### External Dependencies:

* Physics ~~~ [Box2D](http://box2d.org/) and [Chipmunk](http://chipmunk-physics.net/)
* Skeleton Animations ~~~ [Spine](http://esotericsoftware.com/) and [Armature](http://www.armaturestudio.com/)
* Sound ~~~ [OpenAL](https://www.openal.org/) based [CocosDenshion library](https://github.com/victorBaro/cocos2d-V2.x-ARC-UIKit/tree/master/cocos2d-2.x-ARC-iOS/libs/CocosDenshion)
* Graphics ~~~ [OpenGL](https://www.opengl.org/)


### Architecture:

The Cocos2d-x Games Architecture:

<img src="https://raw.githubusercontent.com/cocos2d/cocos2d-x/v3/docs/framework_architecture.jpg" width = 600>


[https://raw.githubusercontent.com/cocos2d/cocos2d-x/v3/docs/framework_architecture.jpg](https://raw.githubusercontent.com/cocos2d/cocos2d-x/v3/docs/framework_architecture.jpg)

The 'Cocos2d C++ Engine' (or 'Cocos2d-x') is the focus of this analysis. We have created a sub-analysis of the C++ Engine's architecture:

(create image)

Game Engine Components
=

Because of the extensive code base, not all components will be covered in this analysis. Provided for reference are all of the names and links to where key components can be found in the git repository.

#### Key Engine Components:

|  |Module|Class or File|Ext. Dependencies|Analyzed|
| ----|----|----|----|----- |
|**Time and Game Loop** | [base](https://github.com/cocos2d/cocos2d-x/tree/v3/cocos/base) | [Director](https://github.com/cocos2d/cocos2d-x/blob/v3/cocos/base/CCDirector.h#L97) - ([mainLoop()](https://github.com/cocos2d/cocos2d-x/blob/v3/cocos/base/CCDirector.cpp#L1429)) | - | **<font color='green'>yes</font>** |
|**Human Interface Devices** | [base](https://github.com/cocos2d/cocos2d-x/tree/v3/cocos/base) | [Controller](https://github.com/cocos2d/cocos2d-x/blob/v3/cocos/base/CCController.h#L50) | - | **<font color='red'>no</font>** |
|**Events and Messaging** | [base](https://github.com/cocos2d/cocos2d-x/tree/v3/cocos/base) | [Event](https://github.com/cocos2d/cocos2d-x/blob/v3/cocos/base/CCEvent.h) | - | **<font color='red'>no</font>** |
|**Graphics and Rendering** | [renderer](https://github.com/cocos2d/cocos2d-x/tree/v3/cocos/renderer) | [Renderer](https://github.com/cocos2d/cocos2d-x/blob/v3/cocos/renderer/CCRenderer.h#L140) | [OpenGL](https://www.opengl.org/) | **<font color='green'>yes</font>** |
|**Game Objects** | [2d](https://github.com/cocos2d/cocos2d-x/tree/v3/cocos/2d) | [Node](https://github.com/cocos2d/cocos2d-x/blob/v3/cocos/2d/CCNode.h#L108) | - | **<font color='green'>yes</font>** |
|**Animation** | [2d](https://github.com/cocos2d/cocos2d-x/tree/v3/cocos/2d) | [Animation](https://github.com/cocos2d/cocos2d-x/blob/v3/cocos/2d/CCAnimation.h#L166) | [Spine](http://esotericsoftware.com/), [Armature](http://www.armaturestudio.com/) | **<font color='red'>no</font>** |
|**Sprites** | [2d](https://github.com/cocos2d/cocos2d-x/tree/v3/cocos/2d) | [Sprite](https://github.com/cocos2d/cocos2d-x/blob/v3/cocos/2d/CCSprite.h#L95) | - | **<font color='red'>no</font>** |
|**Physics** | [physics](https://github.com/cocos2d/cocos2d-x/tree/v3/cocos/physics), [physics3d](https://github.com/cocos2d/cocos2d-x/tree/v3/cocos/physics3d) | - | [Box2D](http://box2d.org/), [Chipmunk](http://chipmunk-physics.net/) | **<font color='red'>no</font>** |
|**Rigid Body Dynamics** | [physics](https://github.com/cocos2d/cocos2d-x/tree/v3/cocos/physics) | [PhysicsBody](https://github.com/cocos2d/cocos2d-x/blob/v3/cocos/physics/CCPhysicsBody.h#L63) | - | **<font color='red'>no</font>** |
|**Collision Detection** | [physics](https://github.com/cocos2d/cocos2d-x/tree/v3/cocos/physics) | [PhysicsContact](https://github.com/cocos2d/cocos2d-x/blob/v3/cocos/physics/CCPhysicsContact.h#L67) | - | **<font color='red'>no</font>** |
|**Audio** | [audio](https://github.com/cocos2d/cocos2d-x/tree/v3/cocos/audio) | [AudioEngine](https://github.com/cocos2d/cocos2d-x/blob/v3/cocos/audio/AudioEngine.cpp#L70) | [OpenAL](https://www.openal.org/) based [CocosDenshion library](https://github.com/victorBaro/cocos2d-V2.x-ARC-UIKit/tree/master/cocos2d-2.x-ARC-iOS/libs/CocosDenshion) | **<font color='red'>no</font>** |
|**Game Data Management** | [storage/local-storage](https://github.com/cocos2d/cocos2d-x/tree/v3/cocos/storage/local-storage) | [LocalStorage.h](https://github.com/cocos2d/cocos2d-x/blob/v3/cocos/storage/local-storage/LocalStorage.h) | - | **<font color='red'>no</font>** |
|**Platform Resource Management** | [platform](https://github.com/cocos2d/cocos2d-x/tree/v3/cocos/platform) | [FileUtils](https://github.com/cocos2d/cocos2d-x/blob/v3/cocos/platform/CCFileUtils.h#L119) | - | **<font color='red'>no</font>** |
|**Device Hardware** | [platform](https://github.com/cocos2d/cocos2d-x/tree/v3/cocos/platform) | [Device](https://github.com/cocos2d/cocos2d-x/blob/v3/cocos/platform/CCDevice.h#L46), [PlatformConfig.h](https://github.com/cocos2d/cocos2d-x/blob/v3/cocos/platform/CCPlatformConfig.h) | - | **<font color='red'>no</font>** |


## Time and Game Loop:

The game loop runs from the **Director** class.

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

The director is ultimately responsible for moving from one [scene](https://github.com/cocos2d/cocos2d-x/blob/v3/cocos/2d/CCScene.h) to the next.

## Graphics and Rendering:

Games are appealing because elements of the game react and change. For example the user may control a karate master fighter player on screen. When the player lands a hit the opposing fighter might be updated to have a bloody nose.

> 'User' is a word which here means someone who is operating the machine on which a game is running.
> 
> 'Player' is a word which will be used to refer to the in game character controlled by the user. 
> 
> ![](images/userVPlayer-AdventureTime.png "")

At each iteration of the game loop, the states of various objects in the game change, such as our fighter character after being punched.  [how is this implemented in the Scene?]

[insert image for this]

After all changes to the scene are made, rendering can be used to translate the codified game objects into parameters the graphics can use to display the scene. Cocos performs these tasks at each iteration of the game loop when `drawScene()` is called.

* Clear the renderer
* Change current scene to the next scene
* Update time dependent states in scene's objects (physics and navigation)
* Clear draw stats on the renderer
* Render in the graphics object
* Swap buffers in the graphics object

[Clear the renderer:](https://github.com/cocos2d/cocos2d-x/blob/v3/cocos/renderer/CCRenderer.cpp#L666)

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

[Set `_runningScene`](https://github.com/cocos2d/cocos2d-x/blob/v3/cocos/base/CCDirector.cpp#L1144) to the scene that needs to be rendered

[Update object transforms](https://github.com/cocos2d/cocos2d-x/blob/v3/cocos/2d/CCScene.cpp#L358) (physics and navigation)

[Clear the renderer's draw stats](https://github.com/cocos2d/cocos2d-x/blob/v3/cocos/renderer/CCRenderer.h#L194)

```c++
void clearDrawStats() { _drawnBatches = _drawnVertices = 0; }
```

[Render scene in the graphics object](https://github.com/cocos2d/cocos2d-x/blob/v3/cocos/platform/CCGLView.cpp#L486)

```c++
void GLView::renderScene(Scene* scene, Renderer* renderer)
{
    CCASSERT(scene, "Invalid Scene");
    CCASSERT(renderer, "Invalid Renderer");

    if (_vrImpl)
    {
        _vrImpl->render(scene, renderer);
    }
    else
    {
        scene->render(renderer, Mat4::IDENTITY, nullptr);
    }
}
```

Swap buffers (platform specific) - [ios method](https://github.com/cocos2d/cocos2d-x/blob/d07794052fed5c3edc29d4a60f99399d49271515/cocos/platform/ios/CCGLViewImpl-ios.mm#L210):

```c++
void GLViewImpl::swapBuffers()
{
    CCEAGLView *eaglview = (CCEAGLView*) _eaglview;
    [eaglview swapBuffers];
}
```

The **Director** class instantiates the objects used to perform scene updates:

* Scene: `Scene* _runningScene`
* Rendering: `Renderer _renderer`
* Graphics: `GLView* _openGLView`

**[GLView](https://github.com/cocos2d/cocos2d-x/blob/v3/cocos/platform/CCGLView.h#L100)** is an abstract class. Each platform contains a class **GLViewImpl** which inherits from **GLView** and defines the required behavior for that platform. For example, the [ios implementation](https://github.com/cocos2d/cocos2d-x/blob/d07794052fed5c3edc29d4a60f99399d49271515/cocos/platform/ios/CCGLViewImpl-ios.h#L41) must check for and accommodate the high pixel density of a retina display.

The GLView implementation is decided through a set of preprocessor directives.

**[Renderer](https://github.com/cocos2d/cocos2d-x/blob/v3/cocos/renderer/CCRenderer.h#L140)**
*  TODO


* **




## Game Objects:
