# 2d-html-canvas documentation

## Description

A reliable engine for faster, straight forward building of 2d games using the html canvas.
Don't reinvet the wheel and Don't repeat yourself.
This documentaion is an overview of the entire project,
For more detailed documentation with examples visit.[2d-html-canvas game engine](http://www.codelordug.com/2d-html-canvas/docs).

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
function game(width = 512, height = 512, setup, assets, load) {

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
It has a default value of 512px

#### height

This is the desired height of the canvas in pixels.
It has a default value of 512px.

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
