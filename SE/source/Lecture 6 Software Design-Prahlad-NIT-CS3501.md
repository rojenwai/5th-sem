National Institute of Technology Manipur- Imphal   
Software Engineering

Software Design  

(Lecture 6\) 

File: NIT-CS3501\- Lecture 6 Software Design-Prahlad 

Dr. Prahlada Rao B B ANRF PM Professor 

28-08-2026 

CSE Department 

1

Organization 

● Introduction to Software Design ● Goodness of a Design 

● Functional Independence 

● Cohesion and Coupling 

● Function-oriented design vs. Object-oriented  design 

● Summary

2

1  
• Students did not come to Salam campus. No Bus, No Class Onam R Holiday Introduction- S/W Design   
Software Design  (Lecture 6\) 

28-08-2026: 55 Students participated in Hackathon at Longol Campus. 3

● Design Phase Transforms SRS document: 

– To a form easily implementable in some  Programming Language. 

SRS    
Design Documents   
Document Design Activities 

• Design Phase Outcome: 

⁃ High level and Detailed Design Document. 

01/09/2023

4

2  
Items Designed & Docmntd During  Design Phase 

● Module Structure, 

● Control relationship among the modules, – Call relationship or Invocation relationship 

● Interface among different modules,   
– Data items exchanged among different modules, ● Data Structures of individual modules,   
● Algorithms for individual modules. 

5

Module Structure 

• High-level design means identification of modules, control relationships  among them 

• Definition of interfaces among the modules. 

• High-level Design is Represented using: 

⁃ Tree-like diagram called Structure chart 

⁃ To represent control hierarchy HLD • Outcome of HLD is DD:   
⁃ Program structure or 

⁃ Software architecture. 

• During Detailed Design: Data Structure, Algorithms of modules is Designed.  6

3  
Introduction- S/W Design Intro~~duction- S/W D~~esign   
● A module consists of:   
– Several functions 

– Associated data structures. 

D1 ..   
Data   
D2 ..   
D3 .. 

Functions   
F1 .. 

F2 ..   
F3 ..   
F4 ..   
F5 .. 

7

● Good Software Designs: 

– Seldom arrived through a single step  procedure: 

– But through a series of steps and    
iterations.

8

4  
Introduction- S/W Design   
● Design activities are usually classified into  two stages: 

– Preliminary (High-level) Design. 

– Detailed Design. 

● Meaning and scope of the two stages: 

– Vary considerably from one methodology to  another.  

9

High-Level Design ● Identify:   
– Modules 

– Control relationships among modules – Interfaces among modules. 

d1 d2 

d3 d1 d4

10

5  
High-Level Design 

● The Outcome of high-level design: 

–Program structure (or software  architecture). 

11

High-Level Design 

● Several Notations available to Represent High-level Design: 

– Usually a Tree-like Diagram called  Structure Chart is used. 

– Other Notations: 

Jackson Diagram or Warnier-Orr    
Diagram can also be used. 

12

6  
Detailed Design 

● For each Module, Design: 

–Data structure 

–Algorithms 

● Outcome of Detailed Design: –Module Specification. 

13

Classification of Design Methodologies

● Procedural (aka Function-oriented) ● Object-oriented 

More recent: 

● Aspect-oriented 

● Component-based (Client-Server)

14

7  
Does a Design Technique Lead  to a Unique Solution? 

● No:   
– Several subjective decisions need to be  made, to trade off among different  parameters. 

–Even, the same designer can come up  with several alternate Design  

Solutions. 

15

Difference bet’n Analysis and Design 

● The aim of Analysis is to:  

Understand the problem with a viewto eliminate  deficiencies in the Requirement specification: – such as incompleteness, inconsistencies, etc. – The model we are trying to build, not be ready. 

● The aim of Design is to:  

Produce a model that will provide a seamless  transition to the Coding Phase, 

– Once Requirements are Analyzed and found  Satisfactory 

– a Design Model is Created which can be easily  implemented. 

16

8  
Analysis Versus Design

● An Analysis Technique helps to elaborate the  Customer requirements through careful thinking: – At the same time consciously avoids making any  decisions regarding implementation. 

● Design Model is obtained from Analysis model  Thru’ transformations over a series of steps: – Decisions regarding implementation are  consciously made. 

17

Q. Best Designs- How to Distinguish?

● How to distinguish bet’n Superior  of two alternate design solutions?  

● Unless we know what is a good  software design: 

–We can not possibly design one.

18

9  
Good and Bad Designs 

● There is no unique way to design a  system. 

● Even using the same design methodology: – Different designers can arrive at very  Different Design solutions. 

● We need to distinguish between Good  and Bad Designs. 

19

Features of Better Designs 

● Should implement all functionalities of the  system correctly. 

● Should be easily Understandable. 

● Should be Efficient. 

● Should be easily Amenable to change, 

– i.e. easily Maintainable.

20

10  
● Understandability of Design is a    
Which of Two is a Better Design?

major issue to: 

– Determine Goodness of design: 

● A Design that is easy to understand is: –Also easy to maintain and change.  

21

Which of Two is a Better Design?

● If Design is not easy to understand: – Tremendous effort needed to maintain it 

● We know, about 60% effort is spent in s/w  maintenance. 

● If a Software is not easy to understand: – Maintenance effort would increase many times.

22

11  
● Should make use of abstraction and    
Understandability How used in Design?   
● Use consistent and meaningful names: – For various Design Components. 

decomposition principles in ample  measure. 

23

Abstraction and Decomposition Principles:  

● Two principal ways: 

–Modular Design 

–Layered Design

24

12  
Modularity 

● Modularity is a fundamental attributes of  any good design. 

– Decomposition of a problem cleanly into  modules: 

● Modules are almost independent of  each other 

 Divide and conquer principle.  25

Modularity 

● If Modules are independent: 

–Modules can be understood separately, o Reduces the complexity greatly. ● To understand why this is so,   
– Remember that it is very difficult to break a bunch of  sticks but very easy to break the sticks individually.

26

13  
Layered Design 

27

Layered Design 

● Neat arrangement of modules in a  hierarchy means: 

–Low fan-out 

– Control abstraction

28

14  
Modularity 

● In technical terms, modules should  display: 

–High cohesion 

–Low coupling. 

● We shall next discuss: 

– Cohesion and Coupling. 

29

Cohesion and Coupling 

● Cohesion is a measure of: 

– functional strength of a module. 

– A cohesive module performs a single task  or function. 

● Coupling bet’n 2modules is measure of: – Degree of the interdependence or interaction  between the two modules.

30

15  
Cohesion and Coupling 

● A module having high cohesion and  low coupling is: 

– Functionally Independent of other    
modules 

● A functionally independent module has  ● ~~Different modules can easily~~ be understood    
minimal interaction with other  

modules. 

31

Advantages of Functional    
Independence 

● Better Understandability and good Design. ● Complexity of design is reduced. 

in isolation: 

– Modules are independent

32

16  
~~directly affect~~ other modules.   
Advantages of Functional    
Independence 

● Functional independence reduces error  propagation.   
– Degree of interaction between modules is  low. 

– An error existing in one module does not  

● Reuse of modules is possible. 

Upto Here 01/09/2023

33

02/09/2023  
Advantages of Functional    
Independence 

● A functionally independent module easily  be taken out and reused in different  program. 

– Each module does some well-defined and  precise function 

– The interfaces of a module with other modulesis simple and minimal.  

34

17  
Functional Independence 

● There are no ways to quantitatively  
measure the degree of cohesion and  coupling. 

● Classification of different kinds of  cohesion and coupling: 

– can give us some idea reg. the degree of  cohesiveness of a module. 

35

Classification of Cohesiveness

● Classification is often subjective: 

– Yet gives us some idea about    
cohesiveness of a module. 

● By examining the type of cohesion  exhibited by a module: 

– We can roughly tell whether it displays  high cohesion or low cohesion.

36

18  
Classification of Cohesiveness

functional   
functional   
1\.   
1\.   
sequential   
sequential   
Degree of cohesion   
2\. 2\.   
Degree of cohesion   
communicational   
communicational   
3\.   
3\.   
procedural   
procedural   
4\.   
4\.   
temporal   
temporal   
5\.   
5\.   
logical   
logical   
6\.   
6\.   
coincidental   
coincidental   
7\.   
7\. 

• The degree of Cohesiveness increases from Coincidental to Functional ![][image1]37

Coincidental Cohesion 7\.

● The module performs a set of tasks: – Which relate to each other very loosely, if at  all. 

–The module contains a random collection of  functions. 

–Functions put in the module out of pure  coincidence without any thought or design. 

38

19  
● All elements of the module perform~~similar operations:~~   
Logical Cohesion 2\. 

– e.g. error handling, data input, data  output, etc. 

● Ex of logical cohesion: 

– A set of print functions to generate an  output report, arranged into a single  module.  

39

Temporal Cohesion 3\.

● The module contains tasks that are  related by the fact: 

– All tasks must be executed in the same time  span. 

● Example: 

– The set of functions responsible for 

● initialization, 

● start-up, shut-down of some process, etc.  40

20  
Procedural Cohesion 4\. 

The set of functions of the module: 

● All part of a procedure (algorithm) – Certain sequence of steps have to be  carried out in a certain order for achieving  an objective, 

– set of functions defined on an array or a    
● Ex. the algorithm for decoding a message. 41

Communicational Cohesion5\.

● All functions of the module: 

– Reference or update the same data structure ● Example: 

stack. 

42

21  
Sequential Cohesion 6\. 

● Elements of a module form different  parts of a sequence, 

– Output from one element of the sequence  – To achieve ~~a single function~~,   
is input to the next. 

– Example: sort 

search 

display 

43

Functional Cohesion 7\.

● Different elements of a module cooperate: 

– e.g. managing an employee's pay-roll. 

● When a module displays functional cohesion– We can describe the function using a single  sentence. 

44

22  
How 2 Determining Cohesiveness

● Write down a sentence to describe the function  of the module 

– If the sentence is compound, 

● It has a sequential or communicational cohesion. – If it has words like ‘first, next, after, then’, etc. ● It has sequential or temporal cohesion. – If it has words like initialize,   
● It probably has temporal cohesion. 

45

5.3.5 Coupling ? 

● Coupling indicates: 

–How closely two modules interact  or how interdependent they are. 

● The degree of coupling bet’n two modules  depends on their interface complexity. 

46

23  
● There are no ways to precisely determine    
Coupling 

coupling bet’n two modules: 

● Classification of different types of coupling  will help us to approximately estimate: 

– the degree of coupling bet’n two modules. 

● Five types of coupling exist between any two  modules. 

47

Classes of coupling Data Degree of coupling 1.2.3.4.5\.  
Stamp 

Control 

Common 

Content 

![][image2]48

24  
Data Coupling 1\. 

● Two modules are data coupled: 

– If they communicate via a parameter: ● an elementary data item, 

● e.g an integer, a float, a character, etc. – The data item should be problem related: ● Not used for control purpose. 

49

Stamp Coupling 2\.

● Two modules are stamp coupled, 

– If they communicate via a composite data item 

● such as a record in PASCAL 

● or a structure in C 50  
25  
Control Coupling 3\. 

● Data from one module is used to direct: – Order of instruction execution in another. ● Ex. of control coupling: 

– A flag set in one module and tested in  another module. 

51

Common Coupling 4\.

● Two modules are common coupled: – If they share some global data. 

52

26  
Content Coupling 5\. 

● Content coupling exists between two modules: – If they share code, 

– e.g, branching from one module into another  module. 

● The Degree of Coupling increases 

– from data coupling to content coupling.  53

Neat Hierarchy 

● Control Hierarchy represents: – Organization of modules. 

– Control hierarchy is also called program  structure. 

● Most common notation: 

– A tree-like diagram called structure chart. 

54

27  
Layered Design 

● Essentially means: 

–Low fan-out 

–Control abstraction 

55

Characteristics of Module Hierarchy

● Depth: 

– Number of levels of control 

● Width: 

– Overall span of control. 

● Fan-out: 

– A measure of the number of modules  directly controlled by given module.

56

28  
invoke a ~~given module.~~   
– High fan-in represents ~~code reuse~~ and is    
Characteristics of Module Structure

● Fan-in: 

– Indicates how many modules directly in general encouraged. 

57

Module Structure 

Fan out=2   
Fan in=0

Fan out=1Fan in=1

Fan out=0  
Fan in=2

Upto here 02/09/2023

58

29  
08/09/2026

Layered Design 

● A Design having Modules: 

– With high fan-out numbers is not a good  design: 

– A module having high fan-out lacks  cohesion.  

59

Goodness of Design 

● A module that invokes a large number of  other modules: 

– Likely to implement several different functions: – Not likely to perform a single cohesive function.

60

30  
Control Relationships 

● A module that controls another module: – Said to be superordinate to it. 

● A module controlled by another module: – Said to be subordinate to it.  

61

Visibility and Layering 

● A module A is said to be visible by another module B, 

– If A directly or indirectly calls B. 

● The layering principle requires   
– Modules at a layer can call only the modules immediately below it.

62

31  
Bad Design 

63

Abstraction 

● A module is unaware (how to invoke etc.) of  the higher level modules. 

● Lower-level modules: 

– Do input/output and other low-level functions. 

● Upper-level modules: 

– Do more managerial functions.

64

32  
Abstraction 

● The principle of Abstraction requires: –Lower-level modules do not invoke  functions of higher level modules. 

– Also known as Layered Design. 

65

High-level Design 

● High-level Design maps functions  into modules {fi} {mj} such that: – Each module has High Cohesion 

– Coupling among Modules is as low as  possible 

– Modules are organized in a neat    
hierarchy

66

33  
High-level Design 

• f1   
• f2   
d1 d2   
• f3 

• • •    
d3 d1 d4 

• fn 

67

5.5 Design Approaches 

● Two fundamentally different software design  approaches: 

– Function-oriented design – Object-oriented design 

● These two design approaches are radically different. – However, are complementary ● Rather than competing techniques. 

– Each technique is applicable at 

● Different stages of the design process.

68

34  
Function-Oriented Design

● A system is looked upon as something, that  performs a set of functions.   
● The function create-new-library- member:   
● Starting at this high-level view of the system: – Each function is successively refined into more  detailed functions. 

– Functions are mapped to a module structure.  69

Example 

– Creates the record for a new member, 

– Assigns a unique membership number – Prints a bill towards the membership

70

35  
Example 

● Create-library-member function consists of the  following sub-functions: 

– Assign-membership-number – Create-member-record 

– Print-bill 

– Available for reference and updation to several    
● Each subfunction: 

– Split into more detailed subfunctions  and so on. 

71

Function-Oriented Design

● The system state is centralized: – Accessible to different functions, 

● Member-records: 

functions: 

– Create-new-member 

– Delete-member 

– Update-member-record

72

36  
Function-Oriented Design

● Several function-oriented design approaches  have been developed: 

– Structured design (Constantine and Yourdon,  1979\) 

– Jackson's structured design (Jackson, 1975\) 

– Warnier-Orr methodology 

– Wirth's step-wise refinement 

– Hatley and Pirbhai's Methodology  

73

Object-Oriented Design 

● System is viewed as a collection of objects (i.e. entities). ● System state is decentralized among the objects: – Each object manages its own state information.

74

37  
Object-Oriented Design- Example  
● Cannot directly refer to or change data of    
● Library Automation Software: – Each library member is a separate object 

● With its own data and functions. 

– Functions defined for one object: other objects. 

75

Object-Oriented Design

● Objects have their own internal data: 

– Defines their state. 

● Similar objects constitute a class. 

– Each object is a member of some class. 

● Classes may inherit features 

– From a super class. 

● Conceptually, objects communicate by  message passing. 

76

38  
OOD vs Function-Oriented Design

● Unlike function-oriented design, 

– In OOD the basic abstraction is not functions  such as “sort”, “display”, “track”, etc., 

– But real-world entities such as “employee”,  “picture”, “machine”, “radar system”, etc. 

77

Object-Oriented versus Function   
Oriented Design 

● In OOD:   
– Software is not developed by designing  functions such as: 

● update-employee-record, 

● get-employee-address, etc. 

– But by designing objects such as: ● employees,   
● departments, etc.

78

39  
Object-Oriented versus Function   
Oriented Design 

● Grady Booch sums up this  

fundamental difference saying: – “Identify verbs if you are after  procedural design and nouns if you  are after object-oriented design.” 

79

Object-Oriented versus Function   
Oriented Design 

● In OOD: 

– State information is not shared in a  centralized data. 

– But is distributed among the objects of  the system.

80

40  
Example: 

● In an employee pay-roll system, the following  can be global data: 

– employee names, 

– code numbers, 

– basic salaries, etc. 

● Whereas, in object oriented design: – Data is distributed among different employee  objects of the system. 

Upto here  

08/09/2026  
81

Object-Oriented versus Function Oriented Design 

● Objects communicate by message  passing. 

– One object may discover the state  information of another object by  interrogating it. 

82

41  
Object-Oriented versus Function   
Oriented Design 

● Of course, somewhere or other the  functions must be implemented: – The functions are usually associated with  specific real-world entities (objects) 

– Directly access only part of the system state  information. 

83

Object-Oriented versus Function   
Oriented Design 

● Function-oriented techniques group  functions together if: 

– As a group, they constitute a higher level  function. 

● On the other hand, object-oriented  techniques group functions together: 

– On the basis of the data they operate on.

84

42  
Object-Oriented versus Function Oriented Design 

● To illustrate the differences between  object-oriented and function-oriented  design approaches, 

– let us consider an example \--- 

– An automated fire-alarm system for a  large building.  

85

Fire-Alarm System

● We need to develop a computerized fire alarm  system for a large multi-storied building: – There are 80 floors and 1000 rooms in the building.

86

43  
Fire-Alarm System

● Different rooms of the building: – Fitted with smoke detectors and fire  alarms. 

● The fire alarm system would  monitor: 

– Status of the smoke detectors.  

87

Fire-Alarm System

● Whenever a fire condition is reported by any  smoke detector: 

– the fire alarm system should: 

● Determine the location from which the fire condition  was reported 

● Sound the alarms in the neighboring locations. 

88

44  
Fire-Alarm System

● The fire alarm system should: –Flash an alarm message on the  computer console: 

● Fire fighting personnel man the  console round the clock.    
fire fighting personnel reset the    
89

Fire-Alarm System

● After a fire condition has been  successfully handled, 

–The fire alarm system should let  alarms.

90

45  
Function-Oriented Approach: 

● /\* Global data (system state) accessible by various functions \*/ BOOL detector\_status\[1000\]; 

int detector\_locs\[1000\];   
BOOL alarm-status\[1000\]; /\* alarm activated when status set \*/  
int alarm\_locs\[1000\]; /\* room number where alarm is located \*/  
int neighbor-alarms\[1000\]\[10\];/\*each detector has at most\*/ /\* 10 neighboring alarm locations \*/ 

The functions which operate on the system state: interrogate\_detectors(); 

get\_detector\_location();   
determine\_neighbor();   
ring\_alarm();   
reset\_alarm();   
report\_fire\_location(); 

91

Object-Oriented Approach: 

● class detector   
● attributes: status, location, neighbors ● operations: create, sense-status, get-location, ● find-neighbors   
● class alarm   
● attributes: location, status   
● operations: create, ring-alarm, get\_location,   
● reset-alarm   
● In the object oriented program,   
– appropriate number of instances of the class detector and alarm should be created. 

92

46  
Object-Oriented versus Function   
Oriented Design 

● In the function-oriented program : – The system state is centralized – Several functions accessing these data  are defined. 

● In the object oriented program, 

– The state information is distributed  among various sensor and alarm  

objects. 

93

Object-Oriented versus Function   
Oriented Design 

● Use OOD to design the classes: –Then applies top-down function  oriented techniques 

● To design the internal methods of    
classes. 

94

47  
Object-Oriented versus Function   
Oriented Design 

● Though outwardly a system may appear  to have been developed in an object  oriented fashion, 

– But inside each class there is a small  hierarchy of functions designed in a top 

down manner. 

95

Summary 

● We started with an overview of: 

– Activities undertaken during the software design phase. 

● We identified: 

– The information need to be produced at the end of the design phase, 

– So that the design can be easily implemented using a programming language. 

● We characterized the features of a good software design by introducing the  concepts of: 

– fan-in, fan-out, 

– cohesion, coupling, 

– abstraction, etc. 

● We classified different types of cohesion and coupling: – Enables us to approximately determine the cohesion and coupling existing in a  design. 

● Two fundamentally different approaches to software design: – Function-oriented approach 

– Object-oriented approach 

● We looked at the essential philosophy behind these two approaches – These two approaches are not competing but complementary approaches. 

96

48

[image1]: <data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAWcAAAA/CAYAAAA8EgmjAAAaVUlEQVR4Xu2dd5AVRdfGX//SstQq/zWWKIVlQMUcECOIYiKIiCRFQUEFEwpIMGIWBEQBESMSFQEDwkoSMQcwIUkRVBAzZud7f/35jGcPc/fuRdh7990+VU/dOzMdTp8+/XRP90zPf5IoUaJEiVJy8h9/IkqUKFGiFF8iOUeJEiVKCUok5yhRokQpQYnkHCVKlCglKJGco0SJEqUEJZJzlChRopSgRHKOEiVKlBKUvOT8559/lsNff/1VrVFqZfD2LUX9/vjjjxT2fKnpmgvVSdeqhPe76mgn+aXXvRTL4e3sQRgrlSLnl19+OeCBBx5IRowYUe0xZMiQ5O677w7w16oK2BLccccdyW233ZYMGzYswIcrFdx5550BgwcPToYPH77B9VKEbHrXXXdVG52LAfyQtnDvvfcG+OulCupUuP/++5N77rlngzClBunL/9GjRyffffddgAjaSiTnjOtVgUjOmx+RnCuHSM5Vh01Kzgy1u3fvHtC3b9+QYHXHDTfckBx66KEB/loxcMghh6QNw18rBTz00ENJnTp1AiBnf71UASmDvfbaKxk1atQG1yP+wRVXXJG0bNkyQOeod+DDlhKk48CBA5PDDz+8WugM0LFBgwbJp59+GrBR5IxceeWVAQsWLCg3/0hi+tV/O7eSb54l67o9p7R///33AKVf0TyOP+f15frbb7+dnHXWWQH54utcZfPzx9ZOWTYjPHqsXr06wKcPKLvPw+pj08sKY3XSsSRXOOmr80cddVTAl19+WS6drLw9fL3Z+Prv4whWV+nr43tI9xUrVgQcc8wx5XTICp+VptU567xNw4e1sLornrVblg2z8vXX/bENb6/7sMDnOWXKlOTWW28N8Pla3wXeH20+trxevH7Wx2w+XjdfNoW111auXJm0atUqM74N78XmkZWnP+fT87plxcsCNmzdunXy2WefBei8lUqR81VXXRUAOf/222+pAfj/1VdfpUNzGdoq+M033yQ//PBDgK0IW0jhxx9/TL7++utyBuaYfJSvja//Ng1vQLBu3bqAX375JZzPImd1APYWozIg/VWrVpXTOQu//vprwNq1a8s5N/oyWhE5S981a9YEEH79+vXlwnsbSw/l78N4m2XBpkOesjnnkPr16wd88cUX4Rw6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>

[image2]: <data:image/png;base64,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gFenoyfy3FVUpeW3yHtPIpZbVR50PwX8t0XLCbhvbBiH/sIqyIjk1v8qtYxNv1rdE0bmDdqnEVYhGrhPr28MCrcziH78tU+P/9+79+wufPy+XKrSoDrw1/XqtStQePrf568qLYMSsXyUDtX/7xG+7GIZ+vT7fPxe89LqaDkB9wYTDaUK3p1vKL6xeOPrLgi3ynirDDgav9z7dPr0VoVRBZ+/SJ/fWH5Ku4+/O6hKv+IQJdo+bnWoPZEG4MvDl0tMS0/F1xXUq6eqchMHN3x5VjHa0+8l3b0RLS3gMhY/gq6ib6Tffvtt7Veio+HB7oI4fv31V6M33ioDVl68gFTNEPx1ZxDz5MvB31e5+fg9u4tYD8qP4lXcKi+e+fpU+XUXMf56+VcZDWr48o/1EMuvJ8qju1A6fJpF1WNVHhI9jxTwwO5CRpwCngLeWfjyj/UQy68nyqO7UDp8msUU8EGLlhTw2Bivv/564yabbNKOm266adl4443LbbfdZnznnXfKNNNMU3bZZRfjL7/80s4AqxpMM3g38k+48MorryyHH354efLJJ40xbPHLL7809u3bt+yxxx7l2GOPNb7yyivtGkf05+P1af/ggw+MRx11VFl88cXLXHPNZdxqq63K008/3a5xUQ7PPPOMMTbIGF9XGdMF6UD33Xdf44svvmjldN555xnnnnvusvfee9fqhzTFMBsxxuXvw7feeqv079+/dn3++eeXCy+8sF0Zc78RfHi67g59XTz33HNl6aWXLosuuqjxs88+q5unrrCqHurRu2vm7+abby4nnHBCrSM89dRTy1VXXdWuLLtiR43igomOaDkBB7FSjzjiCONQQw1lgrX11lu34+2332784Ycfyt13311eeOEFoww0GpzuazRcD8QfGz98/vnnjeOOO66l6eyzzzZGg8Ttd999Z8IKRx111LLUUkuV8cYbzzj99NMXBKcqDhm7fwbff//9ssQSSxg32mgjy/dDDz1k3G233coMM8xQXnrpJSOjpdlnn73cddddxnrhx/JoxKq0qoHzP3VwyimnGN98883y4YcfljnnnNN41llnmcged9xxxtdff71d2AojxuFH9P5az+k04AYbbFCuvvrqmt8bb7yx3HTTTbVr1YnItR+hx/KJ5eHjlH+fXv2v57qvGQidFmlUh1o1wIj+FY/i8un1fj19muN1VXwakOieF+z11luv9vzyyy+39hX9x+tm8VXdh4mO6HUCftFFF3WoePGLL74oJ510UrnllluM+GcpRdeMfg899NByxRVXGI8//ngT+nqoMjQEasMNNzSOP/74lqZzzjnHWCXgCPQiiyxi3HbbbcvPP/9c9t9/f+MwwwxjjULhf/LJJ+Wjjz6qNaAoONw7+OCDy4orrmhkBOcbEJ3FlltuWU477TQjfmaZZZZy5513GnHz6aef1q5JM6Ms7kGeE8ezzz5rvPTSS00QyYNGtjzXNaOxiy++uLz88stGntHQNSP5+OOPTUCnmGIKI6Nh7j3xxBPGzz//3OKkTOGDDz5o4d1///3G77//3p7/+OOPxkceeaRccMEFVmbwjTfeMGFUeuedd16bEb377rtGOgs6EZXPTz/9VB5//PHSd8BMCDJr0ygYKg78QOK49tprrU6gbEHuVT8SaNJA+q+77jojnS3uVT7LLrts2X777W1mAqtsWOUAyWu/fv1qS4K4x35UvpQnnRR2A/FPmalD13KHOrinnnrKnmtGSCdCmgkHUuaUgcoLAV933XVr+SMPbW1tNft87LHHbCZIHcPLLrvMys3bLzZ57733GinzV1991eoAfvXVV+3sN9ERKeAp4Cng/yufFPAU8FZDrxNwjIppOaRRYZgyAIxnxBFHtGkq5N7JJ59c/vCHPxhnnHFGW4KZYIIJjEMPPbQ1knqIjYvwaPQTTjihcaeddirDDjusLQ3AKOBQjQ4iIPxV+vB7xx131MLfdNNNyworrFC+/vprow8D0igQZHUYuqfnhEGDUXxczzrrrLUlFBr5GmusUVZbbTXjPvvsU+aff/6y5pprGgmLKTJr1ZAlGZZpFltsMaPWmOebbz4jYkQZsGwDH330UetEEVJ4ww032Jr3OOOMY6TTQ3hY1oF0IqSTdEA6ub322qvW4dFZkabDDjvMuNBCC1l4q6++upF1f/YRJECTTTaZieTDDz9s3H333c29BIg9A9K15557GinrlVde2dIMEdw+ffrYOjVk2Ys4FR914u1BQoUwQZaJdt55ZxM9iK2xlIWoQ5bMFlxwwXLuuecatYQiItJ07LiBlAnlfOiAQQekrFiammeeeYy77rqr1SN5huwBUR4TTzyxEVvALrSkRpiI8D333GOcZJJJyvLLL19rXwsssEA55phjavZDXOuvv37terPN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>