# Rocket documentation

## Description

A reliable engine for faster, straight forward building of 2d games using the html canvas.
Don't reinvet the wheel and Don't repeat yourself.
This documentaion is an overview of the entire project,
For more detailed documentation with examples visit.[Rocket game engine](http://www.codelordug.com/rocket/docs).

## Table of Contents

- [Table of Contents](#table-of-contents)
- [Examples](#examples)
- [Quick Start](#quick-start)
- [GameEngine Properties](#gameengine-properties)
- [GameEngine Methods](#gameengine-methods)
- [FAQ](#faq)
  - [Is Rocket Game Engine suitable for production quality games?](#is-rocket-game-engine-suitable-for-production-quality-games)
  - [Are there games built on this engine?](#Are-there-games-built-on-this-engine)
  - [How do I manage physics?](#how-do-i-manage-physics)
  - [How do I use the in built AI?](#How-do-I-use-the-in-built-AI)
  - [Is this compatible with Android and iOS?](#is-this-compatible-with-android-and-ios)
- [Introduction](#introduction)
- [The Game Loop](#the-game-loop)
- [The Game Loop vs Browser](#the-game-loop-vs-react-native)
- [Using the GameLoop Component](#using-the-gameloop-component)
- [Behind the Scenes](#behind-the-scenes)
- [Awesome Packages for Game Development](#awesome-packages-for-game-development)
- [Get in Touch](#get-in-touch)
- [Tools](#tools)
- [License](#license)
- [References](#references)

## Adding to a Project

### Using a CDN

You can add the link below to your html file where you want to run your game.

```html

<script src="coming soon" ></script>

```

and you are good to go!!!!.

### Via node

In your project directory run the following command

```js
npm install game-engines/2d

or for yarn 

yarn install game-engines/2d

```

That's all.
Now let's open the box and leverage the rich features of the engine.

## Usage

You don't have to be a javascript guru to
use the game engine. We assume you have some
basic knowledge about game terms such as

```html
Game assets
Sprites
Scene Graph
Interactivity
Collision detection
Animation
etc
```

### for web

After including the script in your web page
you will be able to interact with the 
engine via a global function game.
The game function takes the form

```js
function game(width, height, setup, assets, load) {

    return new Game(width, height, setup, assets, load);
}

```

The game function uses the given parameters to
 instatiate a game object and returns it
The returned object is the game!!!.

Some of the function parameters have default values
Lets look at all the parameters

#### width

This defines the width in pixels of the canvas
 your game will use.

#### height

This is the desired height of the canvas in pixels.

#### setup

The setup parameter is the callback that will be called immediately
after loading the game assets.

#### assets

This is an array of all the assets your
game is going to use.
Assets can be any of the following.

```txt
Note: Only the following formats are supported by default.
[Of course you can add your custom formats]

Images 
    [png, jpg, gif, jpeg, svg]

Fonts 
    [ttf, otf, ttc, woff]

Audio
    [mp3, ogg, wav, webm]

Json
```

#### load

This is an optional callback you can pass
that will run when the asset loader is loading
the game assets.

Now that we have the game object with all the
assets let's engine do the work.

## Core Classes

### The game object

This is returned by the game() function.
It gives a black-box interface to your game.
You can start, pause, continue, stop and do all
the operations on your game througth this object.
Let's dive into this object.

#### Properties

canvas
stage
scale
pointer
state
assets
paused

utilities
display
collision
interactive
sound
tween

#### Methods

load
setup
gameLoop
start
pause
resume

### Text extends GameObject

```js
constructor(
        content = "Hello!",
        x = 0,
        y = 0,
        font = "12px sans-serif",
        fillStyle = "red",
)
```

#### Properties

```js
this.textBaseline = "top";
this.strokeText = "none";
```

#### Methods

```js
render(ctx) {
        ctx.font = this.font;
        ctx.strokeStyle = this.strokeStyle;
        ctx.lineWidth = this.lineWidth;
        ctx.fillStyle = this.fillStyle;

        //Measure the width and height of the text
        if (this.width === 0) this.width = ctx.measureText(this.content).width;
        if (this.height === 0) this.height = ctx.measureText("M").width;
        ctx.translate(
            -this.width * this.pivotX,
            -this.height * this.pivotY
        );
        ctx.textBaseline = this.textBaseline;
        ctx.fillText(
            this.content,
            0,
            0
        );
        if (this.strokeText !== "none") ctx.strokeText();
    }
```

### Sprite extends GameObject

```js
constructor(
        source,
        x = 0,
        y = 0
 )
 ```

#### Methods

```js
createFromImage(source)
createFromAtlas(source)
createFromTileset(source)
createFromTilesetFrames(source)
createFromAtlasFrames(source)
createFromImages(source)
gotoAndStop(frameNumber)
render(ctx)
```

### Rectangle

This class extends the GameObject class

```js
    constructor(
        x = 0,
        y = 0,
        width = 32,
        height = 32,
        fillStyle = "gray",
        strokeStyle = "none",
        lineWidth = 0,
      
    )
```

#### Added Properties

```js
this.mask
```

#### Added Methods

```js
render(ctx)
```

### Line extends GameObject

```js
constructor(
        ax = 0,
        ay = 0,
        bx = 32,
        by = 32,
        lineWidth = 0,
        strokeStyle = "none",
)
```

#### Properties

```js
this.lineJoin = "round";
```

#### Methods

```js
render(ctx) {
        ctx.strokeStyle = this.strokeStyle;
        ctx.lineWidth = this.lineWidth;
        ctx.lineJoin = this.lineJoin;
        ctx.beginPath();
        ctx.moveTo(this.ax, this.ay);
        ctx.lineTo(this.bx, this.by);
        if (this.strokeStyle !== "none") ctx.stroke();
}
```

### Group extends GameObject

```js
constructor(...gameObjectsToGroup)
```

#### Methods

```js
addChild(gameObject)
removeChild(gameObject)
calculateSize() 
```

### GameObject

This is the base class of all
game objects. All the other objects, such as
circle, rectangle, stage, game scene and even
user defined classes should extend this class.

#### properties

```js
this.x = 0;
this.y = 0;
this.width = 0;
this.height = 0;
this.vx = 0;
this.vy = 0;
this.visible = true;
this.rotation = 0;
this.alpha = 1;
this.scaleX = 1;
this.scaleY = 1;
this.pivotX = 0.5;
this.pivotY = 0.5;
this._layer = 0;
this.parent = null;
this.children = [];
this.shadow = false;
this.shadowColor = "rgba(100, 100, 100, 0.5)";
this.shadowOffsetX = 3;
this.shadowOffsetY = 3;
this.shadowBlur = 3;
this.blendMode = null;
this.frames = [];
this.loop = true;
this._currentFrame = 0;
this.playing = false;
this._draggable = null;
this._circular = false;
this._interactive = false;
this.previousX = 0;
this.previousY = 0;
```

#### Getters and Setters

```js
gx
gy
layer
layer(val)
halfWidth
halfHeight
centerX
centerY
position
setPosition(x, y)
localBounds()
globalBounds
empty
currentFrame
circular
circular(value)
draggable
draggable(value)
interactive
interactive(value)
```

#### Methods

```js
addChild(gameObject)
removeChild(gameObject)
putCenter
putTop(b, xOffset = 0, yOffset = 0)
putRight(b, xOffset = 0, yOffset = 0)
putBottom(b, xOffset = 0, yOffset = 0)
putLeft(b, xOffset = 0, yOffset = 0)
swapChildren(child1, child2)
add(...spritesToAdd)
remove(...spritesToRemove)
```

### Circle extends GameObject

```js
constructor(
        x = 0,
        y = 0,
        diameter = 32,
        lineWidth = 0,
        fillStyle = "gray",
        strokeStyle = "none"
      
    )
```

#### Properties

```js
this.circular = true;
this.mask = false;

```

#### Methods

```js
render(ctx) {
        ctx.strokeStyle = this.strokeStyle;
        ctx.lineWidth = this.lineWidth;
        ctx.fillStyle = this.fillStyle;
        ctx.beginPath();
        ctx.arc(
            this.radius + (-this.diameter * this.pivotX),
            this.radius + (-this.diameter * this.pivotY),
            this.radius,
            0, 2 * Math.PI,
            false
        );
        if (this.strokeStyle !== "none") ctx.stroke();
        if (this.fillStyle !== "none") ctx.fill();
        if (this.mask && this.mask === true) ctx.clip();
}
```
