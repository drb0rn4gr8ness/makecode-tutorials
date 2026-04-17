# Code Ninjas Evans GBS

### @diffs true

```template
scene.setBackgroundColor(7)
info.setScore(0)
info.startCountdown(60)

let basket: number[] = []

sprites.onOverlap(SpriteKind.Player, SpriteKind.Food, function (sprite, otherSprite) {

})

game.onUpdateInterval(1200, function () {

})
```

## Welcome to Fruit Basket! 🍎 @showdialog

Get ready — colorful fruit is about to rain from the sky and YOU have to catch as much as you can before the clock runs out!

Today's big concept is **arrays** — one of the most powerful tools in all of coding. By the end of this session, you'll know exactly what arrays are, how to use them, and why they show up in almost every app and game ever made. 🧺

Let's catch some fruit! 🍋🍩

## What is an Array? @showhint

Imagine you have a shopping list. You write down: apples, bananas, milk, eggs. That list can **grow** when you add more items, **shrink** when you cross things off, and you can check **how many items** are on it at any time.

An **array** is EXACTLY that — a list that lives inside your code!

Arrays can hold as many things as you need — numbers, names, sprites, anything. And you can do three super useful things with them:
- ➕ **Add** things to it (called "pushing" an item onto the list)
- 📏 **Check how many** items are in it (that's the "length")
- 🗑️ **Clear it** when you want to start fresh

In our game, we'll use an array called **basket** to track every piece of fruit the player catches. Every catch — another item goes in the basket! 🧺

## Initialize Our Groovy Game! 🍓

Your template already has the setup code inside the `|| loops: on start ||` block. Let's look at what each part does!

- :paint brush: **Background**: Click the color circle in `|| scene: set background color to ||` — try a sunny **green** (color 7) or bright **yellow** (color 5) for that outdoor market feel! 🌞
- :trophy: **Score**: `|| info: set score to (0) ||` — everyone starts at zero. Fair game!
- :clock: **Countdown**: `|| info: start countdown (60) ||` — hit play RIGHT NOW and watch what happens! A 60-second timer appears automatically. When it hits zero, the game ends on its own!
- :basket: **Basket Array**: See that `let basket = []`? That's your **array** — and it's empty right now! It has nothing in it yet, but it's ready and waiting to hold fruit. 🧺

```blocks
scene.setBackgroundColor(7)
info.setScore(0)
info.startCountdown(60)
let basket: number[] = []
```

## Create Your Catcher! 🏃

Time to get your character on screen — the hero who's going to catch ALL this fruit!

- :plus: **Create the Sprite**: Add a `|| variables(sprites): set mySprite to ||` block inside `|| loops: on start ||`. Click **New Variable** and name it **catcher**. Pick a fun character from the Gallery!
- :marker: **Set the Position**: Add a `|| sprites: set mySprite position to x (0) y (0) ||` block. Change **mySprite** to **catcher**, set **x** to **80** and **y** to **105** — near the bottom of the screen!
- :game controller: **Enable Movement**: Add a `|| controller: move mySprite with buttons ||` block and change **mySprite** to **catcher**. Left and right, let's go!
- :lock: **Stay on Screen**: Add a `|| sprites: set mySprite stay in screen ||` block, change it to **catcher**, and set it to **ON**. No running off the edge!

```blocks
scene.setBackgroundColor(7)
info.setScore(0)
info.startCountdown(60)
let basket: number[] = []
let catcher: Sprite = null
catcher = sprites.create(sprites.castle.heroWalkFront1, SpriteKind.Player)
catcher.setPosition(80, 105)
controller.moveSprite(catcher)
catcher.setStayInScreen(true)
```

## Let's Go! 🚀 @showdialog

🎉 Hit play — you should see your character, the score, and that 60-second timer ticking away!

Try moving with the arrow keys! Your catcher is READY.

Now let's make it RAIN fruit! 🍎🍋🍩

## Make Fruit Fall! 🍎🍋🍩

We'll use the game update interval to drop three different fruits randomly. Every 1.2 seconds — a new piece of fruit drops from a random spot!

- :shuffle: **Add an If/Else If/Else Block**: Inside `|| game: on game update every (1200) ||`, add an `|| logic: if <true> then ||` block. Click **+** at the bottom **twice** to get three branches: `if / else if / else`.
- :game die: **First Condition**: Replace the first **true** with `|| math: pick random (1) to (3) ||` `= 1`. 
- :apple: **First Fruit**: Inside the **if** branch, create a `|| variables(sprites): set mySprite to ||` block. Name the variable **fruit**, pick **smallApple** from the food Gallery, and set Kind to **Food**.
- :lemon: **Second Fruit**: Set the **else if** condition to `pick random (1) to (3) = 2`. Inside that branch, create another **fruit** sprite using **smallLemon**.
- :donut: **Third Fruit**: Inside the **else** branch (no condition needed!), create another **fruit** sprite using **smallDonut**.
- :move: **Make it Fall**: AFTER the if/else block, add velocity `vx (0) vy (70)`, position `x (randint 10 to 150) y (0)`, and **Auto Destroy** ON — all set to **fruit**.

~hint Why do all three fruits use the same variable name?
- :info: Because after we pick WHICH fruit to create, all three need the same movement and position code. By using the same variable name **fruit**, we write those three blocks just ONCE instead of three separate times. That's working smarter, not harder! 💡
hint~

```blocks
//@collapsed
let catcher: Sprite = null
let fruit: Sprite = null
game.onUpdateInterval(1200, function () {
    if (randint(1, 3) == 1) {
        fruit = sprites.create(sprites.food.smallApple, SpriteKind.Food)
    } else if (randint(1, 3) == 2) {
        fruit = sprites.create(sprites.food.smallLemon, SpriteKind.Food)
    } else {
        fruit = sprites.create(sprites.food.smallDonut, SpriteKind.Food)
    }
    fruit.setVelocity(0, 70)
    fruit.setPosition(randint(10, 150), 0)
    fruit.setFlag(SpriteFlag.AutoDestroy, true)
})
```

## Fruit is Falling! @showdialog

Apples! Lemons! Donuts! 🍎🍋🍩 Hit play and watch it rain!

Nothing happens when you touch them yet though. Time to fill that basket and USE that array!

## Fill the Basket! 🧺

This is the MOST important part — using the **basket array** to track everything we catch! Add all of this inside the `|| sprites: on overlap ||` block (Player / Food).

- :trophy: **Earn a Point**: Add a `|| info: change score by (1) ||` block. Every fruit = 1 point!
- :sparkles: **Destroy the Fruit**: Add a `|| sprites: destroy mySprite ||` block, change to **otherSprite**, click **+**, pick **confetti** or **rings**. The fruit EXPLODES when caught! 🎊
- :basket: **Add to Basket**: Add an `|| arrays: add value to end of array ||` block. Set the array to **basket** and the value to **1**. This is like tossing a piece of fruit into your basket — the list just got one item longer!
- :music: **Victory Sound**: Add a `|| music: play sound ||` block and pick **power up** or something happy!

~hint What does "add value to end of array" actually do?
- :info: It's called **push** in coding! Every time you call it, a new item gets added to the END of the list. If the basket had 3 items and you push one more — now it has 4. The array grows every single catch!
hint~

```blocks
//@collapsed
let basket: number[] = []
let catcher: Sprite = null
sprites.onOverlap(SpriteKind.Player, SpriteKind.Food, function (sprite, otherSprite) {
    info.changeScoreBy(1)
    otherSprite.destroy(effects.confetti, 200)
    basket.push(1)
    music.play(music.melodyPlayable(music.powerUp), music.PlaybackMode.InBackground)
})
```

## 🧺 Sensei Check — Arrays & Push! @showdialog

YES! Your catcher is catching fruit and adding it to the basket array! 🎉

**Senseis — ask the class these questions before moving on:**

1. "Right now the basket array is empty when the game starts. After the player catches 3 fruits — how many items are in the basket? How do you know?"
2. "What is the word programmers use when they add something to the end of an array? Can anyone shout it out?"
3. "Why is it useful to use an array to track catches instead of just the score number we already have?"

---
Click **Next** when your Sensei gives the signal! 🥷

## Array Length @showhint

Here's something SUPER cool about arrays — every array always knows exactly how many items are in it. That number is called the **length**!

- A brand new empty basket has a length of **0**
- After catching 1 fruit → length is **1**
- After catching 5 fruits → length is **5**

And here's the powerful part: **you can check the length at any time and do something based on it!**

In our game, when the basket reaches **5** we're going to trigger a **BONUS ROUND** — extra points AND a flashy screen effect. Then we clear the basket so the player can fill it up all over again! 🎉

## Bonus Round! 🎊

Let's add the basket-full bonus! Add this INSIDE the overlap event, right after the `push` block.

- :question: **Check the Length**: Add an `|| logic: if <true> then ||` block. Replace **true** with `|| arrays: length of array (basket) ||` `>= 5`.
- :star: **Bonus Points**: Inside the if block, add `|| info: change score by (5) ||`. Five fruits in the basket = five bonus points! 💰
- :sparkles: **BONUS EFFECT**: Add `|| scene: start screen effect ||` and pick **confetti** or **hearts**. LIGHT SHOW! 🌟
- :trash: **Empty the Basket**: Add `|| variables: set basket to ||` and set it to `|| arrays: create array with ||` with nothing inside. Fresh empty basket — fill it again!

~hint What does clearing the basket look like in real life?
- :info: Think of a real shopping basket at checkout — the cashier takes ALL your items out and the basket is empty again. `basket = []` does the same thing: it replaces the full basket with a brand-new empty one. Ready to fill again immediately! 🛒
hint~

```blocks
//@collapsed
let basket: number[] = []
let catcher: Sprite = null
sprites.onOverlap(SpriteKind.Player, SpriteKind.Food, function (sprite, otherSprite) {
    info.changeScoreBy(1)
    otherSprite.destroy(effects.confetti, 200)
    basket.push(1)
    music.play(music.melodyPlayable(music.powerUp), music.PlaybackMode.InBackground)
    if (basket.length >= 5) {
        info.changeScoreBy(5)
        effects.confetti.startScreenEffect()
        basket = []
    }
})
```

## 📏 Sensei Check — Length & Clearing! @showdialog

BONUS ROUND UNLOCKED! Catch 5 fruits and watch the magic happen! 🎊

**Senseis — ask the class:**

1. "After catching 5 fruits, the bonus fires and the basket clears. What is the length of the basket RIGHT AFTER it gets cleared?"
2. "What would happen if I changed `>= 5` to `>= 3`? What about `>= 10`? Would the game be easier or harder?"
3. "Why do we need to clear the basket after the bonus? What would happen if we DIDN'T clear it?"

---
Click **Next** when your Sensei gives the signal! 🥷

## You Did It! 🎉 @showdialog

🏆 **Congratulations — you just built Fruit Basket!** 🏆

And you learned one of the most powerful tools in all of coding:

- 📋 **Arrays** — A list that lives inside your code. It grows, shrinks, and you can check it at any time!
- ➕ **Push** — How you add a new item to the END of an array. One push = one new item!
- 📏 **Length** — Every array always knows how many items are in it. Check it whenever you need!
- 🗑️ **Clearing an Array** — Reset any array to empty by setting it to a fresh empty list. Clean slate, start again!

Arrays are used in **every app and game ever made** — player inventories, high score lists, chat messages, shopping carts. You now know how they work. 🥷

How high can you score in 60 seconds? Challenge everyone in the room! 🍎🍋🍩
