File: NIT-CS3501\- L7 Function-Oriented Software Design- Prahlad N~~ational Institute of Technology Manipur- Impha~~l   
Software Engineering

Function-Oriented Software Design  
(Lecture 7\) 

Dr. Prahlada Rao B B ANRF PM Professor 

09-09-2026 

CSE Department 

1

S/W Design 

● Design Phase: Transforms SRS document: 

– To a form easily implementable in Programming  Language. 

SRS    
Document Design ActivitiesDesign Documents 

• Design Phase Activities: 

⁃ High level Design 

⁃ Detailed Design Document.

2

1  
Function-oriented Design

● Function-oriented Design techniques are  very popular: 

– Currently in use in many Software  Development Organizations. 

● Function-oriented Design techniques: 

~~subfunctions and so on.~~   
– Start with the functional requirements  specified in the SRS document.  

3

Function-oriented Design

Salient features of FOD approach: 

● A system is viewed as something that performs a set of  functions. Starting at this high-level view of the system, each  function is successively refined into more detailed functions. 

● Each of these sub-functions may be split into more detailed  

● The system state is centralized and shared among different  functions. 

Function-oriented Design Techniques: 

● Start with Functional Requirements specified in SRS  Document. 

4

2  
● ~~SA/SD Techniques~~ are discussed further   
Function-oriented Design

Function-oriented Design: 

● Start with the functional requirements specified  ● SA/~~SD (~~Structured Analysis/Structured Design)    
in the SRS document. 

● Structured Analysis (SA), Structured Design  (SD) Techniques are used. 

● SA/SD methodology can be used to perform  High level Design of a Software. 

5

Introduction 

methodology, has essential features of several ● Function-oriented design methodologies: – If you need to use any specific design  methodology later, 

–You can do so easily with small additional  effort.

6

3  
SA/SD (Structured Analysis/Structured  Design) 

● SA/SD technique draws heavily from the  following methodologies: 

– Constantine and Yourdon's methodology 

– Hatley and Pirbhai's methodology 

– Gane and Sarson's methodology – DeMarco and Yourdon's methodology 

● SA/SD technique can be used to perform

– High-level Design.  

7

Overview of SA/SD Methodology 

● SA/SD methodology consists of two activities: – Structured Analysis (SA) 

– Structured Design (SD) 

● During Structured Analysis:   
– functional decomposition takes place. 

● During Structured Design: 

– module structure is formalized.

8

4  
Functional Decomposition

● Each function is analyzed: – Hierarchically decomposed into more  Detailed Functions. 

– Simultaneous decomposition of high-level  data Into more detailed data. 

9

Function-oriented Design

● Function-oriented Design techniques are  very popular: 

– Currently in use in many Software  Development Organizations. 

● Function-oriented Design techniques: – Start with the functional requirements  specified in the SRS document. 

10

5  
Top-down Decomposition- TDD    
~~decomposed into more~~ detailed Functions.   
During Design Process: 

● High-level functions are successively  

● Successive decomposition of high-level  functions, into more detailed functions is  ● After TDD~~, the different~~ functions    
Technically known as Top-down  Decomposition. 

11

Design Process: 

● High-level functions decomposedinto detailed Functions-TDD

identified are mapped to  

modules, and a module structure  is created.

12

6  
Overview of SA/SD Methodology 

● During Structured Analysis: –The SRS document is transformed  into DFD 

● During Structured Design: –The DFD model is transformed  into a structured Chart 

13

Structured Analysis 

● Transforms a textual problem  description into a Graphic Model. –Done using data flow diagrams  (DFDs). 

–DFDs Graphically Represent the  results of Structured Analysis.

14

7  
Structured Design

● All functions represented in DFD

–Mapped to a module structure. ● The Module Structure: –Also called as the Software  Architecture: 

15

Detailed Design ● Software Architecture: –Refined through Detailed  Design. 

–Detailed Design can be directly  implemented: 

● Using a conventional    
Programming Language.

16

8  
– ~~Arrive at a form that is~~ suitable for    
Structured Analysis vs. Structured  Design 

● Purpose of Structured Analysis: – Capture the detailed structure of the  system as the user views it. 

● Purpose of Structured Design: 

implementation in some programming  language.  

17

Structured Analysis vs. Structured Design

● The results of Structured Analysis can be easily  understood even by ordinary customers: – Does not require computer knowledge. 

– Directly represents customer’s perception of the problem. – Uses customer’s terminology for naming different  functions and data. 

● The results of Structured Analysis can be  reviewed by Customers: 

– To check whether it captures all their Requirements.

18

9  
Structured Analysis 

● Based on principles of: 

– Top-down decomposition approach. – Divide and Conquer principle: 

● Each function is considered individually (i.e.  isolated from other functions). 

● Decompose functions totally disregard what  happens in other functions.   
● Ex~~.To show~~ flow of documents or items in an Organization  
– Graphical representation of results using

● Data flow diagrams (or bubble charts). 19

Data Flow Diagrams 

● DFD is an elegant Modelling Technique: – Useful not only to represent the results of  Structured Analysis. 

– Applicable to other areas also: 

● DFD Technique is very popular: – It is powerful and yet simple to understand and use.

20

10  
Data Flow Diagram

● DFD is a Hierarchical Graphical Model: 

– Shows the different functions (or processes) of the system and 

– Data interchange among the processes. 

21

DFD Concepts 

● It is useful to consider each function asa  processing station: 

– Each function consumes some input data. – Produces some output data.

22

11  
Data Flow Model of a Car Assembly Unit 

Engine Store   
Door Store 

Partly Assembled    
Car   
Fit   
Test Fit   
Fit 

Paint and   
Doors   
Wheels   
Engine   
Assembled    
Chassis  

~~Ca~~r   
Car   
with Engine 

Chassis Store   
Wheel Store 

23

Data Flow Diagrams (DFDs) 

● A DFD model: 

– Uses limited types of symbols. –Simple set of rules 

–Easy to Understand: 

–It is a hierarchical model.

24

12  
● Human mind can easily understand any  
Hierarchical Model 

Hierarchical Model: 

● In a Hierarchical Model: 

–We start with a very simple and abstract  model of a system, 

–Details are slowly introduced through The  Hierarchies. 

25

Hierarchical Model

26

13  
Data Flow Diagrams (DFDs) 

● Primitive Symbols are used for Constructing DFDs: 

External entity   
Process 

Data Flow 

Data Store 

Output 

27

Function Symbol 

● A function such as ‘search-book’ is   
represented using a circle:   
search book

– This symbol is called a process or bubble or  transform. 

– Bubbles are annotated with corresponding  function names. 

– Functions represent some activity: 

● Function names should be verbs. 

28

14  
● External entities s.a a ‘Librarian’ is representedby a  ● External ~~entities are real~~ physical entities external to  represent, ext’l H/W or ext’l S/W ~~s.a another~~ Appl’nExternal Entity Symbol   
rectangle symbol: 

Librarian

● A directed arc (or an arrow) symbol is    
SW System and interact with systemby: – Input data to the System or 

– Consume data produced by the System.   
– data flow occurring ~~bet’n two~~ processes or    
– Sometimes external entities are called terminator,  ~~extl entities~~ in the direction of the arrow.   
source, or sink. 

● In addition to human users, the external entity can  SW, that interact with the System being modelled. 

29

Data Flow Symbol 

used to represent   
book-name

– Data flow symbols are usually annotatedwith  the correspond’g data names of the data they  carry. 

30

15  
Data Store Symbol 

● Represents a logical file: 

– A logical file can be:   
book-details 

● a data structure 

● a physical file on disk. 

– Each data store is connected to a process: ● By means of a data flow symbol.  

– ~~Arrows connecting~~ to a data store need not be    
31

Data Store Symbol 

● Direction of data flow arrow: find-book  
– Shows whether data is being read from or written into it.   
Books

● An arrow into or out of a data store: – Implicitly represents the entire data of the data  store. 

annotated with any data name. 

32

16  
Output Symbol 

● Output produced by the system

33

Synchronous Operation

● If two bubbles are directly connected by  a data flow arrow: 

– They are synchronous 

number  
Read numbers   
Validate numbers   
0.2 Valid    
0.1   
Data items 

number 34  
17  
Asynchronous Operation

● If two bubbles are connected via a  data store: 

– They are not synchronous. 

Read   
Validate numbers   
numbers   
0.2 Valid    
numbers   
0.1 

Data items   
number 35

Yourdon's vs. Gane Sarson Notations

● The notations that we would be following are  closer to the Yourdon's notations ● You may sometimes find notations in books that  are slightly different   
– For example, the data store may look like a box with  one end closed

36

18  
How Structured Analysis Performed?

● Initially represent the software at the  most abstract level: 

– Called the context diagram. 

– Entire system is represented as a  single bubble, 

– This bubble is labelled according to  the main function of the system. 

37

Tic-tac-toe: Context Diagram

Tic-tac toe    
software display 

move

Human Player 

38

19  
Context Diagram

● A context diagram shows: – Data input to the system, 

– Output data generated by the  system, 

– External entities. 

39

Context Diagram

● Context diagram captures: – Various entities external to the system and  interacting with it. 

– Data flow occurring between the system  and the external entities. 

● The context diagram is also called as  the level-0 DFD.

40

20  
Context Diagram

● Establishes the context of the system,  i.e.it Represents: 

– Data sources 

– Data sinks.  

41

Level 1 DFD 

● Examine the SRS document: – Represent each high-level function as  a bubble. 

– Represent data input to every high   
level function. 

– Represent data output from every  high-level function.

42

21  
Higher Level DFDs 

● Each High-level function is separately  decomposed into subfunctions: – Identify the subfunctions of the function– Identify the data input to each subfunction

– Identify the data output from each subfunction● These are represented as DFDs. 

43

Decomposition 

● Decomposition of a bubble: – Also called factoring or exploding. ● Each bubble is decomposed to  
– Between 3 to 7 bubbles.

44

22  
Decomposition 

● Too few bubbles make decomposition  superfluous: 

● If a bubble is decomposed to just one or  two bubbles: 

–Then this decomposition is redundant. 

45

Decomposition 

● Too many bubbles: 

– More than 7 bubbles at any level of  a DFD. 

– Makes the DFD model hard to  understand.

46

23  
Decompose How Long?

● Decomposition of a bubble should  be carried on until: 

– A level at which the function of the  bubble can be described using a simple algorithm. 

47

Ex-1: RMS Calculating Software 

● Consider system RMS calculating  software: 

– Reads three integers in the range of \-1000  and \+1000 

– Finds out the Root Mean Square (RMS) of  the three input numbers 

– Displays the result.

48

24  
Example 1: RMS Calculating Software

● The context diagram is simple to  develop: 

–The system accepts 3 integers from  the user 

– Returns the result to him. 

Figure. ~~Level 0- Context Diagram~~  
49

Example 1: RMS Calculating  Software 

Data items   
Compute 

RMS 

0 

User   
result 

50

25  
Example 1: RMS Calculating Software

● From a cursory analysis of the  problem description: 

– We can see that the system needs to  perform several things. 

51

Example 1: RMS Calculating Software

● Accept input numbers from the  user: 

– Validate the numbers, 

– Calculate the root mean square of theinput numbers 

– Display the result.

52

26  
Figure. Level 1- ~~Context Diagram~~  
Ex.1: RMS Calculating Softwarenumbers   
Read   
Validate 

numbers   
numbers   
0.2   
0.1   
Data items   
Valid \-numbers   
error 

Display 0.4   
Compute rms   
0.3 

result   
RMS 

53  
Figure. Level 2- ~~Context Diagram~~  
Example 1: RMS Calculating  Software 

Squared sum   
Calculate squared sum   
Calculate mean   
0.3.2   
0.3.1 

Valid \-   
Mean square   
numbers 

Calculate root   
0.3.3 

RMS 

54

27  
Figure. Level 3- ~~Context Diagram~~  
Example: RMS Calculating  Software 

a bc Square 0.3.1.1Square 0.3.1.2 Square 0.3.1.3 

bsq   
asq   
csq 

Sum   
0.3.1.4 

Squared-sum

55

Example: RMS Calculating Software

● Decomposition is never carried on up to  basic instruction level: 

– A bubble is not decomposed any further: 

‣ If it can be represented by a simple set of  instructions. 

Upto here  

11-9-2026

56

28  
– ~~grossPay \= regularPay \+ overtimePay~~From here    
Data Dictionary   
15-9-2026

● A DFD is always accompanied by a data dictionary. ● A data dictionary lists all data items appearing in a  DFD: 

– Definition of all composite data items in terms of their  component data items. 

– All data names along with the purpose of the data items. ● For example, a data dictionary entry may be: 

57

Importance of Data Dictionary 

● Provides all engineers in a project with  standard terminology for all data: 

– A consistent vocabulary for data is very important 

– Different engineers tend to use different terms to  refer to the same data, 

● Causes unnecessary confusion.

58

29  
Importance of Data Dictionary 

● Data dictionary provides definition of different data:  in terms of their component elements. 

● For large systems, 

– The data dictionary grows rapidly in size and  complexity. 

– Typical projects can have thousands of data dictionary  entries. 

– It is extremely difficult to maintain such a dictionary  manually.  

59

Data Dictionary 

● CASE (Computer Aided Software Engineering)  tools come handy: 

– CASE tools capture the data items appearing  in a DFD automatically to generate the Data  Dictionary.

60

30  
Data Dictionary 

● CASE Tools support queries: 

– About definition and usage of data items. 

● For example, queries may be made to find: 

– Which data item affects which processes, 

– A process affects which data items, 

– The definition and usage of specific data items, etc. 

● Query handling is facilitated: 

– If Data Dictionary is stored in a Relational Database  Management System (RDBMS). 

61

Data Definition 

● Composite data are defined in terms of primitive  data items using following operators: 

● \+: denotes composition of data items, e.g – a+b represents data a and b. 

● \[,,,\]: represents selection, 

– i.e. any one of the data items listed inside the square  bracket can occur. 

– For ex: \[a,b\] represents either a or b occurs.

62

31  
Data Definition 

● ( ): contents inside the bracket represent  optional data 

– which may or may not appear. 

– a+(b) represents either a or a+b occurs. 

● {}: represents iterative data definition, 

– e.g. {name}5 represents five name data. 63

Data Definition 

● {name}\* represents 

– zero or more instances of name data. 

● \= represents equivalence, 

– e.g. a=b+c means that a represents b and c. 

● \*..\*: anything appearing within \*..\* is consideredas comment.

64

32  
● error:string ~~\*~~ error message\*   
Data Dictionary for RMS Software 

● numbers=valid-numbers=a+b+c 

● a:integer \* input number \* 

● b:integer \* input number \* 

● c:integer \* input number \* 

● asq:integer 

● bsq:integer 

● csq:integer 

● squared-sum: integer 

● Result=\[RMS,error\] 

● RMS: integer \* root mean square value\* 65

Balancing a DFD 

● Data flowing into or out of a bubble: 

– Must match the data flows at the next level of DFD. 

● In the level 1 of the DFD, 

– Data item c flows into the bubble P3 and the data item  d and e flow out. 

● In the next level, bubble P3 is decomposed. 

– The decomposition is balanced as data item c flows  into the level 2 diagram and d and e flow out.

66

33  
Balancing a DFD

cc   
b 

c1   
d1 

d   
a   
e 

Level 1 e1 de   
Level 2 

67

Numbering of Bubbles 

● Number the bubbles in a DFD: 

– Numbers help in uniquely identifying any bubble from  its bubble number. 

● The bubble at context level: 

– Assigned number 0\. 

● Bubbles at level 1: 

– Numbered 0.1, 0.2, 0.3, etc 

● When a bubble numbered x is decomposed, 

– Its children bubble are numbered x.1, x.2, x.3, etc.

68

34  
moves on ~~a 3 X 3 square.~~   
Ex 2: Tic-Tac-Toe Computer Game ● A human player and the computer make alternate  

● A move consists of marking a previously  unmarked square. 

● The user inputs a number bet’n 1 and 9 to mark a  square 

● Whoever is first to place three consecutive marks  along a straight line (i.e. along a row, column, or  diagonal) on the square wins. 

69

Ex 2: Tic-Tac-Toe Computer Game 

● As soon as either of the human player or the  computer wins, 

– A message announcing the winner should be  displayed. 

● If neither player manages to get three  consecutive marks along a straight line, 

– And all the squares on the board are filled up, 

– Then the game is drawn. 

● The computer always tries to win a game. 

70

35  
Ex. Tic-Tac-Toe Computer Game  
Fig. ~~Level 0- Context Diagram~~  
Context Diagram  

Tic-tac toe    
display   
software   
0 

move 

Human Player 

71

Fig. Level-1 ~~Data Flow Diagram~~  
Level-1 DFD 

game 

Display board   
move   
0.1   
result 

Check winner   
Validate move   
board   
0.4   
0.2 

Play move   
0.3 

72

36  
Data Dictionary 

● Display=game \+ result 

● move \= integer 

● board \= {integer}9 

● game \= {integer}9 

● result=string 

73

Summary 

● Discussed function-oriented software design methodology– Structured Analysis/Structured Design(SA/SD) – Incorporates features from some important Design Methodologies. ● SA/SD consists of two parts: 

– Structured Analysis 

– Structured Design. 

● The goal of Structured Analysis: 

– Functional Decomposition of the system. 

● Results of Structured Analysis: 

– Represented using Data Flow Diagrams (DFDs). 

● We discussed how hierarchical model is easy to understand. – Number 7 is called the magic number.

74

37  
Summary 

● During structured design, 

– The DFD representation is transformed to a  structure chart representation. 

● DFDs are very popular: 

– Because it is a very simple technique. 

● A DFD model: 

– Difficult to implement using a programming language: 

– Structure chart representation can be easily  implemented using a programming language. 

75

Summary 

● We discussed structured analysis of two examples: – RMS calculating software – Tic-tac-toe computer game software 

● Several CASE tools are available: – Support Structured Analysis and Design. 

– Maintain the Data Dictionary, 

– Check whether DFDs are Balanced or not. 

15-9-2026 Thank Q76

38