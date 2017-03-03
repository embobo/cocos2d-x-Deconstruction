# Component Overview
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
|**Scripting** | - | - | Supports lua & java | **<font color='red'>no</font>** |

Next: [Time and GameLoop](https://github.com/embobo/cocos2d-x-Deconstruction/blob/master/presentation/TimeAndGameLoop.md)
