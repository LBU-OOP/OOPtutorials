# Arrays and ArrayLists

## Introduction
All programming languages have simple variables. The reason is for efficiency. You need an appropriately sized “box” to store your data. If it isn’t then your program will run much more slowly (a problem if like a game it’s doing billions of calculations a second). Some languages like Python are dynamically typed and make the selection of what variable type to use for you, "under the bonnet", meaning that you don't see it going on (but it is). They do this by inferring it from the data you are putting in,

````
Max_Capacity = 17
````
17 is an integer, so it can infer that it should allocate an integer. But then you do:

````
Max_Capacity = 18.5
````
18.5 is a real number, so Python would deallocate the original integer, reallocate a real number data type (double) and assign the value. This is four steps, each of which takes time.
In Java, which is statically typed, WE decide on the datatype, so we’d have to realise that later on we want to store a real value there and allocate a double in the first place (or be forced to store the second one in a different variable).
````
double Max_Capacity = 17;
then later on
Max_Capacity = 18.5;
````
It’s more efficient because it takes fewer steps, it’s clearer because nothing is happening that we don’t explicitly do ourselves and see, but the drawback is that we have the responsibility. In Software Engineering, clarity is always preferable over convenience because we might have to work with other peoples' code and other people will have to work with ours.
We have also seen that we can make more complex data, like a database record, where we can group data items together into a class. A good example is Time, we have hours, minutes and seconds to represent one particular time. This is also a good example because, unlike a database, we can also attach functionality to our classes in the form of methods. So for Time we would need functionality to add and subtract times, because it isn’t a simple matter of just adding etc (i.e. add one second to 23:59:59).
But so far we have only had a single data item at a time. We can crreate multiple data items and process them together using loops by using arrays. Most languages call these data structures arrays but programmers of languages like Python and LISP might think of them as lists.
## Simple Arrays
An array has several advantages. Imagine someone asks you to write a program to calculate the average score of everyone in class. Without arrays, you would have to create a variable for each person you wanted to use in your average calculation. Ok for a class, but you are going to start to complain when we then ask you to do it for your course and you are going to throw a wobbly if we ask you to do it for the university. Arrays make this task easy, and it doesn't matter how many people we have to do it for, it makes no difference. This is because:
1 We can allocate as many as we need in one go.
2 We can process however many there are with a single loop.
In Java we should think of each type having an extra array type, denoted by square brackets, so,
int is integer and int[] is integer array.
double is double precision floating point (real) and double[] is double precision floating point array.
An array in languages like Java is an object type, so we declare it using the “new” keyword.
````
int[] markss = new int[5];
````
The part before the = tells us the type and name (notice that the name is a plural because there will be many), the name is a reference used to connect it to the array object. The part after creates the actual array (an object) and the part in the brackets tells us how big our array is, here five cells or elements, 0,1,2,3,4. This is static typing again, as we have to decide how big it is right now. 
The above line gives us
````
marks[0]
marks[1]
marks[2]
marks[3]
marks[4]
````

Copy and paste this code into a program and run it, and see what happens.
````
int[] marks = new int[5];
marks[0] = 55;
marks[5] = 99;
````

You will see that when you run it you will get an ArrayIndexOutOfBounds Exception.
This is an example of an exception that should never occur (i.e. it’s not like trying to open a file that doesn’t exists that you should add code to deal with). Here The allocation didn’t give me the sixth element marks[5], because I didn’t ask for it. My mistake. If I’d asked the user which element they wanted to use then I should have used an if statement to make sure it wasn’t out of bounds. Here I know the bounds as I decided, so I can programmatically do something about it. With the file not found example, I can't.

Try changing the value in the index to negative values and you’ll see you get the same thing.

To create and Array of doubles I would:
````
double[] distances = new double[100];
````
This would give 100 “elements” distances[0] to distances[99]

So far so good.
Some operations can return arrays as a result. The String class has a method that allows us to split a string on a character, so for example, we could split a sentence on a space and get all the words back individually. In this case we don’t know at development time what length the sentence is (if we are asking the user to type one in). Instead, the split method of string will get to find that out at run time and it makes the appropriately sized array, so all we have to do is tell it the array reference we want it to use:
````
        Scanner myScan = new Scanner(System.in);
        System.out.println("type in a sentance");
        String sentence = myScan.nextLine();
        String[] words;
        words = sentence.split(" ");
        for (int i = 0; i < words.length; i++)
        {
            System.out.println("word "+i+" is "+words[i]);
        }
````
We are doing several things here. Using Scanner should not be unfamiliar by now, but we don't know how many words are in the sentence until RUNTIME, as it depends upon what the user types in and we don’t know that as we are writing the program. Once they have typed something in and the line to split the text is executed (and remember that the split method is part of the string class) and by then it DOES KNOW and can allocate the correctly size array. We can find out what this is because all arrays have a length property. Here it is:
````
words.length
````
We use this in a for loop to iterate one by one over each element, starting at the first and finishing at the last. The brilliant thing is that we can index the array using a variable and here I am using the loop control variable (I’ve called it “i” out of convention, it stands for iterate, but I could have called it anything).
### ForEach loop
It is a very common thing to iterate over an array, starting at the beginning, going one at a time and finishing at the end. Above I have done that by setting the loop control variable (i) to start at the first element (0), I then set it to go up by one each time around the loop (i++ is short hand for i=i+1), and make it stop when the condition fails, i.e. it reaches the last element and i < words.length becomes false. I like that as a lecturer, because I’ve been able to explain it step by step. But, I might make a mistake (commonly putting <= instead of < and then I’d get an OutOfBounds Exception (try it)). Because it is so common to do this the For Each loop is provided to do it for us.

Replace the loop in the example program with:

````
  for (String word : words )
  {
      System.out.println("word is "+word);
  }
````
Here the ForEach loop (yes it is still only spelt “for”) takes a variable declaration to receive an item from the array each time around the loop (String word). We then tell it the array we are iterating over (words). So each time around the loop, “word” gets the next element in the array. Try it.
.
## Arrays Of Objects
[The full example code is here.](https://github.com/LBU-OOP/OOPexampleCode/blob/main/ArrayListExample.java)
So far we have looked at simple arrays of cardinal datatypes (ok for those paying attention String isn’t actually a cardinal datatype but it is shortcutter to behave like one). We can also have arrays of Objects. So we could create a class Time and have an array of Times.

Assuming a definition for Time.Java in our project.
````
Time appointments = new Time[100];
````
That’s fine and it works just the same, and as stated above, we’ve actually already done it because String is a class.
The problem comes when we want to do extra things, like sort our array. It’s easy for integers, just sort biggest to smallest, or smallest to biggest. For string just sort alphabetically etc. But when we have more complex classes it is not always obvious.

Say I have a class to represent a bike rider.
````
public class Rider
{
    string name;
    string team;
    string category;
    Int wattsPerKilo;   
}
````
Interesting note: Watts Per Kilo is how string a rider is. A more muscular and heavy rider will generally be able to produce more watts because they have bigger muscles, but their extra weight will drag them back on the climbs.  Watts per kilo divides their weight by how much power they can produce (in watts). It give a better representation of how fast a rider will go (especially up hill).
The question is, how do we sort riders? On name? On Team? On wattsPerKilo? The answer is any and maybe all depending on the circumstances. The upshot is that Java Standard Libraries (and it’s the same for all languages), while wanting to be helpful can’t possibly provide generic sorting abilities. But what they can do is allow us to tell it how to compare two objects and then sort based on that.

So here we could provide a method to compare two Rider objects an any of those attributes. We could do one for each attribute and we could even do one that used multiple attributes. We can then use one of the standard collection classes to do the actual sorting. Enter ArrayList.
ArrayList is one of the standard collection, there are others such as Vectors, Stacks, LinkedLists, HashTables etc. They all exploit polymorphism and the fact that all classes have a common root in an inheritance hierarchy.
Remember that you can use the “extends” keyword to make one class inherit from another. But if you don’t extend anything then it is as if you had extended the class Object (I really wish they’d called it something else as we already use the term Object to mean something slightly different). In the Riders example above it is exactly as if we’d typed.
````
public class Riders extends Object
````
The upshot is that every Java class (same for C#/C++) every made or every will be made IS AN OBJECT. This means that we can have an array of Object and put any an object (small o) of any class at all in it. This is because a reference to Object can be attached to an object of any class. This means that languages like Java can provide standard collection classes because they are just collections of Object.

For our example I am going to compare on wattsPerKilo.
````
class RiderComparitor implements Comparator <Rider>
	{
		public int compare(Rider one, Rider two)
		{
			if (one.wattsPerKilo > two.wattsPerKilo)
				return 1;
			else if (two.wattsPerKilo > one.wattsPerKilo)
				return -1;
			else
				return 0;
		}
		
	}
````
Here I am implementing the Comparator interface. This ensures that I have the method that ArrayList is going to call to do the sorting. The <> notation allows us to restrict what we are operating on. ArrayList can work on anything because everything drives from Object, but we might not want to be so flexible, as being overly flexible can lead to unknown problems, always err on the side of clarity. So here we restrict it to classes of Rider and classes that extend from that by putting <Rider>.

The code then says what to do with two Riders objects, which one wins, as it were? If the first of the two riders has the better wattsPerKilo then they win (1), if they have worse then they lose (-1), or if it’s the same it’s a draw (0). The ArrayList Sort method just repeatedly calls this method to see how it should compare two objects and it then sorts them (look up Bubble Sort if you are interested in the sorting algorithm itself). The key point is that it is up to you, the designer of the Rider class, how two riders objects are compared.

The main code looks like this (the main example on the link above has more riders, I've removed them for brevity).
````
public ArrayListExample()
	{
		ArrayList<Rider> riders = new ArrayList();
		Rider r1 = new Rider("Geraint Thomas", 11, 5.8f);
		Rider r2 = new Rider("Simon Yates", 15, 5.9f);
		Rider r3 = new Rider("Jonas Vingegaard", 14, 6.5f);
		Rider r4 = new Rider("Tadej Pogacar",918,7.5f);
		riders.add(r1);
		riders.add(r2);
		riders.add(r3);
		riders.add(r4);
		Collections.sort( riders, new RiderComparitor());
		for(int i = 0; i<riders.size(); i++)
		{
			Rider r = (Rider) riders.get(i);
			System.out.println("Rider = "+r.name+" has "+r.wattsPerKilo+" watts/kg");
		}
		
	}
	
````
An ArrayList is created that restricts entries to objects of Rider and classes that may extend Rider. 
After the ArrayList line add the line.
````
Object o = new Object();
riders.add(o);
````
You will get a syntax error on the second line because you are trying to add something above Rider in the hierarchy (an object of the class Object). In this case we want this to happen because this is an ArrayList with associated code to deal with Riders, we don’t want Strings and Times ever being in there (the key Software Engineering principle is that this code could be reused in the future and we don’t want our main code crashing in the future because it can’t compare wattsPerKilo of a Time!). If you remove the \<Rider\> from the ArrayList declaration, you will have removed the restriction and the syntax error will disappear. Quick! Put it back, we aren’t writing sloppy Python here!
Once the riders have been added it uses a single line to sort it (ok here there are only four but there could be 2002).
````
Collections.sort( riders, new RiderComparitor());
````
This uses the code we saw above RiderComparitor to sort the riders ArrayList. It then loops around the riders ArrayList (we could have used a forach loop) and outputs each element, which is now in order of WattsPerKilo, with Tadej Pogacar at the top.

