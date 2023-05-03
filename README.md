Download Link: https://assignmentchef.com/product/solved-cs20a-project-1-conways-game-of-life
<br>
Following what we discussed on multiple file etiquette take the single source file provided, and divide it into appropriate header files and implementation files, one pair of files for each class. Place the main routine in its own file named main.cpp. Make sure each file #includes the headers it needs. Each header file must have include guards. Only include header files when they are actually needed.

Now what about the global constants? Place them in their own header file named globals.h. And what about utility functions like delay or clearScreen ? Place them in their own implementation file named utils.cpp, and place their prototype declarations in globals.h.

The first thing you should do is make sure that the single source compiles as is.  Play around with it to get

comfortable the program.  The program implements Conway’s Game of Life

<a href="https://en.wikipedia.org/wiki/Conway%27s_Game_of_Life">https://en.wikipedia.org/wiki/Conway%27s_Game_of_Life</a><a href="https://en.wikipedia.org/wiki/Conway%27s_Game_of_Life">,</a> which is a simple simulation where cells are either alive or dead based simple rules based on under population or overcrowding.

<strong>Add a feature </strong>

When you run the program you should notice that the &lt;s&gt; options does nothing.  Your job will be to implement this feature.  Run the executable provided with this spec where the feature has been added to the game. For Windows : CS20A_Project1_SOLN.exe, OSX: CS20A_Project1_SOLN.

When you press &lt;s&gt;, depending  in how the current state evolved, you will see how many times a cell has been birthed, ‘.’ indicates no change, ‘A’ through ‘Z’ indicated the number of times it has been birthed (corresponding to 1 through 26, capping at 26).  We are not keeping track of deaths.

Your task is to implement this functionality. You will need to do the following:

 Define a class named Stats  with the following public interface:

class Stats { public:

// Constructor/destructor

Stats();

~Stats();

// Accessors or Getters  void display() const;

// Mutators or Setters

bool record(int r, int c, int val);

private:

// TODO

};

<ul>

 <li>The constructor initializes the Stats’s grid to correspond to the World’s, however Stats keeps tracks of a count of births for each cell, whereas the World simple displays the cells’ state, being represented by characters.</li>

 <li>The destructor cleans up the Stats object. Similar to how the World cleans up after itself.</li>

 <li>The display member function prints the stats grid similar to what is seen in the example program.</li>

 <li>The record function updates the Stats grid at row r and column c by increased that cell by val. The record function should return false if the coordinates are out of bounds, and true otherwise.</li>

</ul>

The class declaration (with any private members you choose to add to support your implementation) must be in a file named stats.h, and the implementation of the Stats class’s member functions must be in stats.cpp. You must not add any other public members to the class. (This implies, for example, that you must not add a public default constructor.) The only member function of the Stats class that may write to cout is Stats::display.

Add a data member of type Stats (<em>not</em> of type pointer-to-Stats) to the World class, and provide this public function to access it; notice that it returns a <em>reference</em> to a Stats object.

class World {

…

Stats&amp; stats();

…

};

Whenever the world is updated we must check to see which cells have been birthed, those cells’ position is then updated in the stats object by adding 1 with the Stats::record function.  Note that if the cell’s state has not changed or if it has died, we do not record anything.

The Game’s &lt;s&gt; option should be completed to display the current stats grid. Press enter to continue. prompt and wait for the user to respond. (cin.ignore(10000,’
’); does that nicely).

<strong>Additional guidelines and hints: </strong>

<ul>

 <li>If a .cpp file uses a class or function declared in a particular header file, then it should #include that header. The idea is that someone writing a .cpp file should not worry about which header files include other header files. For example, a .cpp file using an A object and a B object should include both A.h (where presumably the class A is declared) and B.h (where B is declared), without considering whether or not A.h includes B.h or vice versa.</li>

 <li>In your .h and .cpp files, for any #include of a header defining one of the classes in this project (e.g., #include “game.h”), if you can replace that header with an incomplete type declaration of the class it defines (e.g. class Game;) and all code that must compile does compile, and all code that must not compile does not compile, then you must do so.</li>

 <li>Except to add the member function World::stats or to change string to std::string, you must not make any additions or changes to the public interface of any of the classes. (You are free to make changes to the private members and to the implementations of the member functions.) The word friend and the word sequence pragma once must not appear in any of the files you submit.</li>

 <li>Your program must not use any global variables whose values may change during execution. Global constants (e.g. MAX_ROWS) are all right.</li>

 <li>Except in Game::play (or a function it calls) and Stats::display, your program must write no output to cout beyond what is already in the program or is required by this spec. If you want to print things out for debugging purposes, write to cerr instead of cout. When we test your program, we will cause everything written to cerr to be discarded instead — we will never see that output, so you may leave those debugging output statements in your program if you wish. Note that cerr is an output stream just like cout, just one for errors.</li>

 <li>If we replace your main.cpp file with the following, the program must build successfully:</li>

</ul>

#include “game.h”

#include “game.h”

#include “world.h”

#include “world.h”

#include “stats.h”

#include “stats.h”

#include “life.h”

#include “life.h”

#include “blinker.h”

#include “blinker.h”

#include “glider.h”

#include “glider.h”

#include “globals.h”  #include “globals.h”

int main()  {}




<ul>

 <li>If we replace your main.cpp file with the following, the program must build successfully</li>

</ul>

#include “stats.h” int main()

{

Stats s;

s.record(1, 1,1);

s.display();

}

stats.h must not contain any #include line that, if removed, still allows the above replacement main.cpp to compile successfully.

<ul>

 <li>If we replace your main.cpp file with the following, the program must build successfully</li>

</ul>

#include”blinker.h”

int main() {

Blinker b(1,1);

blinker.h must not contain any #include line that, if removed, still allows the above replacement main.cpp to compile successfully.

<ul>

 <li>If we replace your main.cpp file with the following, the program must build successfully</li>

</ul>

#include”world.h” int main() {

World w;

w.addLife(nullptr);

}

world.h must not contain any #include line that, if removed, still allows the above replacement main.cpp to compile successfully.

<ul>

 <li>If we replace your main.cpp file with the following, the program must build successfully</li>

</ul>

#include”world.h” #include “blinker.h” int main() {

World w;

Blinker b(2, 2);  w.addLife(&amp;b);

}

<ul>

 <li>If we replace your main.cpp file with the following, the program must build successfully</li>

</ul>

#include”world.h”

#include “blinker.h” #include&lt;iostream&gt; using namespace std;

int main() {

int num_steps = 0;

World w;

Blinker b(2, 2);  w.addLife(&amp;b);




do {

w.update();

} while (w.hasWorldChanged() &amp;&amp; (num_steps++) &lt; 10);        w.stats().display();

cout &lt;&lt; “===” &lt;&lt; endl;

}




When Executed we must see:




………..

………..

..E……..

.F.F…….

..E……..

………..

………..

………..

………..

………..

………..

<h1>===</h1>

<ul>

 <li>The following should display “ OUT OF BOUNDS “.</li>

</ul>

#include “stats.h”

#include “globals.h” #include&lt;iostream&gt; using namespace std;

int main() {

Stats s;

if (!s.record(-1, (MAX_ROWS+1) , 0)) {

cerr &lt;&lt; ” OUT OF BOUNDS ” &lt;&lt; endl;

}

}

<ul>

 <li>If we replace your main.cpp file with one the following, the program must <strong><u>NOT</u></strong> build successfully:</li>

</ul>

#include “blinker.h” int main() {

World w;

Blinker b(2, 2);

}

#include”world.h” int main() {

World w;

Blinker b(2, 2);




#include “game.h”

#include “stats.h”

#include “life.h”

#include “blinker.h” #include “glider.h”

#include “globals.h”

int main() {

World w;




#include “stats.h”

#include “life.h”

#include “blinker.h”

#include “glider.h”

#include “world.h”

#include “globals.h”




int main() {

Game g(nullptr, 0);

}

#include “stats.h”

#include “world.h”

#include “globals.h” #include “game.h” int main() {




Life l;

}