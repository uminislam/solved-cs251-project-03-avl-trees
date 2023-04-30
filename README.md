Download Link: https://assignmentchef.com/product/solved-cs251-project-03-avl-trees
<br>
For the last couple weeks we have been building an AVL class — it’s time to put all the pieces together.  The assignment is to create a templated <strong>avltree&lt;TKey, TValue&gt;</strong> class in the file “avl.h” which properly balances trees as part of the insert function.  When completed, <strong>search</strong> and <strong>insert</strong> must be O(lgN) operations; <strong>size</strong> and <strong>height</strong> must be O(1) operations.  Recall that we began modifying insert in HW #07 to compute the heights; in HW #08 you were asked to implement the left and right rotate functions.  Your test cases were created as part of lab week #07.

The major change to make now is to modify <strong>insert</strong> so that as you walk up the tree updating heights, you also check to see if the AVL condition is broken.  If so then rotate to fix — either one rotation for AVL cases 1 and 4, or 2 rotations for AVL cases 2 and 3.  Recall that in class (day 20) we discussed a <strong>_RotateToFix</strong> function that insert could call to fix the tree; this function in turn calls _LeftRotate and _RightRotate.

You will need to implement the following public functions in your avltree class, exactly as shown here.  You cannot add nor remove parameters, or change types:

<strong>template&lt;typename TKey, typename TValue&gt; class avltree </strong>

{ private:

.

.

.  <strong>public: </strong>

avltree()

avltree(avltree&amp; other)

<strong>  virtual ~avltree()          // destructor: </strong>  int size()   int height()

<strong>  void clear()                // clear: </strong>




TValue* search(TKey key)

void insert(TKey key, TValue value)

<strong>  int distance(TKey k1, TKey k2)    // distance: </strong>

<strong> </strong>  void                inorder()   std::vector&lt;TKey&gt;   inorder_keys()   std::vector&lt;TValue&gt; inorder_values()   std::vector&lt;int&gt;    inorder_heights()




<strong>}; </strong>







Note that three functions have been added for the purposes of project #03:  a <strong>destructor</strong> to free memory, a <strong>clear</strong> function to empty a given tree, and a <strong>distance</strong> function that returns the path length between 2 keys.  Your avltree class must now free all allocated memory; more details in the next section.




<h1>Assignment details</h1>

Your avlclass must now contain a <strong>destructor</strong> that properly frees all memory allocated by the avltree class.  On submission we’ll check using <strong>valgrind</strong>, so you should do the same as part of your testing; recall that destructors and valgrind were introduced in lab during week 05.




Your avlclass must also contain a <strong>clear</strong> function that empties the tree of all nodes, properly freeing the memory.  Note that you *cannot* call the destructor to do this; destructors in C++ are special functions that should only be called by the compiler.  Instead, what you should do is create a private helper function that both the destructor and clear call.  When clear returns, the root should be nullptr and the size 0.




Finally, add a function <strong>distance(k1, k2)</strong> that returns the “distance” between the keys k1 and k2.  The distance is defined as the length of the minimum path between k1 and k2.  For example, consider the following tree ———&gt; The distance(5, 100) = 6.  The distance from 31 to 12 is 3.  And the distance from 46 to 12 = 3.  The reverse are also true, e.g. the distance(100, 5) = 6.




If k1 or k2 is not in the tree, then the distance is defined as -1.  If k1 = k2, then the distance is 0.










<h1>Programming Environment</h1>

You are free to program in any environment you want; final submissions will be collected using Gradescope.  If you want to use Codio, a project has been created named “<strong>cs251-project03-avl</strong>”.  The environment will contain catch and valgrind for testing purposes.




In Codio, use “<strong>make catch</strong>” to build your Catch-based “test.cpp” program.  Then “<strong>make run</strong>” to run.  If you want to run your program with valgrind to check for memory leaks / pointer errors, do “<strong>make valgrind</strong>”.




<h1>Requirements</h1>

Your avltree class must be templated, and follow the approach we have been discussing in class (and building in the HW and Labs).  Rebalancing must occur during insert, both search and insert must be O(lgN), and size and height must be O(1).  This implies your private NODE structure must contain a height field that is properly maintained by the insert and the rotate functions.




Additional program requirements:




<ol>

 <li><em>No other data structures may be used to implement the AVL tree itself — i.e. build your tree using a Struct NODE with Key, Value, Height, Left and Right pointers. You can add a Parent pointer if you want, but nothing else should be needed nor added.  You can use a stack to walk up the tree and update the heights, etc., but the tree itself must be built using NODEs and pointers. </em></li>

</ol>

<em> </em>

<ol start="2">

 <li><em>Use std::vector to capture and return the data needed by the <strong>inorder</strong> testing functions. Likewise, if you need an additional data structure to implement your distance function, by all means use one. </em></li>

</ol>





