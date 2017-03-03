# Physics
=

Cocos2d comes integrated with a Physics library called [Chipmunk](http://chipmunk-physics.net/), which provides all of the Physics functionalities needed in complex game environment.

[![Chipmunk](images/chipmunk.png)](https://www.youtube.com/watch?v=z_Sx9N39KHk)

## Rigid Body Dynamics

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

## Continuous Collision Detection

**[Box2D](http://box2d.org/manual.pdf)** is another library that comes with Cocos and has a variety of functions that simulate 2D rigid body dynamics. This is a more advanced feature for users requiring high performance in physics from their games. 

Box2D supports **continuous collision detection**, which is not present in the built-in Chipmunk Physics engine. CCD is a technique used to prevent dynamic bodies from tunneling through static bodies. When tunneling occurs, a scenario like a bullet moving through a glass wall might simply appear as the bullet moving through the wall and reappearing on the other end, with no collision.
This is done by moving shapes in a sweeping motion from their old coordinates to their new coordinates. During the sweep, Box2D looks for collisions that will take place and computes the time of these collisions. At the (TOI) time of impact, the engine executes the collision response function for each body in contact.

## Collision Detection

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
