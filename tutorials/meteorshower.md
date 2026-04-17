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

## Welcome to Meteor Shower! ☄️ @showdialog

Buckle up — you're about to build **Meteor Shower**, a dodge game where rocks rain down from space and YOU have to get out of the way!

But here's the real mission today: you're going to learn two concepts that show up in **literally every program ever written** — **Sequencing** and **Loops**.

Let's launch! 🚀

## Understanding Sequencing @showhint

Here's something really important to know about computers — they are NOT smart. Not even a little bit! 🤖

A computer does EXACTLY what you tell it to do, in EXACTLY the order you write it. It reads your blocks from **top to bottom**, one at a time, like reading a book. It never skips ahead. It never guesses. It never changes the order.

This is called **Sequencing** — and it means the ORDER of your blocks matters a lot!

Think about making a peanut butter sandwich. You have to:
1. Get the bread 🍞
2. Open the peanut butter 🥜
3. Spread it on the bread

If you tried to spread peanut butter BEFORE getting the bread — you'd have a mess! Code works the same way. The order of your steps IS the program.

## Initialize Our Game 🚀

Look at the `|| loops: on start ||` block — it already has three blocks stacked inside it. The computer runs them **one by one from top to bottom**. That is sequencing happening right now!

~hint What does each block do?
- :paint brush: `|| scene: set background color to ||` — sets the background first, before anything else appears on screen
- :trophy: `|| info: set score to (0) ||` — resets the score so everyone starts at zero
- :heart: `|| info: set life to (3) ||` — gives every player 3 lives at the start of every game
hint~

Click the background color circle and pick a dark **space color** — black (color 15) or dark blue (color 1) for that deep space vibe! 🌌

```blocks
scene.setBackgroundColor(1)
info.setScore(0)
info.setLife(3)
```

## Create Your Hero! 🧑‍🚀

Time to create the brave hero who's going to dodge all those meteors!

- :plus: **Create the Sprite**: Add a `|| variables(sprites): set mySprite to ||` block after the lives block. Click **New Variable** and name it **hero**. Pick any character you like from the Gallery — they're about to have a very bad day! 😅
- :marker: **Set the Position**: Add a `|| sprites: set mySprite position to x (0) y (0) ||` block. Change **mySprite** to **hero** and set **x** to **80** and **y** to **105**.
- :game controller: **Enable Movement**: Add a `|| controller: move mySprite with buttons ||` block and change **mySprite** to **hero**.
- :lock: **Stay on Screen**: Add a `|| sprites: set mySprite stay in screen ||` block, change it to **hero**, and set it to **ON**.

~hint Why y = 105?
- :info: The game screen is 120 pixels tall. Setting y to **105** places the hero near the very bottom — so the rocks have a long way to fall before they reach the player! More falling distance = more time to react. Smart design! 🎯
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

## 🔢 Sensei Check — Sequencing! @showdialog

🎉 Hit play and move your hero around with the arrow keys — they're alive!

You just wrote your first **sequence** of blocks. The game set up the background, THEN the score, THEN the lives, THEN created the hero — all in order, step by step.

**Senseis — ask the class these questions before moving on:**

1. "Point to the block that runs FIRST in on-start. Now point to the one that runs LAST!"
2. "What would happen if I moved the `set life to 3` block to the BOTTOM — after the hero is created? Would anything look different?"
3. "Why does the computer run blocks top-to-bottom instead of all at once? What would go wrong if it ran them all at the same time?"

---
Click **Next** when your Sensei gives the signal! 🥷

## Introducing Loops @showhint

Okay, imagine your teacher asked you to write "I will not talk in class" on the board... **50 times.** 😩

You would NOT want to write the same sentence 50 separate times!

A **loop** is the solution. A loop lets you say: **"Do this action X times"** using just a FEW blocks instead of repeating the same blocks over and over and over.

In MakeCode we have a `|| loops: repeat (4) times ||` block — everything inside it runs that many times automatically!

Here's the wild part: you can even put a **sequence inside a loop**. The loop runs top-to-bottom, and inside EACH run, the sequence still runs top-to-bottom. It's like a sequence inside a sequence — **that's real programming power!** 💪

## Spawn a Wave of Rocks! 🪨

A function called `spawnRock` is already written in your template — it creates one falling rock. Now we'll use a **loop** to call it multiple times and create a whole WAVE!

- :repeat: **Add a Repeat Loop**: Inside the `|| game: on game update every (2000) ||` block, add a `|| loops: repeat (4) times ||` block. This is your loop!
- :function: **Call spawnRock**: Inside the repeat loop, add a `|| function: call spawnRock ||` block. The loop will call this 4 times — 4 rocks per wave!
- :clock: **Stagger the Rocks**: After the `call spawnRock` block (still INSIDE the loop), add a `|| loops: pause (500) ms ||` block. Now each rock appears a little after the previous one — a wave, not a wall!

~hint Why does the pause go INSIDE the loop?
- :info: Because the loop repeats **everything inside it** — including the pause! So after each rock spawns, the game waits 500ms before spawning the next one. This is **sequencing inside a loop** — the order of blocks inside a loop still matters, just like anywhere else!
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

## 🔁 Sensei Check — Loops! @showdialog

LOOK AT THOSE METEORS! Every 2 seconds a wave of 4 rocks rains down from space, one after another!

Think about what's happening right now:
1. The **loop** runs 4 times
2. Each run: it calls `spawnRock`, then waits 500ms
3. Then the **game update interval** waits 2 seconds and does it ALL over again

That is **sequencing inside a loop inside an event**. That is REAL programming! 🤯

**Senseis — ask the class:**

1. "How many rocks appear in each wave right now? Where is that number in the code — can you point to it?"
2. "What would happen if I changed the `repeat 4` to `repeat 10`? What about changing `pause 500` to `pause 100`?"
3. "Why is it better to use a loop than to just copy the `spawnRock` block 4 times? What if we wanted 100 rocks?"

---
Click **Next** when your Sensei gives the signal! 🥷

## Losing Lives 💥

Right now the rocks pass right through the hero — that's not scary at all! Let's fix that.

- :hazard: **Take a Life**: Inside the `|| sprites: on overlap ||` block (Player / Enemy), add a `|| info: change life by (-1) ||` block. Make sure the number is **-1** (negative one)!
- :boom: **Destroy the Rock**: Add a `|| sprites: destroy mySprite ||` block, change it to **otherSprite**, click **+**, and pick an explosion effect like **fire** or **warmRadial**.
- :camera: **Camera Shake** *(bonus!)*: Add a `|| scene: camera shake by (4) pixels for (500) ms ||` block — that IMPACT feeling! 💥

```blocks
//@collapsed
let hero: Sprite = null
sprites.onOverlap(SpriteKind.Player, SpriteKind.Enemy, function (sprite, otherSprite) {
    info.changeLifeBy(-1)
    otherSprite.destroy(effects.fire, 200)
    scene.cameraShake(4, 500)
})
```

## Score Points for Surviving! 🏆

Let's reward players for every wave they dodge!

- :trophy: **Score Per Wave**: Add a `|| info: change score by (1) ||` block inside the `|| game: on game update every ||` block, **AFTER** the repeat loop. Every finished wave = 1 point!

~hint Why does the score block go AFTER the loop and not inside it?
- :info: **Sequencing!** The computer finishes the ENTIRE loop first — all 4 rocks — THEN moves to the next block. If the score was INSIDE the loop, you'd score a point 4 times per wave instead of 1. The position of that block completely changes how the game works. That's sequencing in action! 🎯
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

And you learned two concepts that live inside **every single program ever written:**

- 🔢 **Sequencing** — Code runs top to bottom, in order, every time. Where you place a block changes everything your game does!
- 🔁 **Loops** — The `repeat` block lets you do something many times with just a few blocks. No copying. No pasting. Just loop it!
- 💡 **Sequencing inside Loops** — You can combine both ideas. Order still matters inside a loop — just like everywhere else!

You are thinking like a REAL programmer now. 🥷

**Challenge your Sensei:** Can you change the repeat count to make the waves even BIGGER? What happens if you change the pause time to 100ms? How small can you make the interval before it becomes impossible? 🪨
