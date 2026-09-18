~~National Institute of Technology Manipur- Imphal~~   
15-09-2026

Software Engineering 

Formal Specification of Systems (L4) 1\. Introduction    
2\. What is Formal Technique   
3\. Formal Lang: Syn, Sem, Rel Domains 4\. Model vs Property Oriented Methods    
Dr. Prahlada Rao B B 5\. Operational Semantics   
ANRF PM Professor   
~~6\. Merits a~~nd Limitations of Formal Methods ~~7\. Axiomat~~ic Specification   
18-08-2026 

~~8\. Algebra~~ic Specifications;   
CSE Department   
~~9\. Executa~~ble Specifications and 4GL ~~10. Summar~~y   
4.3 Formal Systems Specification  

Organization: 

4.3. 

4.4. 

4.5   
4.6

1  
• Serves as Contract bet’n the Customer and Developers.   
Requirements Analysis and Specification

• An important Life Cycle Phase   
15-09-2026

• ~~For many~~ types of projects subtle problems are acceptable   
• Consists of Two distinct activities: 

­ Requirements Gathering and Analysis 

­ Requirements Specification 

O/P of RAS 

• Software Requirements Specification (SRS) Document: 

SRS 

• Even after taking all care   
­ Some subtle problems may remain in the SRS Document ­ Inconsistency, Incompleteness, and Ambiguity 

SRS Document 

­ Though, it might lead later to rework • For One class of projects, called Safety-critical Projects, ­ Even Minor problems are not acceptable 

• Any failure of a Safety-critical Product 

­ Might result in loss of life and property • How can we ensure, that the Specification is Trouble Free?  
­ Formal Specification

2  
15-09-2026

Introduction-Formal Specification Technique 

• Formal Specification Techniques enable us to: ­ Precisely specify a system 

­ Verify that a system is correctly implemented. 

• We say a System is correctly implemented: 

­ When it satisfies its specification. 

• We will first discuss, important concepts in formal methods • Next we will examine the merits and limitations of formal  techniques 

4.3.1

What is a Formal Technique? • A Formal Technique is a Mathematical Method. 

• Formal Techniques is useful: 

­ To specify a Hardware and / or Software system. 

• Formal techniques can also be used to: ­ Verify whether a specification is realizable, 

­ Verify that an implementation satisfies its specification, 

­ Prove properties of a system without necessarily running  the system, etc.  

3  
15-09-2026

System development life-cycle 

• The generally accepted paradigm for  

System development: 

­ Through a hierarchy of abstractions. 

• Different Stages of Life Cycle: 

­ Requirements Specification, 

­ Design, 

­ Coding, 

­ Testing, Etc.  

Formal Methods 

• Formal Techniques can be used: 

­ At every stage of the system development activity. Specification 

Implementation  
Each stage in this hierarchy:   
Design   
• An implementation of its preceding stage. 

• A specification of the succeeding stage.   
Implementation  
Coding Implementation

Testing Implementation

4  
15-09-2026

Formal Methods   
Syntactic Domain- Formal Methods   
19-08-2026

• The mathematical basis of a Formal Method ­ Provided by its Specification Language. 

• A Formal Specification Language consists of: \- Two sets syn and sem and, \- A relation sat between them. 

• The set syn, is called Syntactic domain. 

• The set sem, is called Semantic domain.   
• The relation sat, is called Satisfaction relation. 

• For a given specification syn, and model of the system sem, 

• if sat(syn, sem), as shown in fig. 3.6 ­ Then syn is said to be the specification of sem­ And sem is the specificand of syn  

• The Syntactic Domain of a formal specification language  consists of: 

­ An alphabet of symbols, set of formation rules to construct  well-formed formulas from the alphabet. 

­ The well-formed formulas are used to specify a system.

5  
\- algebras, theories, and programs.  Semantic Domain of Formal Methods   
15-09-2026

• The Semantic Domain of a formal specification language  consists of: 

 Abstract data type Specification Languages are used to specify  

 Programming Languages are used to specify 

\- functions from input to output values. 

 Concurrent and Distributed System Specification Languages used to  specify 

\- State Sequences, Event Sequences, State-transition Sequences, 

\- Synchronization Trees, Partial Orders, State Machines, etc.  

Satisfaction Relation 

• Given the model of a system, it is important to determine, whether  an element of the semantic domain satisfies the specifications. ­ This satisfaction is determined by using a homomorphismknown as  Semantic Abstraction Function. 

­ The Semantic Abstraction Function maps the elements of the semantic  domain into equivalent classes. 

• There can be different specifications describing different aspects of a  system model, possibly using different specification languages. • Some of these specifications describe the system’s behavior and the  others describe the system’s structure. 

• Two broad classes of Semantic Abstraction Functions are defined: ­ Those that Preserve a System’s Behavior and 

­ Those that Preserve a System’s Structure.

6  
15-09-2026

Model versus Property-Oriented Methods 

• Formal methods are usually classified into two  broad categories: 

­ Model-oriented Approach ­ Property-oriented Approach  

Model-Oriented Style 

In a Model-Oriented Style one defines System behaviour  directly by constructing a model of the system, 

• In terms of mathematical structures s.a: ­ Tuples, Relations, Functions, Sets, Sequences, etc. 

­ Also, State Machines, Petri Nets, etc.

7  
15-09-2026

Property-oriented style 

• In a Property-oriented Style one defines system behaviour  indirectly by stating its properties, usually in the form of 

­ A Set of axioms that the system must satisfy. 

Examples: logic-based, algebraic specification, etc.  

21-08-2026  
Ex: Simple Producer/ Consumer System

• In Property-Oriented Style we list the properties of the  system like: 

­ The consumer can start consuming only after the    
producer has produced an item, 

­ The producer starts to produce an item only after  the consumer has consumed the last item. 

• Producing \==\> No items exist for Consumption • Consuming \==\> Item exists for Consumption 

8  
• We define the basic operations, p (produce), c(consume). Then    
15-09-2026

Example: Producer/ Consumer System

In a Model-oriented approach: 

we can state that 

­ S1+p \==\>S, 

­ S+ c \==\> S1 

­ Make it easier to alter/augment specifications   
• Model-oriented approach we specify a program by writing another  simpler program. 

• Popular known model-oriented specification techniques are: ­ Z ( Z notation) used to specify DS System States, State Sequences, op that  States, pre and post conditions ..etc, 

­ CSP (Communicating Seq Processes) Events, Communication,  Synchronization, Parallel Execution 

­ CCS (Calculus of Communicating System) 

Comparison 

Property-oriented approaches: 

• Property-oriented approaches are suitable for requirements  specification because they can be easily changed. 

• They specify a system as a conjunction of axioms 

­ replace one axiom with another one.  

Model-oriented approaches: 

• Model-oriented approaches are more suited to use in later phases  of life cycle, because even 

­ Minor changes to a specification may lead to drastic changes to  the entire specification. 

• They do not support logical conjunctions (AND) and disjunctions (OR). 

9  
15-09-2026

4.3.3 Operational Semantics 

• Operational semantics of a formal method, is the way  the computations are represents. 

­ i.e. The exact sequence in which the different computations  are carried out 

• There are different types of operational semantics: ­ According to what is meant by a single run of the system, and 

­ How the runs are grouped together to describe the behavior  of the system.  

Operational Semantics (contd) 

• Some commonly used operational semantics are : 

4.3.3-1 Linear Semantics 

• A run of a system is described by a sequence (possibly infinite) of events or states. 

• The concurrent activities are represented by non-deterministic interleavings of the  atomic actions. 

• The behavior of a system in this model consists of the set of all its runs. 

• To make this model realistic, usually justice and fairness restrictions are imposed  on computations to exclude the unwanted interleavings. 

Example: Linear Semantics 

• A concurrent activity a ǁ b is represented by 

­ The set of sequential activities a;b and b;a. 

• This is simple, but rather 

­ Unnatural representation of concurrency.  

10  
• Nodes of the graph ~~represent the possible states~~ in the evolution of a    
15-09-2026

4.3.3-2 Branching Semantics 

• In this approach, behavior of a system is represented by a directed  graph as shown in fig. 3.7. 

system. 

• Although this semantic model distinguishes the branching points in a  
computation, still it represents concurrency by interleaving.  A 

B   
C 

D E 

Fig. 3.7: Branching semantics 

Branching semantics 

• An example involving the transactions in an ATM is shown in fig. 3.7. 

• The descendants of each node of the graph represent the states, which 

• Can be generated by any of the atomic actions enabled at that state. 

A![][image1] 

B   
C 

D E 

Fig. 3.7: Branching semantics 

11  
15-09-2026

4.3.3-3 Maximally Parallel Semantics 

• In this approach, all the concurrent actions enabled  at any state are assumed to be taken together. 

• This is not a natural model of concurrency. since it implicitly assumes 

• The availability of all required computational  resources. 

4.3.3-4 Partial order semantics 

• The semantics ascribed to a system is a structure of states:  satisfying a partial order relation among the states (events). 

• The partial order represents a precedence ordering among events: 

­ and constraints some events to occur only after some other events have  occurred; 

­ While occurrence of other events (concurrent events) is considered to be  incomparable. 

• This fact identifies concurrency, as a phenomenon not translatable to any  interleaved representation. 

12  
15-09-2026

Partial Order Semantics- Simplified Beverage Selling Machine 

• Ex. Figure Shows semantics implied by A Simplified Beverage Selling  Machine. 

• From the figure, we can infer  

that beverage is dispensed  

only if an inserted coin is  

accepted by the machine  

(precedence). 

• Node Ingredient can be  

compared with node Brew, but  

neither can it be compared  

with node Hot/Cold nor with 

node Accepted. 

• Similarly, preparation of  

ingredients and milk are done  

simultaneously (concurrence).  

4.3.4 Merits of Formal Methods • Facilitates precise formulation of specifications • Formal specifications encourage The process of   
• developing rigorous specification is often more important than specification. 

• Construction of a rigorous specification clarifies several aspects of 

­ System behaviour which are not obvious in an informal specification. 

• It is cost-effective to spend more effort at the specification stage. 

­ Otherwise many flaws that go unnoticed will appear at later stages of  software development. 

• For large and complex systems like real-time systems: 

­ 80% of project costs and most of cost overruns result from iterative changes  required due to improper requirements specification. 

• Additional effort required to construct a rigorous formal specification: ­ often well worth the trouble. 

13  
15-09-2026

Merits of Formal Methods 

• Formal methods usually have a well-founded mathematical basis. 

­ formal specifications are precise 

­ can be used to mathematically reason about the properties of a specification 

• Informal specifications are useful in understanding a system and its documentation: ­ but they cannot serve as a basis of verification. 

­ Even carefully written informal specifications are prone to ambiguity and error. • Formal methods have well-defined semantics. 

­ Ambiguity in specifications is automatically avoided when one formally  specifies a system. 

• Formal methods have mathematical basis: 

­ scope for automating analysis of specifications. 

­ Automatic verification: one of the most important advantages of formal methods. • Formal specifications can be executed: 

­ provide immediate feedback on features of the specified system. 

­ The concept of executable specification is related to rapid prototyping.  

Limitations of Formal Methods 

• Formal methods are difficult to learn and use.   
• While using formal specifications Engineers tend to lose the overall  perspective and get lost in the details. 

• The basic incompleteness results of first-order logic (Gödel) suggest: 

­ It is impossible to check absolute correctness of systems Using Theorem  Proving Techniques.

• Formal techniques are not able to handle complex problems. 

­ Even moderately complicated problems blow up the complexity of formal  specification and their analysis. 

­ Also, a large unstructured set of mathematical formulas is difficult to  understand. 

14  
15-09-2026

Formal vs. Informal Specification Methods 

• Formal Specifications: 

­ do not replace Informal Descriptions but complement  them. 

• Comprehensibility of formal specifications is greatly enhanced: ­ when accompanied by an informal description. 

• General recommendation: 

­ Mixed approach 

­ use formal techniques as a broad guideline for use of informal  techniques.  

Upto here: 21-08-2026

Mixed Approach   
25-08-2026

• Formal method is used to identify  verification steps: 

­ But it is legitimate to apply informal  reasoning in correctness arguments. 

­ Any doubt or query relating to an informal  argument is resolved by formal proofs. 

15  
15-09-2026

Model versus Property-Oriented Methods REFRESH

• Formal methods are usually classified into two broad categories: ­ Model-oriented Approach 

­ Property-oriented Approach  

Property-Oriented style 

• In a Property-oriented Style one defines system behaviour indirectly by  stating its properties, usually in the form of 

­ A Set of axioms that the system must satisfy. 

• Ex: logic-based, algebraic specification, etc.  

25-08-2026  
Property-Oriented Specifications 

• Property-Oriented Specifications are divided into  Two Categories: 

­ Axiomatic Specifications ­ Algebraic Specifications 

16  
~~\- write~~ pre-conditions and post-conditions to specify operations   
15-09-2026

Axiomatic Specifications 

In axiomatic specification of a system, first-order logic is used to write pre and post conditions to specify the operations of the system in the form of axioms.  

• Use first order logic: 

• Pre-conditions: Capture the conditions that must be satisfied before an operation  can successfully be invoked 

­ pre-conditions capture the requirements on the input parameters of a function  
• Post-conditions: Conditions that must be satisfied when a function completes  execution for the function, to be considered to have executed successfully. 

­ What are the essentially constraints on the results produced for the function execution  to be considered successful. 

• Domain: 

­ What sort of things it acts upon? 

• Co-domain (range): 

­ What sort of answer does it give? 

How to Develop Axiomatic Specifications?

1\. Establish the range of input values over which the function should behave  correctly: 

­ Establish Input Parameter Constraints As A Predicate. 

2\. Specify a predicate defining the condition: 

­ Which must hold on the output of the function if it behaved properly. 3\. Establish the changes made to the function’s input parameters after  execution of the function. 

­ Pure mathematical functions do not change their input and therefore this  type of assertion is not necessary for pure functions e.g. f(a,b,c) 

­ programming languages allow function inputs to be modified  by passing them as reference. 

4\. Combine all of the above: into pre and post conditions of the function.

17  
15-09-2026

Example1: Axiomatic Specification 

Example1:   
• Specify the pre and post conditions of a function that takes a real  number as argument and returns half the input value if the input is ≤  100, else returns double the value. 

­ f (x : real) : real 

­ pre : x ∈ R 

­ post : {(x≤100) ∧ (f(x) \= x/2)} ∨ {(x\>100) ∧ (f(x) \= 2∗x)} 

Example 2: Axiomatic Specification 

• Consider a function search: 

­ accepts parameters: 

­ an array of integers 

­ an integer key 

­ returns array index of the number in array whose value  equals key: 

­ original input array is unchanged

18  
• pre: exists i in ~~X’First …X’last: x(i)=key~~   
15-09-2026

Axiomatic Specification for Ex2 

Ex2: Axiomatically Specify a Function named search which takes an  Integer Array and an Integer key-value as its arguments and returns the  Index in Array where the key-value is stored 

• Function search(X: Integer Array; key: Integer): Integer 

• post: { X’\[search(X,key)\]=key ∧ (X=X’ ) } • Error: search(X,key)=X’last+1 

 Here the convention followed is:  

If a function changes any of its input parameters and if that  parameter is named X, then it is referred to as X′ after the  function completes execution.  

4.5 Algebraic Specification 

• An object class (or type) is specified in terms of Relationships existing between the operations defined on that type. 

• It was first brought into prominence by Guttag \[1980,1985\]: 

­ Used in specification of abstract data types. 

­ Various notations of Algebraic Specifications have evolved,  including those based on OBJ and Larch languages 

• Essentially Algebraic Specifications: Define a system as: ­ A Heterogeneous Algebra; i.e a collection of different sets   On which several operations are defined. 

• Traditional Algebra are homogeneous. 

• A homogeneous Algebra: 

­ consists of a single set and several operations defined in this set; e.g. { I, \+, \-, \*, / }.

19  
15-09-2026

Traditional Algebra 

• Traditional Algebra are homogeneous. 

• A homogeneous Algebra: 

­ consists of a single set and several operations defined in this set; e.g. { I, \+, \-, \*, / }. 

• In contrast, alphabetic strings A together with operations of: concatenation  and length { A, I, con, len}, is not homogeneous Algebra, 

­ Since the range of the length operation is the set of integers. 

• Each set of symbols in a heterogeneous algebra, is called a sort of the algebra. • To define a heterogeneous algebra, we first need to specify ⁃ Its signature, and 

⁃ The involved operations, their domains and ranges. • The collection of sets that form the heterogeneous algebra: 

­ is called its signature. 

For example consider {S, I, len, concat} 

­ SxI is the signature 

Algebraic Specification 

• An algebraic specification is usually presented in four sections  important parts: 

­ Type Section 

­ Exception Section 

­ Syntactic Section 

­ Semantic section 

1\. Types section: In this, the sorts (or the data types) used is specified.  

2\. Exception section: 

Under normal conditions 

­ The result of an operation may be of some sort. 

­ Under some exceptional conditions, the results may be something else. 3\. Syntax section   
• Names of different data types involved are listed • Names of operators and their domains (signature) listed

20  
­ Specifies what is always true about the ~~behavior of operations.~~   
15-09-2026

Semantic (Equations) Section 

Algebraic specification meaning of a set of interface procedures is  defined by using equations.  

4\. Equations Section:  

This section gives a set of rewrite rules (or equations) defining: ­ meaning of interface procedures in terms of each other. 

•This section is allowed to contain conditional expressions. Ex: a rewrite rule to identify an empty queue may be written as: isempty( create() ) \= true 

• By convention each equation is implicitly universally quantified over  all possible values of the variables. 

• Names not mentioned in syntax section such as ‘r’ or ‘e’ are  variables.  

Algebraic Specification 

Algebraic specific., meaning of a set of interface procedures is defined  by using equations. 

By convention: 

• each equation is implicitly universally quantified over all possible  values of the variables. 

• In simple words, holds good for all values of variables. • Names not mentioned in the syntax section: such 'r' or 'e' are variable. 

• 1st step, defining algebraic specification is identify the set of required  operations. 

• After identify required operators, Classify them as either basic constructor  operators, extra constructor operators, basic inspector operators, or extra  inspection operators. 

• The definition of these categories of operators is as follows:  

21  
2\. Exception section:Lists names of exceptional conditions used in later sections:   
15-09-2026

1\. Types Section lists: 

­ sorts (or types) being specified ­ sorts being imported 

­ Importing a sort: 

­ makes it available in specification. 

­ under exceptional conditions error should be indicated. 

3\. Signature section   
• Defines signatures of interface procedures: 

• e.g. PUSH takes a stack and an element and returns a new stack. ­ push: ­ stack element stack  

4\. Rewrite rules section 

• Lists the properties of the operators: 

­ In the form of a set of axioms or rewrite rules. 

­ allowed to have conditional expressions 

Developing Algebraic Specification

• The first step in defining an algebraic specification: 

­ identify the set of required operations. 

­ e.g. for string identify operations: 

­ create, compare, concatenate, length, etc. 

• Generally Operations fall into 2 classes: 1\. Constructor Operations : 

­ Operations which create or modify entities of the sort  e.g., create, update, add, etc. 

2\. Inspection Operations : 

­ Operations which evaluate attributes of the sort,  

e.g., eval, get, etc. 

• First establish constructor and inspection operations

22  
15-09-2026

Developing Algebraic Specifications

• Next, write down axioms: 

­ Compose each inspection operator  over each constructor operator.  

Developing Algebraic Specifications

• If there are m constructors and n inspection  operators: 

­ We should normally have m\*n axioms. ­ However, an exception to this rule exists. 

• If a constructor operation can be definedusing  other constructors: 

• We need to define inspection operations using  only primitive constructors.

23  
15-09-2026

Example: Stack 

Let us specify an unbounded Stack supporting: 

Types:   
• push 

• defines stack   
• pop   
• uses boolean, element   
Exception:   
• Newstack   
~~Rewrite rules- stack :~~   
• top   
• underflow, novalue 

Syntax: • push:   
­ stack element stack • pop:   
• empty 

Eqations: Stack • pop(newstack) \= underflow  
­ stack stack+{underflow}   
• top:   
• pop(push(s,e)) \= s   
­ stack element+{novalue}   
• empty:   
• top(newstack) \= novalue • top(push(s,e)) \= e   
­ stack boolean   
• newstack:   
• empty(newstack) \= true 

­ stack   
• empty(push(s,e)) \= false 

Rewrite rules 

Rewrite rules let you determine: 

• The meaning of any sequence of calls on the stack functions.  

• Empty(push(pop(push(newstack,e1)),e2)): ­ You can eliminate the call on pop by observing: 

­ It is of the form pop(push(s,e)). 

• After simplification: 

­ empty(push(newstack,e1)) 

­ false

24  
⁃ Can different sequence in application of ~~the rewrite rules always~~  ⁃ If we ~~choose to simplify different terms~~ of the expression in different   
15-09-2026

Two Important Questions 

• Finite Termination Property: 

­ Does application of rewrite rules terminate after a finite  number of steps? 

­ We might endlessly go on applying rewrite rules without  coming to any conclusion?   
• Sometimes development of a specification requires~~, extra function~~s    
• Unique Termination Property: 

give the same answer? 

experiments: 

­ shall we always get the same answer? 

Algebraic Specification 

• For arbitrary algebraic equations: 

­ Convergence is undecidable. 

• If the RHS of each rewrite rule has fewer terms than the left: 

­ Rewrite process must Terminate. 

Auxiliary Functions: 

not part of the system: 

­ To define the meaning of some interface procedures. 

Example: bounded stacks : 

• To specify bounded stacks: need to add a depth function as auxiliary  function: 

­ push returns either a stack or an exception “overflow” when  depth is exceeded.

25  
15-09-2026

Auxiliary Functions 

Bounded Stack: in order to specify a bounded Stack: 

• We need to make changes to different sections of Stack to include  auxiliary functions. 

Syntax: 

• push: 

­ stack element \==\> stack 

• depth: 

­ stack integer 

Auxiliary Functions \-Equations: 

• depth(newstack)=0 

• depth(push(s,e))=depth(s)+1 

• push(s,e)= overflow if depth(s) \>= Max 

Example 2: coord 

• Types: 

­ sort coord 

­ imports integer, boolean 

• Signature: 

­ create(integer,integer) coord ­ X(coord) integer 

­ Y(coord) integer 

­ Eq(coord,coord) boolean 

• Rewrite rules: 

­ X(create(x,y))=x 

­ Y(create(x,y))=y 

­ Eq(create(x1,y1),create(x2,y2))= ((x1=x2) and (y1=y2))

26  
15-09-2026

Structured Specifications 

• Writing formal specifications is time consuming. • To reduce effort, we need to reuse specifications: ­ Instantiation of generic specifications ­ Incremental development of specifications 

Specification Instantiation 

• Take an existing specification: 

­ Specified with some generic parameter ­ Instantiate with some sort 

Incremental Development 

• Develop specifications for simple sorts: 

­ using these specify more complex entities. 

Algebraic Specifications: Pros and Cons 

• Algebraic Specifications have a strong mathematical basis: ­ Can be viewed as Heterogeneous Algebra. 

• An important shortcoming of Algebraic Specifications: 

­ Cannot deal with side effects 

­ Difficult to use with common programming languages. • Algebraic Specifications are hard to understand: 

­ Also changing a single property of the system may require  changing several equations.

27  
15-09-2026

Summary 

• We started by discussing some general concepts in ­ Formal Specification Techniques. 

• Formal specifications have several positive characteristics. 

­ the major shortcoming of formal techniques is that they are hard to use. 

• It is possible that formal techniques will become more usable in future: 

­ with the development of suitable front-ends. 

• We discussed two sample specification techniques, 

­ Axiomatic specification 

­ Algebraic specification 

­ Give us a flavor of the issues involved in formal specification. 

Thank Q 

25-08-2026

28

[image1]: <data:image/png;base64,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>