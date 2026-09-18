File: NIT-CS3501\- ~~Lecture 3- Requirements Analysis and Specification \-Prahlad~~ ~~National Institute of Technology Manipur- Impha~~l   
Software Engineering 

Requirements Analysis and Specification  (Lecture 3\) 

Dr. Prahlada Rao B B ANRF PM Professor 

12-08-2026 

CSE Department 

1

Requirements Analysis and Specification   
Organization  

1\. Introduction 

2\. Requirements Analysis 

3\. Requirements Specification 4\. SRS document 

5\. Decision Table 

6\. Decision Tree 

7\. Summary

2

1  
● Building, ~~without determining~~ what the    
Projects Fail ? 

Many projects fail: 

● Because they start implementing the system. 

customer really wants. 

It is important to Learn: 

● Requirements Analysis and Specification  Techniques carefully. 

3

Requirements Analysis and Specification (RAS) 

● Goals-Requirements and Specification Phase: – Fully understand the user requirements. 

– Remove inconsistencies, anomalies..etc, from  requirements. 

– Document requirements properly in SRS Document. ● RAS consists of two distinct Activities: – Requirements Gathering and Analysis – Specification

4

2  
Who Carries out Requirements Analysis and  Specification? 

● The person who undertakes requirements analysis and specification: 

– Known as Systems Analyst: 

– Collects data pertaining to the product – Analyzes collected data: 

● To understand what exactly needs to be done. 

– Writes the Software Requirements Specification (SRS)   
document. 

5

Requirements Analysis and Specification-Outcome

● Final output of this phase: 

– Software Requirements Specification (SRS) Document. 

● The SRS document is reviewed by the customer. 

– Reviewed SRS document forms the basis of all  future development activities.

6

3  
Requirements Analysis-Activities 

● Requirements Analysis consists of Two main activities: 

– Requirements gathering 

– Analysis of the gathered requirements 

7

Requirements Gathering 

● Analyst gathers requirements through: – Observation of existing Systems. – Studying existing Procedures. 

– Discussion with the Customer and End-users, – Analysis of what needs to be done, etc.

8

4  
Requirements Gathering 

● Also known as Requirements Elicitation. ● If Project is To automate some existing procedures

Eg. Automating existing manual accounting activities, 

● The task of system analyst is a little easier ● Analyst can immediately obtain:   
– Input and Output Formats 

– Accurate details of the Operational Procedures  9

Requirements Gathering Activities 

1\. Studying the existing documentation 2\. Interview 

3\. Task Analysis 

4\. Scenario Analysis 

5\. Form Analysis

10

5  
Attributes of Good System Analyst 

● In the absence of a working system, 

– Lot of imagination and creativity are required. 

● Interacting with customer to gather relevant data:

– Requires a lot of experience. 

● Desirable Attributes of a Good System Analyst: – Good interaction skills, 

– Imagination and creativity, 

– Experience. 

11

Case Study: Automation of Office Work at CSE Dept.

● The academic, inventory and financial information at CSE department: 

– Being carried though manual processing by two office clerks, a store keeper and two attendants. 

● Considering the Low Budget he/she had at his/her  Disposal: 

– The HoD entrust the work to a Team Of Student  Volunteers.

12

6  
Case Study: Automation of Office Work at CSE Dept.

● The team was first briefed by the HoD about the  specific activities to be automated. 

● The analyst first discussed with the two clerks: – Regarding their specific responsibilities (tasks) that  were to be automated. 

● The analyst also interviewed student and faculty  representatives who would also use the software. ● For each task, they asked:   
– About the steps through which these are performed.

– They also discussed various scenarios that might  arise for each task. 

● The analyst collected all types of forms that were 

being used. 

13

Analysis of the Gathered Requirements 

● Main purpose of Requirements Analysis: – Clearly understand the User Requirements 

– Detect Inconsistencies, Ambiguities and  Incompleteness. 

● Incompleteness and Inconsistencies: – Resolve through further discussions with the  end-users and the customers. 

14

7  
Inconsistent Requirement 

● Some part of the requirement: – Contradicts with some other part. 

● Example: 

– One customer says turn OFF heater and OPEN  water shower when temperature \> 100 0C 

– Another customer says turn OFF heater andturn  ON cooler when temperature \> 100 0C  

15

Incomplete Requirement 

● Some requirements have been omitted: – Possibly due to oversight. 

● Example: 

– The Analyst has not recorded: when temperature falls   
below 90C: 

● Heater should be turned ON ● Water shower turned OFF.

16

8  
Analysis of the Gathered Requirements (CONT.) 

● Requirements Analysis involves: 

– Obtaining a clear, in-depth understanding of the   
product to be developed, 

– Remove all ambiguities and inconsistencies from  the initial customer perception of the problem. 

● It is quite difficult to obtain: 

– A clear, in-depth understanding of the problem: 

– Especially if there is no working model of the  problem. 

17

Analysis of the Gathered Requirements  (CONT.) 

● Experienced analysts take considerable time: 

– To understand the exact requirements the  customer has in his mind. 

● Experienced systems analysts know often, as a  result of painful experiences \--- 

– Without a clear understanding of the problem, it  is impossible to develop a satisfactory system. 

18

9  
Analysis of the Gathered Requirements(CONT.) 

● Several things about the project should be  clearly understood by the analyst: – What is the problem? 

– Why is it important to solve the problem? – What are the possible solutions to the problem?

– What complexities might arise while solving the  problem? 

19

Analysis of the Gathered Requirements(CONT.) 

● Some anomalies and inconsistencies can be very

subtle: 

– Escape even most experienced eyes. 

● If a formal model of the system is constructed, 

– Many of the subtle anomalies and inconsistencies  get detected.

20

10  
Analysis of the Gathered Requirements(CONT.) 

● After collecting all data regarding the system to be developed, 

– Remove all inconsistencies and anomalies fromthe  requirements, 

– Systematically organize requirements into a Software  Requirements Specification (SRS) document. 

21

Software Requirements Specification

● Main aim of Requirements Specification: – Systematically organize the requirements  arrived during requirements analysis. 

– Document requirements properly. 

● The SRS document is useful in various contexts: – Statement of user needs 

– Contract document 

– Reference document 

– Definition for implementation

22

11  
SRS: A Contract Document 

● Requirements document is a reference document. 

● SRS document is a contract between the development team and the customer. 

– Once SRS document is approved by the customer 

– Controversies are settled by referring to SRS document.

● Once customer agrees to the SRS document: 

– Development team starts to develop the product according to   
the requirements recorded in the SRS document. 

● The final product will be acceptable to the customer: 

– As long as it satisfies all the requirements recorded in the   
SRS document.  

23

SRS Document 

● The SRS document is known as black-box specification: 

– The system is considered as a black box whose internal   
details are not known. 

– Only its visible external (input/output) behavior is  documented. 

Input Data S Output Data

24

12  
– What needs to be done   
SRS Document (CONT.) 

● SRS document concentrates on: Properties of a Good SRS Document   
– Carefully avoids the solution (how to do) aspects. ● The SRS document serves as a contract   
– Between development team and the customer. – Should be carefully written 

● The requirements at this stage: – Written using end-user terminology. ● If necessary:   
– Later a formal requirement specification may be  developed from it. 

25

● It should be concise 

– and at the same time should not be ambiguous. 

● It should specify what the system must do – and not say how to do it. 

● Easy to change., 

– i.e. it should be well-structured. 

● It should be consistent. 

● It should be complete. 

● It should be traceable   
– You should be able to trace which part of the   
specification corresponds to which part of the design,   
code, etc and vice versa. 

● It should be verifiable 

– Eg ‘system should be user friendly’ is not verifiable26

13  
Input Data ~~Output Data~~   
From Here: 14-08-2026

SRS Document (CONT.) 

● SRS document contains three important parts: – Functional requirements, 

– Non-functional requirements, 

– Goals of Implementation. 

Functional requirements 

● It is desirable to consider every system: – Performing a set of functions { fi }.   
– Each function fi considered as: 

– Transforming a set of input data to corresponding  output data. 

fi 

27

Example: Functional Requirement 

● F1: Search Book 

– Input: 

● An author’s name: 

– Output: 

● Details of the author’s books and the locations of  these books in the library. 

Author Name Book Details   
F1

28

14  
Functional Requirements 

● Functional requirements describe: 

– A set of high-level requirements – Each high-level requirement: ● Takes in some data from the user ● Outputs some data to the user – Each high-level requirement: ● Might consist of a set of identifiable functions  
● Processing required to obtain the ~~output data set fro~~m   
29

Functional Requirements 

● For each high-level requirement: – Every function is described in terms of: ● Input data set 

● Output data set 

input data set.

30

15  
Nonfunctional Requirements 

● Characteristics of the system which can not  be expressed as functions: 

– Maintainability, 

– Portability, 

– Usability, etc.  

31

Nonfunctional Requirements 

● Non-functional requirements include: – Reliability issues, 

– Performance issues: 

Example: How fast the system can produce results 

– So that it does not overload another system to which   
it supplies data, etc. 

– Human-computer interface issues, 

– Interface with other external systems, 

– Security, maintainability, etc.

32

16  
Non-Functional Requirements 

● Hardware to be used, 

● Operating System or DBMS to be used ● Capabilities of I/O devices 

● Standards Compliance 

● Data Representations 

– By the interfaced system 

33

Goals of Implementation 

● Goals: Describe things that are desirable of the system: 

– But, would not be checked for compliance. 

● For example: 

– Reusability issues 

– Functionalities to be developed in future

34

17  
Organization of the SRS Document 

● Introduction. 

● Functional Requirements 

● Nonfunctional Requirements – External interface requirements 

– Performance requirements 

● Goals of implementation 

– Outputting ~~the system response to~~ the user.35  
Functional Requirements 

● A high-level function is one: 

– Using which the user can get some useful piece of work   
done. 

● Can the receipt printing work be done during withdrawal of money from an ATM: 

– Be called a useful piece of work? ● A high-level requirement typically involves: – Accepting some data from the user, 

– Transforming it to required response, and then 36

18  
● Even for ~~the same~~ high-level function,   
High-Level Function 

● A high-level function: 

– Usually involves a series of interactions betweenthe system and one or more users. 

– There can be different interaction sequences or  scenarios 

– Due to users selecting different options or entering  different data items. 

– Title, Author Name, Publisher name, Year of Publication, ~~ISBN Number, Catalog Number, Location in the Library.~~  
37

Example Functional Requirements 

● List all functional requirements 

– With proper numbering. 

Req. 1: 

● Once the user selects the “search” option, – He is asked to enter the key words. 

● The system should output details of all books 

– Whose title or author name matches any of the key words entered. ● Details include: 

38

19  
Example Functional Requirements 

Req.2: 

● When the “renew” option is selected, 

– The user is asked to enter his membership  number and password. 

● After password validation, 

– The list of the books borrowed by him are  displayed. 

● The user can renew any of the books: 

– By clicking in the corresponding renew box. ~~Publication, ISBN Number, Catalog Number, Location in the~~    
39

Req. 1: 

R.1.1: 

● Input: “search” option, 

● Output: user prompted to enter the key words. 

R1.2: 

● Input: key words 

● Output: Details of all books whose title or author  name matches any of the key words. Details include: Title, Author Name, Publisher name, Year of  

Library. 

● Processing: Search the book list for the keywords40

20  
Req. 2: 

R2.1:   
● ~~Inp~~ut: “renew” option selected,   
● Output: User prompted to enter his membership number and password.   
R2.2:   
● ~~Inp~~ut: Membership number and password ● Output: 

– List of the books borrowed by user are displayed. 

– User prompted to enter books to be renewed or 

– User informed about bad password ● Processing: Password validation, search books issued to the user from borrower list and display. 

41

Req. 2: 

● R2.3: 

– Input: user choice for renewal of the books  issued to him through mouse clicks in the  corresponding renew box. 

– Output: Confirmation of the books renewed

– Processing: Renew the books selected by the  user in the borrower list.

42

21  
Bad SRS Documents 

Bad SRS Documents- Charecteristics   
● Unstructured Specifications: – Narrative essay– is one of the worst types  of specification document: 

● Difficult to change, 

● Difficult to be precise, 

● Difficult to be unambiguous, 

● Scope for contradictions, etc.   
Ex:“~~Library member names should be stored in a sorted descending o~~rder”  
43

● Noise: 

– Presence of text containing information irrelevant to the problem. 

● Silence: 

– Aspects important to proper solution of the problem are   
omitted. 

● Overspecification: 

– Addressing “how to” aspects 

– Overspecification restricts the solution space for the  designer. 

● Contradictions: 

– Contradictions might arise 

● if the same thing described at several places in    
different ways.

44

22  
Charecteristics of Bad SRS Documents

● Ambiguity: 

– Literary expressions 

– Unquantifiable aspects, e.g. “good user interface” ● Forward References: 

– References to aspects of problem – Defined only later on in the text. 

● Wishful Thinking: 

– Descriptions of aspects 

– For which realistic solutions will be hard to find. 45

Representation of Complex Processing Logic: 

● Decision Trees 

● Decision Tables 

● Decision trees: 

– Edges of a decision tree represent conditions – Leaf nodes represent actions to be performed. 

● A decision tree gives a graphic view of: 

– Logic involved in decision making 

– Corresponding actions taken. 

46

23  
Example: Library Membership Software (LMS) 

● A Library Membership automation Software (LMS) should 

support the following three options: 

– New member, 

– Renewal, 

– Cancel membership. 

● When the New member option is selected, 

● The software asks details about the member:   
● Name,   
● Address,   
● Phone number, etc. 

● If proper information is entered, 

– A membership record for the member is created – A bill is printed for the annual membership charge plus the  security deposit payable.  

47

Example LMS (Contd.) 

● If the Renewal option is chosen, 

– LMS asks the member's name and his membership number

● Checks whether he is a valid member. 

– If the name represents a valid member, 

● The membership expiry date is updated and the annual  membership bill is printed, 

● Otherwise an error message is displayed. 

● If the Cancel Membership option is selected and the name of a valid member is entered, 

– The membership is cancelled, 

– A cheque for the balance amount due to the member is printed 

– The membership record is deleted.

48

24  
\- Get details   
\- Create record   
\- Print bills   
\- Get Details   
\- Update record   
\- Print bills   
input\- Get Details \- Delete record   
\- Print error message   
Decision Tree for LMS

New member 

Renewal 

User 

Cancel 

\- Print Cheque 

Invalid option 

Upto Here 14-08-26Fig. 3.4: Decision tree for LMS  

49

Decision Tree for LMS

![][image1]  
Fig. 3.4: Decision tree for LMS 

Upto Here 14-08-26

50

25  
Decision Table 

● Decision tables specify: 

– Which Variables are to be tested 

– What Actions are to be taken if the conditions are true, – The order in which decision making is performed. 

● A decision table shows in a tabular form: – Processing logic and corresponding actions 

● Upper rows of the table specify: 

– The variables or conditions to be evaluated ● Lower rows specify: 

– The actions to be taken when the corresponding  conditions are satisfied. 

From Here 18-08-26  
51

Decision Table 

DT Technical Terminology: ● A column of the table is called a rule: ● A rule implies: 

– if a condition is true, then execute the  corresponding action.

52

26  
Fig 3.5: Decision table for LMS

Valid selection NO ~~YES YES YES~~  
New member \-- ~~YES NO NO~~  
Renewal \-- ~~NO YES NO~~  
Cancellation \-- ~~NO NO YES~~  
Display error message yes \-- ~~\-- \--~~ Build customer record \-- ~~\-- \--~~  
Fig. 3.5: Decision table for LMS   
Generate bill \-- ~~\--~~  
Ask membership details ~~\--~~   
Upto Here 14-08-26  
Update expiry date ~~\-- \-- \--~~ Print cheque \-- ~~\-- \--~~   
53  
Delete record \-- ~~\-- \--~~  
Example: Decision Table for LMS● Conditions 

● Actions 

Ask member's name etc.  

54

27  
Decision Tree Vs Decision Table

● Both Decision Tables and Decision Trees – Can represent Complex Program Logic. 

● Decision Trees are easier to read and understand – When the number of conditions are small. 

● Decision Tables help to look at every possible

combination of conditions. 

55

Formal Specification 

● A formal specification technique is a mathematical  method to: 

– Accurately specify a system. 

– Verify that implementation satisfies specification. – Prove properties of the specification. 

● Advantages: 

– Well-defined semantics, no scope for Ambiguity

– Automated tools can check Properties of Specifications

– Executable specification 

● Disadvantages of formal specification techniques: – Difficult to Learn and use 

– Not able to handle Complex systems

56

28  
Formal Specification 

● Mathematical techniques used include: – Logic-based   
– Set Theoretic 

– Algebraic Specification 

– Finite State Machines … etc. 

57

Semiformal Specification 

● Structured Specification Languages – SADT (Structured Analysis and Design Technique) 

– PSL/PSA (Problem Statement Language / PS Analyzer) ● PSL is a Semi-formal Specification Language ● PSA can Analyze the Specifications expressedin PSL

58

29  
● If non-functional requirements are ~~important for~~    
Executable Specification Language

● If Specification is expressed in formal language: 

– it becomes possible to execute the specification to  provide a system prototype. 

● However, Executable Specifications are usually slow 

and inefficient. 

● Executable Specifications only test Functional  Requirements: 

some products: 

– The utility of an executable specification prototype is   
limited. 

59

4GLs 

● 4GLs (Fourth Generation Languages) are examples – Executable specification languages. ● 4GLs are successful 

– Because there is a lot of commonality data processing   
applications. across 

● 4GLs rely on Software Reuse 

– Where common abstractions have been identified and  parameterized. 

● Rewriting 4GL Programs in Higher Level Languages: – Result in upto 50% lower memory requirements – Also the programs run upto 10 times faster.

60

30  
Summary 

● Requirements Analysis and Specification 

– An important phase of Software Development: 

– Any error in this phase would affect all subsequent phases of  development. 

● Consists of two different activities: 

– Requirements gathering and analysis 

– Requirements specification 

● The aims of Requirements Analysis: 

– Gather all user requirements 

– Clearly understand exact user requirements – Remove inconsistencies and incompleteness. 

● The goal of Specification: 

– Systematically Organize Requirements. 

– Document the Requirements in a SRS document.  61

Summary 

● Main components of SRS document: – Functional requirements 

– Non-functional requirements 

– Constraints 

● Techniques to express Complex logic: – Decision Tree 

– Decision Table 

● Formal Requirements Specifications have several Advantages. ● Major Shortcoming is, that these are hard to use. 

62

31  
L3- Requirements Analysis and Specification  END 

Thank You 

18-08-2026

63

32

[image1]: <data:image/png;base64,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>