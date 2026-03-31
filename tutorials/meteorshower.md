# Code Ninjas Evans GBS

### @diffs true

```template
scene.setBackgroundColor(1)
info.setScore(0)
info.setLife(3)

sprites.onOverlap(SpriteKind.Player, SpriteKind.Enemy, function (sprite, otherSprite) {

})

game.onUpdateInterval(2000, function () {

})

function spawnRock() {
    let rock = sprites.create(sprites.space.spaceAsteroid0, SpriteKind.Enemy)
    rock.setVelocity(0, 80)
    rock.setPosition(randint(10, 150), 0)
    rock.setFlag(SpriteFlag.AutoDestroy, true)
}
```

## Welcome to Code Ninjas Evans! 👋 @showdialog

Today you are building **Meteor Shower** — a dodge game where rocks fall from the sky in waves and you have to get out of the way!

Along the way you will learn two of the most important ideas in all of coding: **sequencing** and **loops**.

Ready? Let's go!

## Understanding Sequencing @showhint

Before we write a single block, let's talk about **sequencing**.

In coding, sequencing means that your blocks run **in order, from top to bottom**, one step at a time — just like reading a book.

The computer never skips ahead or goes backwards. It finishes each instruction before moving to the next one. The **order** you put your blocks in matters a lot!

## Initialize Our Game

Look at the `|| loops: on start ||` block. It already has three blocks inside it. Notice how they stack on top of each other — the computer runs them one by one from top to bottom. That is sequencing in action!

~hint What does each block do?

- :paint brush: `|| scene: set background color to ||` — sets the background before anything else appears
- :trophy: `|| info: set score to (0) ||` — resets the score so everyone starts at zero
- :heart: `|| info: set life to (3) ||` — gives the player 3 lives at the very start

hint~

Try clicking the background color circle and picking a dark **space color** like black or dark blue to set the mood!

```blocks
scene.setBackgroundColor(1)
info.setScore(0)
info.setLife(3)
```

## Create Your Hero

Time to create the character who will dodge all those falling rocks!

- :plus: **Create the Sprite**: Add a `|| variables(sprites): set mySprite to ||` block after the lives block. Click **New Variable** and name it **hero**. Pick any character you like from the Gallery!
- :marker: **Set the Position**: Add a `|| sprites: set mySprite position to x (0) y (0) ||` block. Change **mySprite** to **hero** and set **x** to **80** and **y** to **105**. This puts the hero near the bottom of the screen.
- :game controller: **Enable Movement**: Add a `|| controller: move mySprite with buttons ||` block. Change **mySprite** to **hero**.
- :lock: **Stay on Screen**: Add a `|| sprites: set mySprite stay in screen ||` block, change it to **hero**, and set it to **ON**.

~hint Why y = 105?

- :info: The game screen is 120 pixels tall. Setting y to 105 places the hero near the very bottom so the rocks have room to fall before they reach the player!

hint~

```blocks
scene.setBackgroundColor(1)
info.setScore(0)
info.setLife(3)
let hero: Sprite = null
hero = sprites.create(sprites.castle.heroWalkFront1, SpriteKind.Player)
hero.setPosition(80, 105)
controller.moveSprite(hero)
hero.setStayInScreen(true)
```

## Looking Good! @showdialog

🎉 Hit play and move your hero around with the arrow keys!

You just wrote your first **sequence** of blocks. Notice how the game sets up the background, then the score, then the lives, then creates the hero — all in order, step by step.

Now let's add the meteors. First, we need to talk about **loops**!

## Introducing Loops @showhint

Imagine your teacher asked you to write "I will not talk in class" on the board **50 times**. You would not want to write the same sentence 50 separate times!

A **loop** solves this. A loop lets you say: **"do this action X times"** using just a few blocks instead of repeating the same blocks over and over.

In MakeCode we have a `|| loops: repeat (4) times ||` block that does exactly that. Everything you put inside it will run the number of times you set!

## Spawn a Wave of Rocks! 🪨

A function called `spawnRock` is already written for you in the template. It creates one falling rock. Now we will use a **loop** to call it multiple times and create a whole wave!

- :repeat: **Add a Repeat Loop**: Inside the `|| game: on game update every (2000) ||` block, add a `|| loops: repeat (4) times ||` block.
- :function: **Call spawnRock**: Inside the repeat loop, add a `|| function: call spawnRock ||` block. This will create one rock each time the loop runs.
- :clock: **Stagger the Rocks**: After the `call spawnRock` block (still inside the loop), add a `|| loops: pause (500) ms ||` block. This makes each rock appear a little after the previous one instead of all at the same time!

~hint Why does the pause go inside the loop?

- :info: Because the loop repeats everything inside it, the **pause goes inside too**. That means after each rock spawns, the game waits 500ms before spawning the next one. This is sequencing inside a loop — order still matters even when you are looping!

hint~

```blocks
//@collapsed
function spawnRock() {
    let rock = sprites.create(sprites.space.spaceAsteroid0, SpriteKind.Enemy)
    rock.setVelocity(0, 80)
    rock.setPosition(randint(10, 150), 0)
    rock.setFlag(SpriteFlag.AutoDestroy, true)
}

game.onUpdateInterval(2000, function () {
    for (let i = 0; i < 4; i++) {
        spawnRock()
        pause(500)
    }
})
```

## Rocks Are Falling! @showdialog

Hit play! Every 2 seconds a wave of 4 rocks should fall from the sky, one after another.

Think about what is happening:
1. The **loop** runs 4 times
2. Each time it runs, it calls `spawnRock` then waits 500ms
3. Then the **game update interval** waits 2 seconds and does it all over again

That is **sequencing inside a loop inside an event**. That is real programming!

## Losing Lives

Right now the rocks pass right through the hero. Let's make them actually dangerous!

- :hazard: **Take a Life**: Inside the `|| sprites: on overlap ||` block (Player / Enemy), add a `|| info: change life by (-1) ||` block. Make sure the number is **-1**.
- :boom: **Destroy the Rock**: Add a `|| sprites: destroy mySprite ||` block, change it to **otherSprite**, click the **+** sign, and pick an explosion effect like **fire** or **warmRadial**.
- :camera: **Camera Shake** *(bonus!)*: Add a `|| scene: camera shake by (4) pixels for (500) ms ||` block to add some impact!

```blocks
//@collapsed
let hero: Sprite = null
sprites.onOverlap(SpriteKind.Player, SpriteKind.Enemy, function (sprite, otherSprite) {
    info.changeLifeBy(-1)
    otherSprite.destroy(effects.fire, 200)
    scene.cameraShake(4, 500)
})
```

## Add a Score

Let's reward players for every wave they survive!

- :trophy: **Score Per Wave**: Add a `|| info: change score by (1) ||` block inside the `|| game: on game update every ||` block, **after** the repeat loop. Every time a wave finishes, the score goes up by 1.

~hint Why does the score block go after the loop?

- :info: Because of sequencing! The computer finishes the entire loop first (all 4 rocks), then moves to the next block — which is your score. If you put the score block inside the loop, you would score a point 4 times per wave instead of 1!

hint~

```blocks
//@collapsed
function spawnRock() {
    let rock = sprites.create(sprites.space.spaceAsteroid0, SpriteKind.Enemy)
    rock.setVelocity(0, 80)
    rock.setPosition(randint(10, 150), 0)
    rock.setFlag(SpriteFlag.AutoDestroy, true)
}

game.onUpdateInterval(2000, function () {
    for (let i = 0; i < 4; i++) {
        spawnRock()
        pause(500)
    }
    info.changeScoreBy(1)
})
```

## You Did It! 🎉 @showdialog

🏆 **Congratulations — you just built Meteor Shower!** 🏆

Here is what you learned today:

- 🔢 **Sequencing** — Code runs top to bottom, in order. Where you place a block changes what your game does!
- 🔁 **Loops** — The `repeat` block lets you do something many times without copying the same blocks over and over.
- 💡 **Sequencing inside Loops** — You can combine both ideas. The order of blocks inside a loop still matters!

These two concepts are inside every program ever written. You are thinking like a real programmer now.

Challenge your Sensei: can you change the repeat count to make the waves bigger? What happens if you change the pause time? 🪨
