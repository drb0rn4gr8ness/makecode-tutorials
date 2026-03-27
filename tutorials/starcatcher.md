# Code Ninjas Evans GBS

### @diffs true

```template
scene.setBackgroundColor(1)
info.setScore(0)
info.setLife(3)

sprites.onOverlap(SpriteKind.Player, SpriteKind.Food, function (sprite, otherSprite) {

})

sprites.onOverlap(SpriteKind.Player, SpriteKind.Enemy, function (sprite, otherSprite) {

})

game.onUpdateInterval(1500, function () {

})
```

## Welcome to Code Ninjas Evans! 👋 @showdialog

Get ready to build **Star Catcher** — a game where your ninja moves left and right to catch falling stars while dodging dangerous bombs!

By the end of today you will have built a real, playable game completely with code. Let's go!

## Initializing Our Game

~hint What does initializing mean?

- :book: Initializing just means **"setting things up before the game begins."** We want our game to always start the same way — same background, same score, same number of lives — so every player gets a fair start!

hint~

Your template already has some setup code inside the `|| loops: on start ||` block. Let's look at what each piece does and make it our own!

- :paint brush: **Background Color**: The `|| scene: set background color to ||` block sets the background. Click the colored circle and try a dark color like **black** or **navy blue** to make the stars pop!
- :trophy: **Score**: The `|| info: set score to (0) ||` block makes sure everyone starts at zero points.
- :heart: **Lives**: The `|| info: set life to (3) ||` block gives every player 3 chances before the game ends.

```blocks
scene.setBackgroundColor(1)
info.setScore(0)
info.setLife(3)
```

## Create Your Ninja! 🥷

Time to create the star of the show — your player sprite!

~hint What is a sprite?

- :info: A **sprite** is any image that can move around on the screen. Our ninja, the stars, and the bombs are all sprites!

hint~

- :plus: **Create the Sprite**: Add a `|| variables(sprites): set mySprite to ||` block inside `|| loops: on start ||`. Click **New Variable** and name it **ninja**. Pick a character image from the Gallery — any person or creature you like!
- :marker: **Set the Position**: Add a `|| sprites: set mySprite position to x (0) y (0) ||` block. Change **mySprite** to **ninja** and set **x** to **80** and **y** to **100** so the ninja starts near the bottom of the screen.
- :game controller: **Enable Movement**: Add a `|| controller: move mySprite with buttons ||` block and change **mySprite** to **ninja**. This lets the player control the ninja with the arrow keys!
- :lock: **Stay on Screen**: Add a `|| sprites: set mySprite stay in screen ||` block, change it to **ninja**, and make sure it says **ON**. This keeps your ninja from running off the edge!

```blocks
scene.setBackgroundColor(1)
info.setScore(0)
info.setLife(3)
let ninja: Sprite = null
ninja = sprites.create(sprites.castle.heroWalkFront1, SpriteKind.Player)
ninja.setPosition(80, 100)
controller.moveSprite(ninja)
ninja.setStayInScreen(true)
```

## You Did It! 🔥 @showdialog

🎉 Your ninja is on the screen and moving around!

Hit the play button and try moving with the arrow keys. Pretty cool, right?

Let your Sensei know how you're feeling before we move on to the next big topic: **Events!**

## Introducing Events @showhint

Up next we are going to write code inside **event blocks**.

An event block **listens** for something specific to happen in the game. When that thing happens, the code inside the event block runs automatically.

Think of it like a smoke detector — it just sits there doing nothing until it detects smoke, and then it springs into action! 🔥

## On Game Update Event @showhint

We will use the `|| game: on game update every <Interval> ||` event to make things happen on a timer.

This block waits for the time inside it to pass and then runs your code. It keeps repeating forever as long as the game is running.

~hint What does 1500 mean?

- :info: Time in code is often measured in **milliseconds**. There are 1000 milliseconds in one second. So 1500 milliseconds = 1.5 seconds. Every 1.5 seconds our code will run!

hint~

## Make Stars Fall! ⭐

Let's make stars rain down from the sky for our ninja to catch. We will add code inside the `|| game: on game update every <Interval> ||` block.

- :star: **Create a Star**: Add a `|| variables(sprites): set mySprite to ||` block inside the update event. Create a **New Variable** called **star** and pick a star, coin, or food image from the Gallery.
- :move: **Give it a Speed**: Add a `|| sprites: set mySprite velocity to vx (0) vy (0) ||` block. Change **mySprite** to **star** and set **vy** to **60**. This makes the star fall straight down!
- :pin: **Random Start Position**: Add a `|| sprites: set mySprite position to x (0) y (0) ||` block. Set **y** to **0** (top of the screen) and wrap the **x** value with a `|| math: pick random (0) to (160) ||` block so stars appear in different places each time.
- :ghost: **Auto Destroy**: Add a `|| sprites: set mySprite flag ||` block and turn on **Auto Destroy**. This cleans up stars that the ninja misses so the game doesn't slow down.
- :label: **Set the Kind**: Add a `|| sprites: set mySprite kind to ||` block, change the sprite to **star**, and set the kind to **Food**.

~hint Why do we use the Food kind?

- :info: MakeCode uses "kinds" as labels so we can tell sprites apart. We use **Food** for things the player wants to collect. Later we will use **Enemy** for things the player wants to avoid!

hint~

```blocks
//@collapsed
let ninja: Sprite = null
game.onUpdateInterval(1500, function () {
    let star = sprites.create(sprites.projectile.star1, SpriteKind.Food)
    star.setVelocity(0, 60)
    star.setPosition(randint(0, 160), 0)
    star.setFlag(SpriteFlag.AutoDestroy, true)
})
```

## Catch the Stars! 🌟

Stars are falling but nothing happens when the ninja touches them yet. Let's fix that with an **overlap event**!

- :trophy: **Add a Point**: Inside the `|| sprites: on overlap ||` block that already says **Player** and **Food**, add a `|| info: change score by (1) ||` block to give the player a point.
- :sparkles: **Add an Effect**: Add a `|| sprites: destroy mySprite ||` block, change it to **otherSprite**, click the **+** sign, and pick a fun effect like **confetti** or **spray**. This destroys the star when it's caught!
- :music: **Play a Sound**: Add a `|| music: play sound ||` block and choose a happy sound like **power up** or **jump**.

```blocks
//@collapsed
let ninja: Sprite = null
sprites.onOverlap(SpriteKind.Player, SpriteKind.Food, function (sprite, otherSprite) {
    info.changeScoreBy(1)
    otherSprite.destroy(effects.confetti, 200)
    music.play(music.melodyPlayable(music.powerUp), music.PlaybackMode.InBackground)
})
```

## Excellent Work! @showdialog

🎉 Hit play and try catching some stars!

You just used an **overlap event** — one of the most important tools in game programming. Whenever two sprites touch, your code runs automatically.

Now let's make the game harder and more exciting with **conditionals**!

## Introducing Conditionals @showhint

A **conditional** lets your code make a decision.

It works like this: **"IF something is true, THEN do this... otherwise do that."**

You use conditionals in real life all the time! For example:

- **IF** it is raining, **THEN** bring an umbrella ☔
- **IF** you are hungry, **THEN** eat a snack 🍎

In our game, we want to randomly drop a **bomb** instead of a star sometimes. We will use a conditional to make that decision!

## Add Falling Bombs! 💣

Let's update our update interval to sometimes spawn a bomb instead of a star.

- :shuffle: **Add a Random Check**: At the very **top** of your `|| game: on game update every ||` block, add an `|| logic: if <true> then / else ||` block. This creates two paths — one for stars and one for bombs.
- :game die: **Add Randomness**: Replace the **true** condition with a `|| logic: (0) < (0) ||` block. On the left side put a `|| math: pick random (1) to (10) ||` block. On the right side put the number **3**. This means there is a **3 in 10 chance** a bomb will spawn!
- :bomb: Move your existing star code into the **else** section (the bottom half). In the **if** section (the top half), create a new sprite variable called **bomb**, pick a scary-looking image from the Gallery, give it the same falling speed and random position, turn on Auto Destroy, and set the **Kind** to **Enemy**.

~hint Help! I'm confused about where to put the code.

- :info: The **if** section runs when the random number is 3 or less → a **bomb** appears.
- The **else** section runs the rest of the time → a **star** appears.
- So most of the time the player sees stars, but occasionally a bomb sneaks in!

hint~

```blocks
//@collapsed
let ninja: Sprite = null
game.onUpdateInterval(1500, function () {
    if (randint(1, 10) <= 3) {
        let bomb = sprites.create(sprites.projectile.explosion1, SpriteKind.Enemy)
        bomb.setVelocity(0, 80)
        bomb.setPosition(randint(0, 160), 0)
        bomb.setFlag(SpriteFlag.AutoDestroy, true)
    } else {
        let star = sprites.create(sprites.projectile.star1, SpriteKind.Food)
        star.setVelocity(0, 60)
        star.setPosition(randint(0, 160), 0)
        star.setFlag(SpriteFlag.AutoDestroy, true)
    }
})
```

## Lose a Life on Bomb! 💥

Now we need to make the bombs actually do damage. We will use the other overlap event that is already in your template.

- :hazard: **Take Away a Life**: Inside the `|| sprites: on overlap ||` block that says **Player** and **Enemy**, add a `|| info: change life by (-1) ||` block. Make sure the number is **-1** (negative one)!
- :boom: **Destroy the Bomb**: Add a `|| sprites: destroy mySprite ||` block, change it to **otherSprite**, click **+**, and pick an explosion effect.
- :camera shake: **Camera Shake** _(bonus!)_: Add a `|| scene: camera shake by (4) pixels for (500) ms ||` block to make it feel like an impact!

```blocks
//@collapsed
let ninja: Sprite = null
sprites.onOverlap(SpriteKind.Player, SpriteKind.Enemy, function (sprite, otherSprite) {
    info.changeLifeBy(-1)
    otherSprite.destroy(effects.fire, 200)
    scene.cameraShake(4, 500)
})
```

## You Did It! 🎉 @showdialog

🏆 **Congratulations — you just built Star Catcher!** 🏆

Here is a quick recap of everything you learned today:

- ⭐ **Variables** — We used them to store our sprites, score, and lives
- 🔔 **Events** — We used overlap events and a timer event to make the game react
- 🤔 **Conditionals** — We used an if/else block to randomly decide between stars and bombs

That is the foundation of almost every game ever made. You should be super proud!

Find a Sensei and show off your high score. Can anyone in the room beat it? 🥷
