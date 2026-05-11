# Code Ninjas Evans GBS

### @diffs true

```template
scene.setBackgroundColor(1)

sprites.onOverlap(SpriteKind.Player, SpriteKind.Food, function (sprite, otherSprite) {

})

sprites.onOverlap(SpriteKind.Player, SpriteKind.Enemy, function (sprite, otherSprite) {

})

sprites.onOverlap(SpriteKind.Player, SpriteKind.Projectile, function (sprite, otherSprite) {

})

game.onUpdateInterval(1500, function () {

})
```

## Welcome to Groovy Star! 🌟 @showdialog

Get ready to build **Groovy Star** — a game where YOUR star grooves across the screen catching musical notes and dodging bad vibes before the clock runs out!

But here's the twist — today isn't just about building a game. Today you're going to learn **6 real programming concepts** that actual game developers use every single day.

Let's GO! 🎶

## Initialize Our Groovy Game! 🎵

Time to set the stage! **Initializing** means telling the computer how to set everything up before the fun begins — the same way every single time so every player gets a fair start.

~hint What does initializing mean?
- :book: Initializing just means **"telling the computer what to remember before the game starts."** Score always begins at zero, lives always start at 3, and the timer always counts from 60 — every single time!
hint~

Let's add four blocks inside `|| loops: on start ||`:
- :paint brush: **Background Color**: Click the colored circle in the `|| scene: set background color to ||` block. Pick something bold — try **purple** or **dark blue** for that concert stage vibe! 🎤
- :trophy: **Score**: Add an `|| info: set score to (0) ||` block. Every player starts at zero — fair game, fair game!
- :heart: **Lives**: Add an `|| info: set life to (3) ||` block. Every player gets 3 chances before it's game over.
- :marker: **Countdown**: Add an `|| info: start countdown (60) ||` block. Hit play right now — a 60-second timer appears automatically! Your game is already ALIVE! ⏱️

```blocks
scene.setBackgroundColor(9)
info.setScore(0)
info.setLife(3)
info.startCountdown(60)
```

## What is a Variable? 🧠

Here's something **WILD** about computers — they DO have memory, but they won't USE it unless YOU tell them to! 🤯

When you wake up in the morning, you automatically remember your name, your age, your favorite food. You don't have to do anything — your brain just knows!

Computers? **They have a giant brain ready to remember things, but it stays empty until YOU give it instructions.** No instructions? The memory just sits there, unused!

That's where **variables** come in! A variable is how YOU flip the switch and tell the computer to actually USE its memory. Let's hand it something to remember!

- :star: **Make the Variable**: Click the **Variables** category in the toolbox, then hit **Make a Variable...** and name it **noteSpeed**. You just told the computer to set aside a memory slot with that name!
- :move: **Set Its Value**: Drag a `|| variables: set noteSpeed to (0) ||` block into the BOTTOM of `|| loops: on start ||`. Change the **0** to **80**. THAT'S you handing the computer a value to remember!

~hint Why use a variable instead of just typing 80 wherever we need it?
- :book: Because NOW if we want to change the speed, we only change the number in ONE place — the variable — and everywhere that uses it automatically updates! That's the POWER of variables. One change, instant effect everywhere. 💡
hint~

You just stored the number 80 with the name `noteSpeed`. **In the next step, you'll use that memory for the very first time!** 🧠

```blocks
scene.setBackgroundColor(9)
info.setScore(0)
info.setLife(3)
info.startCountdown(60)
let noteSpeed = 80
```

## Create Your Groovy Star! ⭐

Time to bring YOUR star to life! This is the most exciting moment — the second you add this code, your character appears on screen!

~hint What is a sprite?
- :info: A **sprite** is any image that can move around on the screen. Your star, the falling notes, the bad vibes — they're all sprites! Think of them like actors on a stage.
hint~

Here's how we build YOUR star — four blocks, in this order:
- :plus: **Create the Sprite**: Add a `|| variables(sprites): set mySprite to ||` block inside `|| loops: on start ||`. Click **New Variable** and name it **star**. Pick a star, shimmer, or gem image from the Gallery — something that screams GROOVY!
- :pin: **Set the Position**: Add a `|| sprites: set mySprite position to x (0) y (0) ||` block. Change **mySprite** to **star**, set **x** to **80** and **y** to **100** so your star starts near the bottom of the stage!
- :game controller: **Enable Movement**: Add a `|| controller: move mySprite with buttons vx (100) vy (100) ||` block. Change **mySprite** to **star**, drag your `|| variables: noteSpeed ||` block on top of **vx** to use the variable you just made, and set **vy** to **0**. Left and right ONLY — we're staying on the dance floor!
- :lock: **Stay on Stage**: Add a `|| sprites: set mySprite stay in screen ||` block, change it to **star**, and flip it to **ON**. No flying off the edge!

```blocks
scene.setBackgroundColor(9)
info.setScore(0)
info.setLife(3)
info.startCountdown(60)
let noteSpeed = 80
let star: Sprite = null
star = sprites.create(sprites.effects.star1, SpriteKind.Player)
star.setPosition(80, 100)
controller.moveSprite(star, noteSpeed, 0)
star.setStayInScreen(true)
```

## 🎉 Sensei Check — Variables! @showdialog

BOOM! Your star is on screen and moving around! Hit play and try it out — you earned this! ⭐

**Senseis — ask the class these questions before moving on:**

1. "Does the computer just KNOW how fast the star should move on its own? What did we have to do to give it that information?"
2. "Which line of code tells the computer to remember the star's speed? Can everyone point to it?"
3. "Thumbs UP if you think changing `noteSpeed` to 200 makes the star move FASTER — thumbs DOWN if you think slower!"

---
Click **Next** when your Sensei gives the signal! 🥷

## What is an Event? @showhint

Imagine you have a bodyguard who **NEVER sleeps** and **NEVER blinks.** 👀

Their only job is to watch for one specific thing. The moment it happens — **BAM** — they spring into action!

That's exactly what an **event block** does. You don't press a button. You don't call it. **It calls itself!**

We already have a few event guards set up in your template:
- The `|| game: on game update every (1500) ms ||` block — yes, **a timer counts as an event too!** It fires automatically every 1.5 seconds.
- One overlap event watching for **Player + Food** (your star + a note)
- One overlap event watching for **Player + Enemy** (your star + a bad vibe)

Let's start putting them to work! 🔥

## Make Musical Notes Fall! 🎵

Time to fill the sky with music! We're going to add code inside the `|| game: on game update every (1500) ms ||` block — that's the **timer event** you just learned about! It fires automatically every 1.5 seconds.

~hint What does 1500 mean?
- :info: Time in code is measured in **milliseconds**. 1000 milliseconds = 1 second. So 1500 milliseconds = 1.5 seconds. Every 1.5 seconds, a new note drops from the sky! 🎵
hint~

Add these steps INSIDE the `|| game: on game update every ||` block — in this exact ORDER:
- :plus: **Create a Note**: Add a `|| variables(sprites): set mySprite to ||` block. Create a **New Variable** called **note**. Pick a musical note, gem, or coin image — something fun to collect!
- :marker: **Set the Kind**: Make sure the kind is set to **Food**. This tells the game "this is something the player wants to catch!"
- :move: **Give it Speed**: Add a `|| sprites: set mySprite velocity to vx (0) vy (0) ||` block. Change **mySprite** to **note**, keep **vx** at **0**, and set **vy** to `noteSpeed`. Watch — we're using that variable AGAIN! 🎯
- :pin: **Random Start Position**: Add a `|| sprites: set mySprite position to x (0) y (0) ||` block. Set **y** to **0** (top of the screen). Wrap **x** with a `|| math: pick random (0) to (160) ||` block. **Random** means a different number every time — so notes fall from a different spot at every drop. Surprise!
- :trash: **Auto Destroy**: Add a `|| sprites: set mySprite flag ||` block and turn on **Auto Destroy**. This cleans up any notes that fall past the bottom so your game stays fast!

~hint Why do we need Auto Destroy?
- :info: Without it, every note the star misses keeps living INVISIBLY below the screen — still taking up memory! Auto Destroy is like a cleanup crew that removes them the moment they go offscreen. 🧹
hint~

```blocks
let note: Sprite = null
game.onUpdateInterval(1500, function () {
    note = sprites.create(sprites.food.smallBurger, SpriteKind.Food)
    note.setVelocity(0, noteSpeed)
    note.setPosition(randint(0, 160), 0)
    note.setFlag(SpriteFlag.AutoDestroy, true)
})
```

## 🔔 Sensei Check — Events! @showdialog

LOOK AT THOSE NOTES FALL! Your game is coming alive! 🎶

**Senseis — ask the class:**

1. "Did you have to PRESS anything to make those notes fall? What's making them fall every 1.5 seconds?"
2. "What KIND of event is the on-game-update-every block — is it a button event? A timer event? Something else?"
3. "What's the difference between `on start` (runs once) and `on game update every` (runs over and over)?"

---
Click **Next** when your Sensei gives the signal! 🥷

## Understanding Sequencing @showhint

Quick question — do you put your shoes on BEFORE your socks? 😬

**Of course not!** Order matters!

In programming, this is called **Sequencing** — the computer reads your code from top to bottom, one step at a time, in **EXACTLY** the order you wrote them.

It never skips ahead. It never goes backwards. **Top. To. Bottom. Every. Single. Time.**

Look back inside your `on game update every` block — the computer does every single line in order, starting from the very top. Create the note FIRST, set its speed NEXT, set its position AFTER that. Swap any two lines and the game can break! The computer just follows your instructions, in order, no questions asked!

## Catch the Notes! 🌟

Let's make something AMAZING happen the moment your star catches a note! Add all of this inside the `|| sprites: on overlap ||` block that says **Player** and **Food**.

- :trophy: **Earn a Point**: Add a `|| info: change score by (1) ||` block. One note = one point!
- :trash: **Confetti Explosion**: Add a `|| sprites: destroy mySprite with effect ||` block. Change **mySprite** to **otherSprite**, click the **+** sign, and pick **confetti** or **rings**. BOOM — the note EXPLODES when caught! 🎊

~hint Who calls the overlap event? How does it know to run?
- :book: YOU never call it — MakeCode watches every single frame. The moment the star sprite and a note sprite overlap even one pixel? MakeCode fires that event block automatically. That's what makes it an **event** — something from the outside triggers it!
hint~

```blocks
sprites.onOverlap(SpriteKind.Player, SpriteKind.Food, function (sprite, otherSprite) {
    info.changeScoreBy(1)
    otherSprite.destroy(effects.confetti, 200)
})
```

## 🔢 Sensei Check — Sequencing! @showdialog

YOUR STAR IS CATCHING NOTES! Hit play and go catch everything you can! 🎯

**Senseis — ask the class:**

1. "Point to the block that runs FIRST inside the overlap event. Now point to the one that runs LAST!"
2. "If I moved the destroy effect line BEFORE the score change line — would the game look different to you? Would the points still count?"
3. "What's the rule? The computer reads code from TOP to BOTTOM — every single time?"

---
Click **Next** when your Sensei gives the signal! 🥷

## What is a Conditional? @showhint

You just locked in **sequencing** — code marches straight down the page, top to bottom, line by line. 📜

But what if we want the code to take a **DETOUR**? That's called **BRANCHING** 🌿 — leaving the main path to do something different. And the trick that creates a branch? **Asking a question.**

But not just any question! _"What's your favorite pizza topping?"_ won't cut it — way too many answers! 🍕 We need a question with only **TWO** possible answers: ✅ **YES** or ❌ **NO**.

Programmers have a fancy word for those YES/NO answers — a **BOOLEAN** 🤖. Think of it like a light switch 💡 — it's either **ON (yes / true)** or **OFF (no / false)**. Never in between. Booleans are the SECRET WEAPON of every computer — only two answers, but you can build EVERYTHING out of them!

Picture your code as a video-game character speed-running a track. Suddenly the track SPLITS! A glowing sign blocks the way, demanding a boolean answer:

_"Is there a dragon ahead?"_ 🐲
- **YES (true)** → take the LEFT branch and HIDE!
- **NO (false)** → keep BLASTING straight ahead! 💨

Your character can only take ONE branch. Never both. Never neither.

This whole setup — the question, the boolean answer, the branching — is called a **conditional**. In our game, we'll ask the computer: _"Should we drop a BAD VIBE this time?"_ — and the boolean answer picks which branch runs!

## Add Bad Vibes! 😤

Let's make the game TRICKY! Update the inside of your `|| game: on game update every ||` block — we're wrapping everything in a decision!

- :shuffle: **Add an If/Else**: At the very TOP of the update block, add an `|| logic: if <true> then / else ||` block. This creates TWO paths — one for bad vibes and one for notes.
- :game die: **Make it Random**: Replace the **true** condition with a `|| logic: (0) < (0) ||` comparison. On the LEFT put a `|| math: pick random (1) to (10) ||` block. On the RIGHT put **3**. This means a bad vibe appears about 30% of the time!
- :bomb: **Create the Bad Vibe**: In the **if** section (when the random number is 3 or less), add a new sprite variable called **badVibe**. Pick a spiky, scary, or glitchy image. Set kind to **Enemy**, same `noteSpeed` for velocity, same random x position, Auto Destroy ON.
- :move: **Move the Note Code**: Move your existing note code into the **else** section (it runs the OTHER 70% of the time).

~hint I'm confused about the if vs. else sections!
- :info: The **IF** section runs when the dice roll lands on 1, 2, or 3 — that's 3 out of 10. **BAD VIBE drops!**
- The **ELSE** section runs all other times — 4, 5, 6, 7, 8, 9, or 10. **NOTE drops!**
- So most of the time you see notes, but every so often — surprise! Bad vibe incoming! 💀
hint~

```blocks
let badVibe: Sprite = null
let note: Sprite = null
game.onUpdateInterval(1500, function () {
    if (randint(1, 10) <= 3) {
        badVibe = sprites.create(sprites.projectile.explosion1, SpriteKind.Enemy)
        badVibe.setVelocity(0, noteSpeed)
        badVibe.setPosition(randint(0, 160), 0)
        badVibe.setFlag(SpriteFlag.AutoDestroy, true)
    } else {
        note = sprites.create(sprites.food.smallBurger, SpriteKind.Food)
        note.setVelocity(0, noteSpeed)
        note.setPosition(randint(0, 160), 0)
        note.setFlag(SpriteFlag.AutoDestroy, true)
    }
})
```

## Lose a Life on Bad Vibe! 💥

Now let's make those bad vibes actually DANGEROUS! Add this inside the `|| sprites: on overlap ||` block that says **Player** and **Enemy**.

- :heart: **Take Away a Life**: Add a `|| info: change life by (-1) ||` block. Make sure the number is **negative one** (-1)!
- :trash: **Destroy the Bad Vibe**: Add a `|| sprites: destroy mySprite with effect ||` block. Change to **otherSprite**, click **+**, and pick a fire or explosion effect.
- :camera shake: **CAMERA SHAKE** _(bonus!)_: Add a `|| scene: camera shake by (4) pixels for (500) ms ||` block — makes it feel like a real IMPACT! 📷💥

```blocks
let noteSpeed: number = 80
sprites.onOverlap(SpriteKind.Player, SpriteKind.Enemy, function (sprite, otherSprite) {
    info.changeLifeBy(-1)
    otherSprite.destroy(effects.fire, 200)
    scene.cameraShake(4, 500)
})
```

## 🤔 Sensei Check — Conditionals! @showdialog

Your game has DANGER now! Dodge those bad vibes! 😤

**Senseis — ask the class:**

1. "`randint(1, 10) <= 3` — how many numbers out of 10 make a bad vibe drop? Count them out loud!"
2. "What number would you change to make bad vibes appear MORE often? What about LESS often?"
3. "What does the ELSE branch do? Shout it out — when does ELSE run?"

---
Click **Next** when your Sensei gives the signal! 🥷

## Variables Are ALIVE! 🔥 @showhint

Okay — here's where things get **REALLY cool.** 🔥

Remember how we told the computer to remember `noteSpeed`? We said: _"Computer, remember the number 80!"_

Well guess what — **we can CHANGE that memory while the game is running!**

Every time you catch 5 notes, we're going to make `noteSpeed` go UP by 10. The computer doesn't just remember a number — it **updates its own memory in real time!**

Your variable is ALIVE. And your game is about to get wild. 🌀

## Crank Up the Speed! ⚡

Let's make the game get HARDER as you score! We're adding one more thing inside your **Player + Food overlap event** — right after `change score by 1`.

We need a way to ask the computer: _"Did the score just hit a multiple of 5?"_ The trick is **mod** — a fancy word for "divide and look at the remainder." When the score divides evenly by 5 (0, 5, 10, 15, 20...), the remainder is **0** — and that's our signal to speed things up!

- :shuffle: **Add a Speed Check**: Add an `|| logic: if <true> then ||` block right after the score change.
- :game die: **Check Every 5 Points**: Replace **true** with a `|| logic: (0) = (0) ||` block. On the left, add `|| info: score ||`. Wrap it with `|| math: (0) mod (0) ||` and set the right side to **5**. Set the right side of the equals to **0**.
- :move: **Increase the Speed**: Inside the if block, add a `|| variables: change noteSpeed by (10) ||` block. Every 5 catches — SPEED UP!

~hint Want a real-world picture of mod?
- :book: Think of mod as a speedometer that clicks every 5 points. **Score 5? Click. Score 10? Click. Score 15? Click.** Each click = the remainder hits 0 = the speed goes up by 10! 🏎️
hint~

Hit play and catch 5 notes — feel that speed jump? **Your variable just changed itself!** That's the magic of storing information in memory — you can read it AND change it whenever you want!

```blocks
let noteSpeed: number = 80
sprites.onOverlap(SpriteKind.Player, SpriteKind.Food, function (sprite, otherSprite) {
    info.changeScoreBy(1)
    otherSprite.destroy(effects.confetti, 200)
    if (info.score() % 5 == 0) {
        noteSpeed += 10
    }
})
```

## Add a POWER-UP! 🌟

We're adding something EXTRA. Something SPECIAL. Something GROOVY. 🌟

A **POWER-UP** is going to fall from the sky — a groovy lightning bolt! If you catch it?

- **+3 points** — BIG score boost!
- A wild **starField light show** 🌠

We're using the SAME event system you already know — but now it's watching for a THIRD kind of sprite!

## Wire Up the Power-Up! ⚡

We're stacking THREE possibilities now — a power-up, a bad vibe, OR a note. To pick one, we'll use **`if` / `else if` / `else`**: the computer checks them top-to-bottom and takes the **FIRST** branch that's true. Same branching idea as before — but now the track splits into THREE branches instead of two! 🌿

**Step 1 — Add to the Spawner:**

Go back inside your `|| game: on game update every ||` block and add click the **`+`** in the existing **`if` / `else`** block to add an **`else if`** block. Move your badVibe code into the **`else if`** block. Now add a new check in the **`if`** block. This one checks `randint(1, 10) = 1` — a 10% chance!

Inside that new if block:
- :plus: Create a new sprite variable called **powerUp**. Pick a lightning bolt, star, or glowing gem from the Gallery.
- :marker: Set the kind to **Projectile**
- :move: Give it the same `noteSpeed` velocity and random x position
- :trash: Auto Destroy ON

**Step 2 — Wire the Overlap Event:**

Inside the `|| sprites: on overlap ||` block that says **Player** and **Projectile**, add:
- :trophy: `|| info: change score by (3) ||` — triple points! 💰
- :trash: `|| sprites: destroy otherSprite with effect (starField) ||` — LIGHT SHOW! 🌠
- :music: `|| music: play sound (power up) ||`
- :camera shake: `|| scene: camera shake by (2) pixels for (500) ms ||`

~hint Why do we use Projectile kind for the power-up?
- :info: MakeCode has built-in kinds: Player, Food, Enemy, Projectile. We already used Player, Food, and Enemy — so Projectile is the perfect slot for our power-up! The kind is just a label that lets the overlap event know WHICH two sprites touched.
hint~

```blocks
//@collapsed
let powerUp: Sprite = null
let badVibe: Sprite = null
let note: Sprite = null
game.onUpdateInterval(1500, function () {
    if (randint(1, 10) == 1) {
        powerUp = sprites.create(sprites.effects.electricEffect1, SpriteKind.Projectile)
        powerUp.setVelocity(0, noteSpeed)
        powerUp.setPosition(randint(0, 160), 0)
        powerUp.setFlag(SpriteFlag.AutoDestroy, true)
    } else if (randint(1, 10) <= 3) {
        badVibe = sprites.create(sprites.projectile.explosion1, SpriteKind.Enemy)
        badVibe.setVelocity(0, noteSpeed)
        badVibe.setPosition(randint(0, 160), 0)
        badVibe.setFlag(SpriteFlag.AutoDestroy, true)
    } else {
        note = sprites.create(sprites.food.smallBurger, SpriteKind.Food)
        note.setVelocity(0, noteSpeed)
        note.setPosition(randint(0, 160), 0)
        note.setFlag(SpriteFlag.AutoDestroy, true)
    }
})
sprites.onOverlap(SpriteKind.Player, SpriteKind.Projectile, function (sprite, otherSprite) {
    info.changeScoreBy(3)
    otherSprite.destroy(effects.starField, 500)
    music.play(music.melodyPlayable(music.powerUp), music.PlaybackMode.InBackground)
    scene.cameraShake(2, 500)
})
```

## You Did It! 🎉 @showdialog

🏆 **Congratulations — you just built Groovy Star!** 🏆

And you didn't just build a game — you learned **6 real programming concepts:**

- 🛠️ **Initialization** — Setting the stage before the game begins. Background color, score, life, countdown — your code prepared everything before play started.
- 🧠 **Variables** — You gave the computer its memory. `noteSpeed` stored a number and you used it everywhere!
- 🔔 **Events** — Guards that never sleep. Timers fire on schedule, overlap events fire on contact — your code reacts automatically. You never had to call them!
- 🔢 **Sequencing** — Code runs top to bottom, in order, every time. The order of your steps IS the program.
- 💡 **Booleans** — The light switch of programming. YES or NO. TRUE or FALSE. Two answers, infinite power.
- 🌿 **Conditionals** — Branching off the main path. A boolean question splits your code: IF bad vibe, ELSE note. The computer takes ONE branch — never both.

These are the **foundations of every game, app, and program ever made.** You are thinking like a real programmer. 🥷⭐

Show off your high score — can anyone in the room beat it? 👊

## Make It YOUR Own! 🎨

Want to keep going? Here are some ways to customize Groovy Star — try them all!

**Change the variables (you already know how!):**

- :move: Change `noteSpeed` from 80 to **120** or **150** — feel the difference immediately!
- :move: Change the speed boost from `+= 10` to `+= 15` for an even wilder ride
- :shuffle: Change `% 5` to `% 3` for a speed boost every 3 catches instead of 5
- :game die: Change `<= 3` to `<= 5` to make bad vibes appear 50% of the time!

**Change the look:**

- :paint brush: Try a different background color — yellow, orange, or pink for neon concert vibes!
- :shuffle: Swap your star sprite for any shimmer, gem, or dancing character in the Gallery
- :star: Change the catch effect from `confetti` to `hearts`, `rings`, or `spray`

**Add some sounds:**

- :music: Add a `|| music: play sound ||` inside the **Player + Food** overlap (catching notes) for a celebration ding on every catch! 🎶
- :music: Add `power up` for `jump up`, `zapped`, or `magic wand` on the power-up overlap
- :music: Add `wawawawaa` inside the bad vibe overlap for a hilarious fail sound 😂

**Change the scoring:**

- :trophy: Change `change score by (1)` to **2** or **5** for bigger point swings
- :trophy: Change `change score by (3)` on the power-up to **10** for a MEGA bonus!
