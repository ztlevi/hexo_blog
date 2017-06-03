---
title: Swift Basics
categories: coding
tags: [coding, swift]
date: 2017-05-29 22:13:07
---
<!-- markdown-toc start - Don't edit this section. Run M-x markdown-toc-generate-toc again -->
**Table of Contents**

- [Constants and Variables](#constants-and-variables)
- [Type Annotations](#type-annotations)
- [Naming Constants and Variables](#naming-constants-and-variables)
- [Printing](#printing)
- [UInt](#uint)
- [Floating-Point Numbers](#floating-point-numbers)
- [Type Safety and Type Inference](#type-safety-and-type-inference)
- [Numeric Literals](#numeric-literals)
- [Type Aliases](#type-aliases)
- [Tuples](#tuples)
- [Optionals](#optionals)
    - [If Statements and Forced Unwrapping](#if-statements-and-forced-unwrapping)
    - [Optional Binding](#optional-binding)
    - [implicitly unwrapped optional](#implicitly-unwrapped-optional)

<!-- markdown-toc end -->

<!--more-->
Constants and Variables
=======================

If a stored value in your code is not going to change, always declare it as a constant with the let keyword. Use variables only for storing values that need to be able to change.

``` Swift
let maximumNumberOfLoginAttempts = 10
var currentLoginAttempt = 0”
```

Type Annotations
================

It is rare that you need to write type annotations in practice. If you provide an initial value for a constant or variable at the point that it is defined, Swift can almost always infer the type to be used for that constant or variable, as described in Type Safety and Type Inference.

``` swift
var welcomeMessage: String
welcomeMessage = "Hello"
```

In the welcomeMessage example above, no initial value is provided, and so the type of the welcomeMessage variable is specified with a type annotation rather than being inferred from an initial value.

Naming Constants and Variables
==============================

Constant and variable names can contain almost any character, including Unicode characters:

``` swift
let π = 3.14159
let 你好 = "你好世界"
let 🐶🐮 = "dogcow"
```

Printing
========

Swift uses string interpolation to include the name of a constant or variable as a placeholder in a longer string, and to prompt Swift to replace it with the current value of that constant or variable. Wrap the name in parentheses and escape it with a backslash before the opening parenthesis:

``` swift
print("The current value of friendlyWelcome is \(friendlyWelcome)")”
```

UInt
====

Swift also provides an unsigned integer type, UInt, which has the same size as the current platform’s native word size:

-   On a 32-bit platform, UInt is the same size as UInt32.
-   On a 64-bit platform, UInt is the same size as UInt64.

Floating-Point Numbers
======================

Floating-point types can represent a much wider range of values than integer types, and can store numbers that are much larger or smaller than can be stored in an Int. Swift provides two signed floating-point number types:

-   Double represents a 64-bit floating-point number.
-   Float represents a 32-bit floating-point number.

Double has a precision of at least 15 decimal digits, whereas the precision of Float can be as little as 6 decimal digits.

Type Safety and Type Inference
==============================

Because of type inference, Swift requires far fewer type declarations than languages such as C or Objective-C. Constants and variables are still explicitly typed, but much of the work of specifying their type is done for you.

Type inference is particularly useful when you declare a constant or variable with an initial value. This is often done by assigning a literal value (or literal) to the constant or variable at the point that you declare it.

Numeric Literals
================

Integer literals can be written as:

-   A decimal number, with no prefix
-   A binary number, with a 0b prefix
-   An octal number, with a 0o prefix
-   A hexadecimal number, with a 0x prefix

All of these integer literals have a decimal value of 17:

``` swift
let decimalInteger = 17
let binaryInteger = 0b10001       // 17 in binary notation
let octalInteger = 0o21           // 17 in octal notation
let hexadecimalInteger = 0x11     // 17 in hexadecimal notation”
```

Floating-point literals can be decimal (with no prefix), or hexadecimal (with a 0x prefix). They must always have a number (or hexadecimal number) on both sides of the decimal point. Decimal floats can also have an optional exponent, indicated by an uppercase or lowercase e; hexadecimal floats must have an exponent, indicated by an uppercase or lowercase p.

For decimal numbers with an exponent of exp, the base number is multiplied by 10exp:

1.25e2 means 1.25 x 10<sup>2</sup>, or 125.0. 1.25e-2 means 1.25 x 10<sup>-2</sup>, or 0.0125. For hexadecimal numbers with an exponent of exp, the base number is multiplied by 2exp:

0xFp2 means 15 x 2<sup>2</sup>, or 60.0. 0xFp-2 means 15 x 2<sup>-2</sup>, or 3.75. All of these floating-point literals have a decimal value of 12.1875:

``` swift
let decimalDouble = 12.1875
let exponentDouble = 1.21875e1
let hexadecimalDouble = 0xC.3p0
```

Numeric literals can contain extra formatting to make them easier to read. Both integers and floats can be padded with extra zeros and can contain underscores to help with readability. Neither type of formatting affects the underlying value of the literal:

``` swift
let paddedDouble = 000123.456
let oneMillion = 1_000_000
let justOverOneMillion = 1_000_000.000_000_1
```

Type Aliases
============

Type aliases define an alternative name for an existing type. You define type aliases with the typealias keyword.

Type aliases are useful when you want to refer to an existing type by a name that is contextually more appropriate, such as when working with data of a specific size from an external source:

``` swift
typealias AudioSample = UInt16”
```

Tuples
======

Tuples group multiple values into a single compound value. The values within a tuple can be of any type and do not have to be of the same type as each other.

In this example, (404, "Not Found") is a tuple that describes an HTTP status code. An HTTP status code is a special value returned by a web server whenever you request a web page. A status code of 404 Not Found is returned if you request a webpage that doesn’t exist.

``` swift
let http404Error = (404, "Not Found")
// http404Error is of type (Int, String), and equals (404, "Not Found")
```

If you only need some of the tuple’s values, ignore parts of the tuple with an underscore (\_) when you decompose the tuple:

``` swift
let (justTheStatusCode, _) = http404Error
print("The status code is \(justTheStatusCode)")
// Prints "The status code is 404"
```

Alternatively, access the individual element values in a tuple using index numbers starting at zero:

``` swift
print("The status code is \(http404Error.0)")
// Prints "The status code is 404"
print("The status message is \(http404Error.1)")
// Prints "The status message is Not Found"
```

You can name the individual elements in a tuple when the tuple is defined:

``` swift
let http200Status = (statusCode: 200, description: "OK")
```

If you name the elements in a tuple, you can use the element names to access the values of those elements:

``` swift
print("The status code is \(http200Status.statusCode)")
// Prints "The status code is 200"
print("The status message is \(http200Status.description)")
// Prints "The status message is OK
```

`Note: 
Tuples are useful for temporary groups of related values. They are not suited to the creation of complex data structures. If your data structure is likely to persist beyond a temporary scope, model it as a class or structure, rather than as a tuple. For more information, see Classes and Structures.`

Optionals
=========

You use optionals in situations where a value may be absent. An optional represents two possibilities: **Either there is a value, and you can unwrap the optional to access that value, or there isn’t a value at all.**

The example below uses the initializer to try to convert a String into an Int:

``` swift
let possibleNumber = "123"
let convertedNumber = Int(possibleNumber)
// convertedNumber is inferred to be of type "Int?", or "optional Int"
```

Because the initializer might fail, it returns an optional Int, rather than an Int. An optional Int is written as Int?, not Int. The question mark indicates that the value it contains is optional, meaning that it might contain some Int value, or it might contain no value at all. (It can’t contain anything else, such as a Bool value or a String value. It’s either an Int, or it’s nothing at all.)

If Statements and Forced Unwrapping
-----------------------------------

Once you’re sure that the optional does contain a value, you can access its underlying value by adding an exclamation mark (!) to the end of the optional’s name. The exclamation mark effectively says, “I know that this optional definitely has a value; please use it.” This is known as forced unwrapping of the optional’s value:

``` swift
if convertedNumber != nil {
    print("convertedNumber has an integer value of \(convertedNumber!).")
}
// Prints "convertedNumber has an integer value of 123."
```

`NOTE: 
Trying to use ! to access a nonexistent optional value triggers a runtime error. Always make sure that an optional contains a non-nil value before using ! to force-unwrap its value.`

Optional Binding
----------------

You use optional binding to find out whether an optional contains a value, and if so, to make that value available as a temporary constant or variable. Optional binding can be used with if and while statements to check for a value inside an optional, and to extract that value into a constant or variable, as part of a single action.

Write an optional binding for an if statement as follows:

``` swift
 if let constantName = someOptional {
    statements
}
```

implicitly unwrapped optional
-----------------------------

``` swift
let possibleString: String? = "An optional string."
let forcedString: String = possibleString! // requires an exclamation mark

let assumedString: String! = "An implicitly unwrapped optional string."
let implicitString: String = assumedString // no need for an exclamation mark
```

You can think of an implicitly unwrapped optional as giving permission for the optional to be unwrapped automatically whenever it is used. **Rather than placing an exclamation mark after the optional’s name each time you use it, you place an exclamation mark after the optional’s type when you declare it.**

`NOTE: 
If an implicitly unwrapped optional is nil and you try to access its wrapped value, you’ll trigger a runtime error. The result is exactly the same as if you place an exclamation mark after a normal optional that does not contain a value.`
