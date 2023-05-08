Download Link: https://assignmentchef.com/product/solved-swen221-assignment-5-settlers-of-catan
<br>
<h1>1           Settlers of Catan</h1>

Catan is a popular board game where up to 4 players collect resorces, build settlements and play for points on a hexagonal board.

On each turn, players may place settlements on the corners of an available hex, or a road on an available edge. At the start of each turn 2 dice are rolled and resources are produced from the hexes labelled with the rolled number. These resources are then used by players to build settlements to hopefully collect more resources until some player collects enough points to win. Points are earned by building settlements. The full rules also include a set of cards called “development cards” and a set of trading posts, but we are modelling a variation that <strong>does not feature development cards or trading posts</strong>, so you do not need to worry about them in this assignment. To better understand the rules, you can find the o cial rule set at https://www.catan.com/en/download/?SoC_rv_Rules_091907.pdf

<h2>1.1         Setup</h2>

Before the game takes place, setup must be performed.

<ol>

 <li>A hexagonal board is constructed as in the above Figure by placing 3 concentric layers ofhexagonal tiles. That is, a single tile, surrounded by six tiles, which are then also surrounded by 12 additional tiles.</li>

 <li>Each tile is assigned a resource from a randomly sorted pool of 4 <strong>Wood</strong>, 3 <strong>Stone</strong>, 3 <strong>Brick</strong>, 4 <strong>Wheat</strong>, 4 <strong>Sheep </strong>and 1 <strong>Desert</strong>. This is done row by row, from left to right and top to bottom. For example in the image on the first page, the leftmost tile on the top row is assigned stone, followed by wood for the middle top tile and brick to the rightmost top tile. Then wheat is assigned to the leftmost tile on the second row, and so on.</li>

 <li>Each tile is assigned a resource counter with a number (from 2 to 12). This is done in a clockwisefashion starting from the top leftmost tile and spiralling inwards. In the above figure we start with 8, then 4, 6, 10, 9, 6, 5, 4, 10, 3, 5, 11, 2, 12, 11, 3, 8, 9. The final tile in this example is a Desert, but in most games the desert will not necessarily be in the centre, and will be skipped when placing resource counters.</li>

 <li>Each player take turns to place two settlements and two roads on the board. Settlements areplaced at the corners of tiles and roads along the edges. Settlements may not be adjacent to another player’s settlement. Roads have to be placed next to a player’s settlement.</li>

</ol>

<h2>1.2         Order of Play</h2>

A player’s turn consists of the following actions:

<ol>

 <li>Distribute Resources: Two six-sided dice are rolled giving a number between 2 and 12. All tilesmarked with that number distribute resources to all players who own settlements on that tile according to the following rules:

  <ul>

   <li>Each town gets 1 resource</li>

   <li>Each city gets 2 resources</li>

  </ul></li>

 <li>Build: The player may build new towns, upgrade existing towns to cities or build roads.</li>

</ol>

There are several rules that govern how the above actions take place. Firstly, a player may not place a settlement adjacent to another player’s town. Each possible site for a settlement or a road may only contain one settlement or road. Except in the setup phase, players may only place towns in open spots next to roads they own.

Points are awarded in the following way: 1 point for each town and 2 points for each city.

<h1>2           Getting Started</h1>

In this assignment you will implement certain parts of the Catan game. Using <em>Generic types </em>you will implement a hexagonal graph where each node is a tile on the board. Using <em>Java Streams </em>and <em>Java Lambdas </em>you will implement parts of the logic of the setup.

You can complete this assignment by working on the code in catan.jar. However, there is a GUI available in catanGUI.jar; you can run the GUI with the command line java -jar catanGUI.jar. It expects a jar catan.jar in the same folder. At the start, the GUI will not work properly since you need to implement more behaviour in catan.jar. For the submission, you only need to submit your improved version of catan.jar (with source code, as usual).

When you have completed catan.jar, you should see a GUI come up similar to the following:

When your code is completed, pressing the buttons “Set Resources” and “Set Resource Counters” will allocate resource types (e.g. stone, brick, etc) to the tiles and amounts to those tiles. You can then build settlements and roads by dragging from the respective icons.

<h2>2.1         Understanding the Code</h2>

To get started, import the catan.jar file from the lecture schedule on the course website. For this assignment, there are three key classes you will be working with:

<ul>

 <li><strong>(</strong>HexNode<strong>)</strong>. The class HexNode represents an hexagonal tile on the board and implements the interface graph.Node. This class gives structure to the underlying board allowing, for example, one to determine adjacent tiles, etc.</li>

 <li><strong>(</strong>CatanTile<strong>)</strong>. The class game.CatanTile provides the contents for a HexNode which provides necessary functionality for the game itself.</li>

 <li><strong>(</strong>Game<strong>)</strong>. The class CatanGame provides a concrete instantiation of the game. It makes extensive use of classes in the package model.</li>

</ul>

In addition to the above files, supplementary code is present in catanGUI.jar. <strong>The source code for this library is not provided, as you will not need to modify it, nor import it into eclipse</strong>.

<h1>Part 1 — HexNode</h1>

Before we can implement the full Catan game, we need to develop a basis for it. A skeleton implementation of Node is provided called HexNode which currently does not implement all the required functionality. You need to complete its implementation as necessary. When you’ve done this, you should find the tests in Part1Tests all pass. A valid graph should represent an hexagonal grid, this means that for example:

<ul>

 <li>A node can not have itself as a neighbour.</li>

 <li>If going WEST from node1 we reach node2, then going EAST from node2 we reach node1. That is, the graph is non-directional: if node1 is connected to node2, then node2 is connected to node1 in the opposite direction.</li>

 <li>If going EAST from node1 we reach node2, and going NORTHEAST from node1 we reach node3, then going SOUTHEAST from node3 we reach node2.</li>

 <li>the method isValid() contains useful assertions checking that the graph is valid according to those criteria. We encourage you to use isValid() or a similar personalized method to check if your code is preserving the validity of the graph.</li>

</ul>

We suggest you to implement the methods in the following order:

<ol>

 <li>hasNeighbor(Direction)</li>

 <li>add(Direction, Node&lt;Direction, V&gt;)</li>

 <li>isConnected(Direction, Node&lt;Direction, V&gt;)</li>

 <li>connect(Direction, Node&lt;Direction, V&gt;)</li>

 <li>fillNeighborhood()</li>

 <li>generate(Integer)</li>

 <li>toList()</li>

 <li>stream()</li>

 <li>clockwiseStream()</li>

</ol>

Carefully read the documentation of what those methods should do on the interface Node. The last two methods allows to stream the nodes:

<ul>

 <li>stream: nodes are streamed from left to right, and top to bottom starting at the top leftmost node and ending at the bottom rightmost node.</li>

 <li>clockwiseStream: nodes are streamed clockwise starting from the top leftmost node, and ending at the center node.</li>

</ul>

<strong>NOTE: </strong>while there are complex but e cient ways to create streams without materializing the list of elements, this is not required by this assignment, and you can simply create a list with the elements in the right order and then create a stream from such list.

<h1>3           Part 2</h1>

CatanTile and CatanGame have many methods that needs to be implemented in this phase. For the methods CatanTile.addSettlement(Settlement, Location) and CatanTile.addRoad(Road, Direction), observed that a tile <em>shares </em>it’s settlement and road locations with neighbouring tiles.

In CatanGame, there are several methods which we suggest you implement in the following order:

<ol>

 <li>toString(Stream&lt;Node&lt;K, V&gt;&gt; stream, Function&lt;V, String&gt; mapper&gt;. This method aims to provide a rich mechanism for printing out information from the graph. This method makes good use of generic types to ensure a flexible API.</li>

</ol>

<strong>NOTE: </strong>CatanGame already has an implementation of the basic toString() method. This returns a string of the ids of all the nodes in the correct order. <em>You may find it useful to examine this method</em>.

<strong>HINT: </strong>After implementing this method, you should find that test toStringTest1() now passes.

<ol start="2">

 <li>setResources(List&lt;Resources&gt; pool): taking a pool of resources we need to distribute them in a left to right, top to bottom manner as previously described. <em>The implementation of this method is provided as an example.</em></li>

</ol>

<strong>HINT: </strong>To get tests testSetResources1/2/3() to pass, you will need to implement methods in CatanTile.

<ol start="3">

 <li>setResourceCounters(List&lt;ResourceCounter&gt; pool): taking a pool of resource counters, we need to distribute them on the board in a clockwise fashion, starting from the top leftmost tile, spiralling into the center. If we encounter any DESERT tiles, we assign that tile a counter with the value NONE. <em>This method needs to be implemented.</em></li>

</ol>

<strong>HINT: </strong>Reading testSetResourceCounters1 may help you to understand the required behaviour better.

<ol start="4">

 <li>distributeResources(Integer diceRoll): taking a dice roll of between 2 and 12, we need to distribute any resources gained to players that have settlements on tiles with that number. It is a good strategy to implement distributeResources A correct implementation for CatanTile.addSettlement(Settlement, Location) is crucial to be able to complete distributeResources(Integer diceRoll). <em>This method needs to be implemented.</em></li>

</ol>

When you have implemented those methods, you should find the tests in Part2Tests all pass.

<h1></h1>