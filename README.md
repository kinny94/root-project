# Root Coding Challenge

# Overview
Question - Process the input file with the given data and generate a report containing each driver with total miles driven and average speed. Sort the output by most miles driven to least. Round miles and miles per hour to the nearest integer.

I have complete the assignment using JavaScript and Nodejs. My implementation also uses some npm modules like Mocha and Chai for testing the file. The program uses the input.txt file in the root directory. However the program is quite flexible, if you wanna try the program with some other test cases. Just add the other test file of '.txt' format to the root directory and run the command **node index.js filename**. ( Replace "filename" with name of the test file ). 

# File Structure
* node_modules ( Once the **npm install** command is executed )
* .gitignore	
* index.js	( main solution file )
* input.txt 	( Input file with provided input from the gist )
* package.json	
* package-lock.json
* README.md ( Documentation about the program )
* test.js ( A file containing all the test cases )
* utils.js ( File containing all the necessary methods )

# Excecution
Inorder to run the program, you need to make sure that Node is installed in your System. You can  install node from [here]( https://nodejs.org/en/ ). Once Node is installed on your system, you need to run the following commands.

1. npm install
2. npm test
2. npm start

* npm start will run both the test cases and the entire program.
* **NOTE: I would recommend pasting the custom input in the input.txt file and then run the *npm start* command. If are using a different input file with a name different than *input.txt* then you have to write the command *node index.js inputFileName.txt* in order to run it.**

# Thought Process

To keep the program as simple as possible, I have used OOPS concepts and added modularity to the program. This makes testing of the modules much easier and also allows you to modify the functioning of the program easily. All the important functions that I have used are in the **utils.js** file. In order to explain my thought process, I would first explain the functioning of a few functions that I have created.

###### calculateTime( startTime, endTime ) : 
This function takes two arguements which is the start and end time of a trip in a String format. The String is converted into Date first and then the time is extracted from that Date using the *getTime* function of the Date class. Then the difference between these two time is calculated and the time of the trip is returned in hours.

###### calculateSpeed( startTime, endTime, miles ) :
This function takes three arguments, the start time of the trip, the end time of the trip and number of miles covered in that trip. The function uses the **calculateTime** function to get the overall time of a trip. This time is then used to calculate the average speed of of the trip by dividing the miles covered by total time of the trip.


#### Program Functioning:-

Firstly, I am checking if the user is using the provided test case in the input.txt file or if he is using his own test file using the **node index.js filename** command. Then, I am reading the entire input file and storing it in a variable **data**. 

I split the data by a line break and then each line to an array **allLines**. I then pass this array as a function parameter to the function **getAllTripData( )**.

###### getAllTripData( linesInInputFile ) : 

**Function output:-** This function takes an array of all lines in the input file and returns an object with driver's name stored as a *key* and an array of their trip details stored as a *value* to that particular driver key. The function returns an object in the following format.

```
obj = {
	Dan: [0.5, 17.3], [0.3333, 21.8]],
    Alex: [ [1.25, 42.0] ],
    Bob: []
}
```

**Working :-** If the line is the array is an information about a driver, it creates a new *key* with that drivers name, and if it's an information about a trip, then it adds that trip to the value array with necessary information. This function calculates the total time of a trip by using the **calculateTime** method and then calculates the average speed of that trip using the **calculateSpeed** method. Using these two methods the function makes sure that there are no trips added to the array stored as *value*, which has a speed less than *5mph* and more than *100mph*.

After, that I traverse over this object and calculate the total time of all the trip and the and total distance travelled by the driver in all the trips. I then calculate the average speed from the overall distance and overall time and manipulate the object received from the **getAllTripData()** function and store an value of a key, for a particular driver, as an array containing the total miles travelled as the first element and the average speed as the second parameter, as in the following format.

```
obj = { 
	Dan: [ 39, 47 ],
    Alex: [ 42, 34 ],
    Bob: [0, 0 ]
}
```
This object is then passed to the **sortingAnArrayOfObject()** function as a parameter.

###### sortingAnArrayOfObject( object ):
This function takes an object as a parameter and sorts the object in a descending order based on the first value ( 0 index ) of the array stored as a value, which is the total number of miles traveled, and returns an array with sorted data in the following format. The function returns a sorted array formed from the above object, with *keys* stored as the first element of the array and *value* stored as the second element of the array.

```
[
	['Alex', [ 42, 34 ] ],
    ['Dan', [ 39, 47	] ],
    ['Bob', [ 0, 0 ] ]
]
```
This array is then passed to the **printResult** function as a parameter.

###### printResults( arrayOfData ) :
This function takes an array of processed data and manipulates it to print the data in a way given in the gist.


# Testing

I have used two Javascript libraries namely **Mocha** and **Chai** for testing. I hhave implemented unit testing to test all the modules in the **utils.js** file. 
All the tests are defined in the **test.js** file and they make sure that each function returns and do what they are supposed to.

In order to run the test file, just run the command **npm test**.
**npm start** will also run all the test cases automatically.

