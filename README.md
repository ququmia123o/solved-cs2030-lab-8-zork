Download Link: https://assignmentchef.com/product/solved-cs2030-lab-8-zork
<br>



<h1>Task Content</h1>

<table width="680">

 <tbody>

  <tr>

   <td width="680"><strong>Zork!</strong><strong>Problem Description</strong>If you think that a computer game requires stunning graphics, or least, cute ones, to be captivating, then you haven’t played Zork. Created in the late 1970s, before sound cards or graphics cards were invented, Zork was a text-only adventure game famed for its storytelling and advanced text parser. In it, you play the role of an explorer plonked in front of a house, surrounded by a forest, with no hint of what your goal might be: whether to rescue an imprisoned princess, or to find hidden treasure.You interact by typing commands, such as “GO NORTH”, or “HIT THE TROLL WITH THE ELVISH SWORD”, and the game responds with textual descriptions, such as “Phosphorescent mosses, fed by a trickle of water from some unseen source above, make the crystal grotto glow and sparkle with every color of the rainbow”. These words spark one’s imagination of mystery, fear, and adventure in ways that graphics and sound cannot.Its commercial launch was a great success, spawning a trilogy (because otherwise the entire game could not fit into computer memory) that in total sold over 800,000 copies, and keeping it among the “Top 50 Games of All Time” even twenty years later. Zork foreshadowed, and influenced, the development of modern AI chatbots.<strong>Task</strong>In this task, you are only required to work with three things: a candle, a sword and a troll. These things are placed at possibly different rooms. For simplicity, you may assume that at no time will there be two of the same thing in a room. The objective is to simulate and test different scenarios of game play.This task is divided into several levels. You need to complete all levels. Read through all the levels to see how the different levels are related.You are also given the <a href="https://codecrunch.comp.nus.edu.sg/taskfile.php/5186/Pair.java">Pair</a> and <a href="https://codecrunch.comp.nus.edu.sg/taskfile.php/5186/ImList.java">ImList</a> classes. Notice that two additional methods stream() and toList() that respectively return the elements in a stream or an unmodifiable (immutable) list (of type List) are provided.<strong>Level 1</strong>Write a class Room to represent a room in the game. Things can be placed in a room. In this level, we shall place a Candle in the foyer. To simulate the passing of time, a method tick() in class Room is called.With respect to the candle, every tick causes the candle to change state.The following are the state changes of the candle.Candle flickers.Candle is getting shorter.Candle is about to burn out.Candle has burned out.</td>

  </tr>

 </tbody>

</table>

<table width="606">

 <tbody>

  <tr>

   <td width="606">jshell&gt; new Room(“foyer”);$.. ==&gt; @foyer jshell&gt; new Candle()$.. ==&gt; Candle flickers. jshell&gt; new Candle().identify()$.. ==&gt; “Candle” jshell&gt; new Room(“foyer”).add(new Candle());$.. ==&gt; @foyer Candle flickers. jshell&gt; new Room(“foyer”).add(new Candle()).tick()$.. ==&gt; @foyerCandle is getting shorter. jshell&gt; new Room(“foyer”).add(new Candle()).tick().tick()$.. ==&gt; @foyerCandle is about to burn out. jshell&gt; new Room(“foyer”).add(new Candle()).tick().tick().tick()$.. ==&gt; @foyerCandle has burned out. jshell&gt; new Room(“foyer”).add(new Candle()).tick().tick().tick().tick() $.. ==&gt; @foyerCandle has burned out.</td>

  </tr>

 </tbody>

</table>

<table width="606">

 <tbody>

  <tr>

   <td width="606">jshell&gt; new Troll()$.. ==&gt; Troll lurks in the shadows. jshell&gt; new Troll().identify()$.. ==&gt; “Troll” jshell&gt; new Sword()$.. ==&gt; Sword is shimmering. jshell&gt; new Sword().identify()$.. ==&gt; “Sword” jshell&gt; Room foyer = new Room(“foyer”).add(new Candle()).add(new Troll())foyer ==&gt; @foyer Candle flickers.Troll lurks in the shadows. jshell&gt; Stream.iterate(foyer, x -&gt; x.tick()).limit(6).forEach(System.out::println)@foyerCandle flickers.Troll lurks in the shadows.@foyerCandle is getting shorter.Troll is getting hungry.</td>

  </tr>

 </tbody>

</table>

Note that any ticks beyond the last state of the candle causes it to remain in it’s final state. Also, make sure that Room does not sub-class from any other class (apart from Object of course).

<h1>Level 2</h1>

Let’s now include two more things, Troll and Sword, into our room. Just like the candle, each of these things have their own states:

For the Troll:

Troll lurks in the shadows.

Troll is getting hungry.

Troll is VERY hungry.

Troll is SUPER HUNGRY and is about to ATTACK!

Troll attacks! For the Sword:

Sword is shimmering.

Things are output in order of which they are added into the room. Also note that your program should be flexible enough for other things to be included in future.

<table width="606">

 <tbody>

  <tr>

   <td width="606">@foyerCandle is about to burn out.Troll is VERY hungry.@foyerCandle has burned out.Troll is SUPER HUNGRY and is about to ATTACK!@foyerCandle has burned out.Troll attacks!@foyerCandle has burned out.Troll attacks! jshell&gt; foyer = foyer.add(new Sword())foyer ==&gt; @foyer Candle flickers.Troll lurks in the shadows.Sword is shimmering. jshell&gt; Stream.iterate(foyer, x -&gt; x.tick()).limit(3).forEach(System.out::println)@foyerCandle flickers.Troll lurks in the shadows.Sword is shimmering.@foyerCandle is getting shorter.Troll is getting hungry.Sword is shimmering.@foyerCandle is about to burn out.Troll is VERY hungry.Sword is shimmering. jshell&gt; foyer foyer ==&gt; @foyer Candle flickers.Troll lurks in the shadows.Sword is shimmering.</td>

  </tr>

 </tbody>

</table>

<h1>Level 3</h1>

Now, we are ready to interact with the objects. An interaction occurs by passing an action into an overloaded tick method that takes one argument. The action is in the form of a lambda that describes what actions to take on one or more things.

As an example, we can pass a dummy action x -&gt; x (the identity lambda) into tick. The test will take the following form:

jshell&gt; new Room(“foyer”).add(new Candle()).add(new Sword()).tick(x -&gt; x)

$.. ==&gt; @foyer

<table width="606">

 <tbody>

  <tr>

   <td width="606">jshell&gt; new Room(“foyer”).add(new Candle()).add(new Sword()).tick(x -&gt; x) $.. ==&gt; @foyerCandle is getting shorter.Sword is shimmering. jshell&gt; new Room(“foyer”).add(new Candle()).add(new Sword()).tick(x -&gt; x).tick(x -&gt; x)$.. ==&gt; @foyerCandle is about to burn out.</td>

  </tr>

 </tbody>

</table>

Candle is getting shorter. Sword is shimmering.

As you can see, applying the dummy action above results in the same behaviour as

jshell&gt; new Room(“foyer”).add(new Candle()).add(new Sword()).tick()

$.. ==&gt; @foyer

Candle is getting shorter. Sword is shimmering.

In addition, write the action takeSword into the file actions.jsh. Note that this will result in three different outputs (see sample run below) according to the state of things in the room. These output (prepended with “–&gt;”) must be specified within actions.jsh and not in the individual classes. You may choose any suitable types for the lambda.

<table width="606">

 <tbody>

  <tr>

   <td width="606">jshell&gt; new Room(“foyer”).add(new Sword()).tick(killTroll)–&gt; There is no troll.$.. ==&gt; @foyerSword is shimmering. jshell&gt; new Room(“foyer”).add(new Sword()).add(new Troll()).tick(killTroll)–&gt; You have no sword.$.. ==&gt; @foyer Sword is shimmering.Troll is getting hungry. jshell&gt; new Room(“foyer”).add(new Sword()).add(new Troll()).tick(takeSword).tick(killTroll)–&gt; You have taken sword.–&gt; Troll is killed.$.. ==&gt; @foyerSword is shimmering. jshell&gt; new Room(“foyer”).add(new Candle()).add(new Troll()).add(new Sword()).tick().tick(takeSwo–&gt; You have taken sword.$.. ==&gt; @foyerCandle is about to burn out.Troll is VERY hungry.Sword is shimmering. jshell&gt; new Room(“foyer”).add(new Candle()).add(new Troll()).add(new Sword()).tick().tick(takeSwo–&gt; You have taken sword.–&gt; Troll is killed.$.. ==&gt; @foyerCandle has burned out.Sword is shimmering. jshell&gt; new Room(“foyer”).add(new Candle()).add(new Troll()).add(new Sword()).tick().tick(killTro</td>

  </tr>

 </tbody>

</table>

Sword is shimmering.




jshell&gt; new Room(“foyer”).add(new Sword()).tick(takeSword)

–&gt; You have taken sword.

$.. ==&gt; @foyer

Sword is shimmering.




jshell&gt; new Room(“foyer”).add(new Sword()).tick(takeSword).tick(takeSword)

–&gt; You have taken sword.

–&gt; You already have sword.

$.. ==&gt; @foyer

Sword is shimmering.




jshell&gt; new Room(“foyer”).tick(takeSword)

–&gt; There is no sword.

$.. ==&gt; @foyer




jshell&gt; new Room(“foyer”).add(new Candle()).add(new Troll()).add(new Sword()).tick() $.. ==&gt; @foyer

Candle is getting shorter.

Troll is getting hungry.

Sword is shimmering.




jshell&gt; new Room(“foyer”).add(new Candle()).add(new Troll()).add(new Sword()).tick(x -&gt; x)

$.. ==&gt; @foyer

Candle is getting shorter.

Troll is getting hungry.

Sword is shimmering.




jshell&gt; new Room(“foyer”).add(new Candle()).add(new Troll()).add(new Sword()).tick().tick(x -&gt; x)

$.. ==&gt; @foyer

Candle is about to burn out.

Troll is VERY hungry. Sword is shimmering.

<h1>Level 4</h1>

Now add another action killTroll into actions.jsh. Look at the sample runs below for the behaviour of the action.

Once again, the output (prepended with “–&gt;”) must be specified in actions.jsh and not in the respective class files. Also note that a killed troll will vanish from the room.

<table width="606">

 <tbody>

  <tr>

   <td width="606">–&gt; You have no sword.$.. ==&gt; @foyerCandle is about to burn out.Troll is VERY hungry.Sword is shimmering. jshell&gt; new Room(“foyer”).add(new Candle()).add(new Troll()).add(new Sword()).tick().tick(killTro–&gt; You have no sword.–&gt; You have taken sword.$.. ==&gt; @foyerCandle has burned out.Troll is SUPER HUNGRY and is about to ATTACK! Sword is shimmering. jshell&gt; new Room(“foyer”).add(new Candle()).add(new Troll()).add(new Sword()).tick().tick(killTro–&gt; You have no sword.–&gt; You have taken sword.–&gt; Troll is killed.$.. ==&gt; @foyerCandle has burned out.Sword is shimmering. jshell&gt; new Room(“foyer”).add(new Candle()).add(new Troll()).tick(killTroll)–&gt; You have no sword.$.. ==&gt; @foyerCandle is getting shorter.Troll is getting hungry.</td>

  </tr>

 </tbody>

</table>

<table width="606">

 <tbody>

  <tr>

   <td width="606">jshell&gt; new Room(“dining”).add(new Candle()).add(new Sword())$.. ==&gt; @dining Candle flickers.Sword is shimmering. jshell&gt; new Room(“dining”).add(new Candle()).add(new Sword()).go(x -&gt; new Room(“mystery”, x)) $.. ==&gt; @mystery Candle flickers.Sword is shimmering.</td>

  </tr>

 </tbody>

</table>

<table width="606">

 <tbody>

  <tr>

   <td width="606">jshell&gt; new Room(“dining”).add(new Candle()).add(new Sword())$.. ==&gt; @dining Candle flickers.Sword is shimmering. jshell&gt; new Room(“dining”).add(new Candle()).add(new Sword()).go(x -&gt; new Room(“mystery”, x)) $.. ==&gt; @mystery Candle flickers.Sword is shimmering. jshell&gt; new Room(“dining”).add(new Candle()).tick().add(new Sword()).go(x -&gt; new Room(“mystery”, $.. ==&gt; @mysteryCandle is getting shorter.Sword is shimmering. jshell&gt; new Room(“foyer”).add(new Sword()).tick(takeSword).go(x -&gt; new Room(“dining”).add(new Can–&gt; You have taken sword.</td>

  </tr>

 </tbody>

</table>

<h1>Level 5</h1>

We are now ready to venture into other rooms. Going into a room requires that a room be created first. This is done via the go method that takes in another lambda of the form x -&gt; new Room…. As an example, we can represent <em>deja vu </em>with the following test:

Notice that this new mystery room that we just entered looks like the same room before! Not only that we can also bring an item that we picked into a new room.

jshell&gt; new Room(“foyer”).add(new Sword()).tick(takeSword).go(x -&gt; new Room(“dining”).add(new Can

–&gt; You have taken sword.

$.. ==&gt; @dining

Sword is shimmering.

Candle flickers.

Note that things brought into a new room are listed first.

<table width="606">

 <tbody>

  <tr>

   <td width="606">$.. ==&gt; @diningSword is shimmering.Candle flickers. jshell&gt; Room r1 = new Room(“foyer”).add(new Candle()) r1 ==&gt; @foyer Candle flickers. jshell&gt; Room r2 = r1.go(x -&gt; new Room(“library”).add(new Sword())) r2 ==&gt; @library Sword is shimmering. jshell&gt; Room r3 = r2.go(x -&gt; new Room(“dining”).add(new Troll())) r3 ==&gt; @diningTroll lurks in the shadows. jshell&gt; r3.tick(killTroll)–&gt; You have no sword.$.. ==&gt; @diningTroll is getting hungry. jshell&gt; r2.tick(takeSword).go(x -&gt; new Room(“dining”).add(new Candle()).add(new Troll()))–&gt; You have taken sword.$.. ==&gt; @diningSword is shimmering.Candle flickers.Troll lurks in the shadows. jshell&gt; r2.tick(takeSword).go(x -&gt; new Room(“dining”).add(new Candle()).add(new Troll())).tick(ki–&gt; You have taken sword.–&gt; Troll is killed.$.. ==&gt; @diningSword is shimmering.Candle is getting shorter.jshell&gt; r1.go(x -&gt; new Room(“library”).…&gt; add(new Sword()).…&gt; tick(takeSword).…&gt; go(y -&gt; new Room(“dining”).add(new Candle()).add(new Troll()))).tick(killTroll) –&gt; You have taken sword.–&gt; Troll is killed.$.. ==&gt; @diningSword is shimmering.Candle is getting shorter.</td>

  </tr>

 </tbody>

</table>

<table width="606">

 <tbody>

  <tr>

   <td width="606">jshell&gt; Room r1 = new Room(“foyer”).add(new Candle()) r1 ==&gt; @foyer Candle flickers. jshell&gt; Room r2 = r1.go(x -&gt; new Room(“dining”).add(new Troll())) r2 ==&gt; @diningTroll lurks in the shadows. jshell&gt; Room r3 = r2.go(x -&gt; new Room(“library”).add(new Sword())) r3 ==&gt; @library Sword is shimmering.jshell&gt; r1 r1 ==&gt; @foyer Candle flickers.jshell&gt; r2 r2 ==&gt; @dining</td>

  </tr>

 </tbody>

</table>

<h1>Level 6</h1>

Finally, we would like to go back to the previous rooms. For simplicity, once we come back from a room, the room that we came back from vanishes, so we can’t go into it again. Note that when you return from room B to room A, things in room A are output first, followed by B (this is to be consistent with the output in the previous level dealing with go). That is to say, things in the room that is created earlier are always listed first. Also note that once we enter into a new room, and return from it, time in the original room ticks only once.

Lastly, add an action dropSword to drop the sword.


