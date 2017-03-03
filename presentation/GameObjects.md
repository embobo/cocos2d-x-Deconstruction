# Game Objects
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

![](images/NodesVsSprites.png)

The [**Sprite**](https://github.com/cocos2d/cocos2d-x/blob/d07794052fed5c3edc29d4a60f99399d49271515/cocos/2d/CCSprite.h#L95) class is another inheritor of the **Node** class. Important to this class is it's **Texture** member which contains a 2D image used by the sprite object. This class is also limited to containing only other **Sprite** children.

##### Creating a Sprite:

```c++
// Create sprite from image directly in constructor:
auto aSprite = Sprite::create("aSprite.png");
```

##### Changing a Sprite Image:

```c++
// Change image on sprite:
aSprite->setTexture("aDifferentSprite.png");
```

##### Manipulating Sprite Placement:

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
