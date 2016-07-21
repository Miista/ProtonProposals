# Record syntax for Proton

Introduction
============

A record is a collection of data. The prime example is a person.

A record in Proton is immutable. That is, once it has been declared
there is no way to mutate the data held in an instance of said record.

### Assumptions

I am making the following assumptions:

* Type names starts with a capital letter (e.g. `Person` instead of `person`)
* The type goes on the right side of an expression. (`age: Int` instead of `Int age`)
* Instantiation does not require `new`
 
Some of these assumptions might prove wrong in which case I will update
this list accordingly. Also some might prove to be an inspiration for
future proposals.

### Features

Just for clarity, the features outlined in this proposal is the following:

1. Declaration of a record
2. Generation "magic" for records

Declaration
===========

Declaring a record should ideally be as simple as possible.
I propose to introduce `record` as a keyword.
Like in the following example:

    record Person(name: String, age: Int)

Declaring a record would also generate accessors for any given attribute
declared for the record. 
As in the example both `name` and `age` would be members of the `Person` record
and accessors would be created for both members.

Usage
=====

Accessing a member of a record would be possible using dot-syntax.
That is `record.memberName`.

The declared record would be instantiated and stored in a variable
Here `let` is used for declaration of a value. 

    let person = Person("John Doe", 99)
    let hisAge = person.age


A record can be used in place of any other expression in a `let` expression.

    let p = Person("John Doe", 0) in { ... }



### Mutation

**NOTE:** This might need to go in its own separate proposal.

Since records in this proposal is immutable we can't directly
mutate values.
We need some way to mutate and update values in a record.

I propose to introduce the keyword `with` for mutating one or several
members of a record.

    let person1 = person with { age = 5 } // Will create a new instance of Person with age set to 5
    let person2 = person with { age = 5, name = "Jane" }

Grammar
=======

### Declaring a Record

~~~
record            = "record", typeName, "(", fieldDeclarations, ")"
fieldDeclarations = fieldDeclaration, { fieldDeclaration }
fieldDeclaration  = identifierName, ":", typeName

memberAccess      = typeName, ".", identifierName

mutateExpr        = typeName, "with", "{", mutateMembers, "}"
mutateMembers     = mutateMember, { mutateMember }
mutateMember      = identifierName, "=", expression

// Below is just the general declaration of identifiers
typeName          = capitalLetter, { anyLetter }
identifierName    = lowercaseLetter, { lowercaseLetter }
~~~
