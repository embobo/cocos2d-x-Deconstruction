# Time and Game Loop
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

![](https://github.com/embobo/cocos2d-x-Deconstruction/blob/master/images/init().png)
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

![](https://github.com/embobo/cocos2d-x-Deconstruction/blob/master/images/drawScene().png)
*Figure III: Director::drawScene() breakdown*

The director is ultimately responsible for moving from one [scene](https://github.com/cocos2d/cocos2d-x/blob/v3/cocos/2d/CCScene.h) to the next.
