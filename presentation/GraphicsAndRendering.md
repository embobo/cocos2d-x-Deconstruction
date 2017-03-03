# Graphics and Rendering

Rendering the next scene makes calls to OpenGL. In addition to the `_openGLView` object used by the **Director** class, Cocos calls OpenGL static methods. These methods are prefixed with 'gl'- for example `glClearColor()`. In total, rendering of the `_runningScene` is handled by two core classes, the **GLView** class, and **Renderer** class. Below is a brief overview of these classes:

**[GLView](https://github.com/cocos2d/cocos2d-x/blob/v3/cocos/platform/CCGLView.h#L100):**

**GLView** is an abstract class that is inherited by the **GLViewImpl** class in each platform with behaviors specific to that platform. An example of platform dependent graphics might be the need to check for and accommodate the high pixel density of a retina display on an ios device.

```c++
virtual bool isRetinaDisplay() const override { return getContentScaleFactor() == 2.0; }
```

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

## Next: [Finito](https://github.com/embobo/cocos2d-x-Deconstruction/blob/master/presentation/STARTHERE.md)
