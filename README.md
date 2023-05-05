Download Link: https://assignmentchef.com/product/solved-csi2110-lab7-hashing
<br>
In this lab, you will implement several different collision resolution techniques for Hashing.You will also use Hashing in an application for word counting on a large text.

<strong>Part 0: Overview of startup code structure:</strong> your TA will walk you through this part.

<ul>

 <li style="list-style-type: none;">

  <ul>

   <li>Download the following file: <a href="Lab7.zip">Lab7.zip</a></li>

   <li>Hash functions:StringHash: Simple hashing function for stringsReverseStringHash: Uses the same function as before, but on the reversed sting</li>

   <li>Hash tables:ArrayHashTable: An implementation for a hash table handling overflow by finding another place in the table via probing table positions. This must be general enough such that any form of probing can be done. So, the constructor requires 2 hash functions, in the case of linear and quadratic probing, the second one will be null, in the case of double hashing or quadratic double hashing the second hash function will be provided.ChainedHashTable: An implementation for a hash table handling overflow by using separate chaining (each table position can hold an array list of elements hashing to that position)</li>

   <li>Stepping Functions: Functions to take the i value of the step and return the actual step value, the second and third require the long value of the second hash to calculate the step: LinearProbeStep, QuadraticProbeStep, DoubleHashStep, QuadraticDoubleHashStep.</li>

   <li>TestingToyTest: A simple test to check if all values are being added, and overwriting and get work properley, for debuggingHashingTest: A test to check the statistics of the various methods of collision resolution using book chapters to test with.</li>

  </ul></li>

 <li><strong>Part 1: Implementing Hashing with different collision resolution techniques</strong>Note: Be aware that remove and contains are implemented in such a way that methods put and get must be aware of special values to indicate that a table position has never been occupied (NULL at the table) and that the position is AVAILABLE but it has been occupied before (Entry&amp;ltK,V&amp;gt present at the table with key=null).</li>

</ul>

<ul>

 <li style="list-style-type: none;">

  <ol>

   <li><strong>Implementing Linear Hashing</strong>In this part, you will complete the implementation of methods get and put in class ArrayHashTable which implements interface HashTable. You will implement linear hashing, which attempts to place a key in the following successive positions h(k) mod N, (h(k)+1) mod N, (h(k)+2) mod N, etc. We can simply say the i-th attempt uses the function (h(k)+i) mod N.The hash function h1 has been initialized in the constructor and the stepping function as well. In addition LinearProbeStep method has been passed with the correct value for the step (check its method step).Use class ToyTest to test your implementation (you can comment out the tests for the classes you have not implemented yet).</li>

   <li><strong>Implementing quadratic hashing, (linear) double hashing, and quadratic double hashing.</strong>Modify your implementation to allow for different in-table collision resolution techniques: linear hashing, quadratic hashing, linear double hashing, quadratic double hashing. This can be done by simply changing the “step” that you move away from the home address h(k). In linear hashing this step is step(i)=i, while for quadratic hashing step(i)=i*i. Linear double hashing and quadratic double hashing uses another hash function h2(k) to calculate the step: step(i,k)=i*h2(k) and step(i,k)=i*i*h2(k), respectively.Within ArrayHashTable the constructor requires a SteppingFunction object, this object should be used to calculate the step for each of the 4 cases, the object takes an int for the i value, a long (may or may not be used, depending on double hashing), and a size for taking the modulus (mod).The stepping function has been initialized in the constructor, but their methods step must be updated to work correctly as they currently return 1 (see classes QuadraticProbeStep, DoubleHashStep, QuadraticDoubleHashStep). Test your code with ToyTest.</li>

   <li><strong>Implementing Hashing with separate Chaining</strong>Here the elements of the hash table are Linked Lists of entries (K,V) where K is a key and V is its associated value. Implement methods get and put for class ChainedHash.If you run out of time during the lab, feel free to skip this part and use this solution (<a href="ChainedHashTable.java">ChainedHashTable.java</a>) so that you can move on to Part 2 and perform the tests there.</li>

  </ol></li>

</ul>

<ul>

 <li><strong>Part 2: Word count problem.</strong>You are given two large texts TheAeneidBook1.txt and TheOdysseyBook1.txt.Your task is to compute the list of different words in the text and the number of times each word occurs.The class HashingTest already implements for you the word parsing from these files, so that you can concentrate on word count.We propose an efficient way of doing this using a Hash Table. Store in the hash table each word found (key K) and its frequency (value V). Given a list of words (with repetitions), go through this list one by one. A new word is added to the hash table with frequency one, while a word already present in the hash table should get its frequency incremented.This should be done by simply using one of the Hashing classes that implement interface HashTable and only calling methods provided by this interface. This code is going to be a loop with a small body to be added inside method HashAndStats(ArrayList words, HashTable table).The main program of class HashingTest takes care of testing it using different collision resolution techniques so that we can compare stats.Run this program and analyze its output.Feel free to play with different table sizes later and compare stats.</li>

</ul>