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

## Welcome to Code Ninjas Evans! 👋 @showdialog

Today you are building **Fruit Basket** — a 60-second challenge where colorful fruit rains down and you have to catch as much as you can!

The big concept for today is **arrays**. Arrays are one of the most useful tools in all of coding, and by the end of this session you will know exactly what they are and how to use them.

Let's go!

## Introducing Arrays @showhint

Imagine you have a shopping list. You write down: apples, bananas, milk, eggs. That list can grow when you add more items, shrink when you cross things off, and you can check how many items are on it at any time.

An **array** is exactly that — a list that lives inside your code. You can:
- **Add** things to it
- **Check how many** items are in it
- **Clear it** when you want to start fresh

In our game, we will use an array called **basket** to track every piece of fruit the player catches!

## Initialize Our Game

Your template already has the setup done. Let's look at what each part does.

- :paint brush: **Background**: `|| scene: set background color to ||` — try a sunny green or yellow!
- :trophy: **Score**: `|| info: set score to (0) ||` — starts everyone at zero.
- :clock: **Countdown**: `|| info: start countdown (60) ||` — this starts a 60-second timer. When it hits zero, the game ends automatically!
- :basket: **Basket Array**: `let basket = []` — this creates an **empty array** called basket. It has nothing in it yet, but it is ready to hold items!

```blocks
scene.setBackgroundColor(7)
info.setScore(0)
info.startCountdown(60)
let basket: number[] = []
```

## Create Your Catcher

- :plus: **Create the Sprite**: Add a `|| variables(sprites): set mySprite to ||` block inside `|| loops: on start ||`. Click **New Variable** and name it **catcher**. Pick a fun character from the Gallery!
- :marker: **Set the Position**: Add a `|| sprites: set mySprite position to x (0) y (0) ||` block. Change **mySprite** to **catcher** and set **x** to **80** and **y** to **105**.
- :game controller: **Enable Movement**: Add a `|| controller: move mySprite with buttons ||` block and change **mySprite** to **catcher**.
- :lock: **Stay on Screen**: Add a `|| sprites: set mySprite stay in screen ||` block, change it to **catcher**, and set it to **ON**.

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

## Let's Go! @showdialog

🎉 Hit play — you should see your character, the score, and a 60-second countdown timer ticking away!

Now let's make colorful fruit fall from the sky!

## Make Fruit Fall 🍎🍋🍩

We will use the game update interval to drop three different kinds of fruit randomly. We use an `|| logic: if / else if / else ||` block to pick which one to drop each time.

- :shuffle: **Add an If/Else If/Else Block**: Inside `|| game: on game update every (1200) ||`, add an `|| logic: if <true> then ||` block. Click the **+** at the bottom of the block **twice** to add two more branches so you have `if / else if / else`.
- :game die: **First Condition**: Replace the first **true** with a `|| logic: (0) = (0) ||` block. On the left side add `|| math: pick random (1) to (3) ||`. On the right side put **1**.
- :apple: **First Fruit**: Inside the **if** branch, create a `|| variables(sprites): set mySprite to ||` block. Name the variable **fruit** and set the image to **smallApple** from the food Gallery. Set its **Kind** to **Food**.
- :lemon: **Second Fruit**: Replace the second **true** (else if) with `pick random (1) to (3) = 2`. Inside that branch, create another **fruit** sprite using the **smallLemon** image.
- :donut: **Third Fruit**: Inside the **else** branch (no condition needed), create another **fruit** sprite using the **smallDonut** image.
- :move: **Make it Fall**: After the if/else block, add `|| sprites: set mySprite velocity to vx (0) vy (70) ||` and `|| sprites: set mySprite position to x (randint 10 to 150) y (0) ||`. Also turn on **Auto Destroy**. Change **mySprite** to **fruit** for all three blocks.

~hint Why do all three fruits use the same variable name?

- :info: Because after we pick which fruit to create, all three need the same movement and position setup. By using the same variable name **fruit**, we can write those three blocks just once instead of three times!

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

Hit play — apples, lemons, and donuts should be raining down!

Nothing happens when you touch them yet. Time to fill the basket!

## Fill the Basket 🧺

Now for the most important part — using the **basket array** to track what we catch!

- :trophy: **Earn a Point**: Inside the `|| sprites: on overlap ||` block (Player / Food), add a `|| info: change score by (1) ||` block.
- :sparkles: **Destroy the Fruit**: Add a `|| sprites: destroy mySprite ||` block, change it to **otherSprite**, click **+**, and choose a fun effect like **confetti** or **rings**.
- :basket: **Add to Basket**: Add an `|| arrays: add value to end of array ||` block. Set the array to **basket** and the value to **1**. This is like tossing the fruit into your basket!
- :music: **Play a Sound**: Add a `|| music: play sound ||` block and choose **power up** or something happy.

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

## Introducing Array Length @showhint

Every array has a **length** — that is just the number of items currently in it.

- A brand new empty basket has a length of **0**
- After catching 1 fruit it has a length of **1**
- After catching 5 fruits it has a length of **5**

We can check the length of our basket array and do something special when it reaches **5** — like giving bonus points and emptying it so the player can fill it up again!

## Bonus Round! 🎉

Let's add a basket-full bonus. We will add a **conditional** right after the `push` block that checks if the basket is full.

- :question: **Check the Length**: After your `add to basket` block, add an `|| logic: if <true> then ||` block. Replace **true** with a `|| logic: (0) >= (0) ||` block. On the left side add `|| arrays: length of array (basket) ||`. On the right side put **5**.
- :star: **Bonus Points**: Inside the if block, add a `|| info: change score by (5) ||` block. Five fruits = five bonus points!
- :sparkles: **Bonus Effect**: Add a `|| scene: start screen effect ||` block and pick something flashy like **confetti** or **hearts**.
- :trash: **Empty the Basket**: Add a `|| variables: set basket to ||` block and set it to `|| arrays: create array with ||` with nothing inside. This creates a brand-new empty array, clearing the basket so the player can start filling it again!

~hint What does clearing the basket look like in real life?

- :info: Think about a real shopping basket. When you check out, all your items are taken out and the basket is empty again. `basket = []` does the same thing — it replaces the full basket with a fresh empty one!

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

## You Did It! 🎉 @showdialog

🏆 **Congratulations — you just built Fruit Basket!** 🏆

Here is what you learned today:

- 📋 **Arrays** — A list that lives inside your code. It can hold as many items as you need!
- ➕ **Push** — How you add a new item to the end of an array.
- 📏 **Length** — Every array knows how many items are in it. You can check it at any time!
- 🗑️ **Clearing an Array** — You can reset an array to empty by setting it to a new empty list.

Arrays are used in almost every app and game ever made — to store player scores, inventory items, messages, and so much more. You now know how they work!

How high can you score in 60 seconds? Challenge your friends! 🍎🍋🍩
