# JavaScript

script goes at the bottom of the body tag because it takes the longest to load, type script

make header main and footer first

console log in app.js to see if it's connected

SECTION Data Types

Primitive (value type) / Non-Primitive (reference type)
number, string, boolean / object, array, function

// primitive
let number = 5
let string = 'hello'
let bool = true

// non-primitive
let object = {thing: "it's a thing"}
let array = [1,2,3,4,5]
function example(){
console.log("I'm a function")
}
using example() is invoking the function example

SECTION operators
// number math and operators
number++
number--
number + 5 NOTE number + 5, just did some math but remembers nothing
number += 5 // NOTE number = number + 5
number -= 5
number \*= 2
number /= 2
number %= 2
let sum = 2 + number

// comparative operators
number == 5 // returns true or false if it's true or false
number === 5 // checks for equality and data type
console.log(sum)

// string operators
let string2 = 'world'
string += 'world' // string = string + 'world'
string = `Hello ${string2}` // interpolation
if you have to turn a string into a number use parseInt()

// bool operators
bool == true // are these equal?
bool != true // are these not equal?

// extra conditional fun
console.log(5 == '5') // true
console.log(5 == '5' && 5 == '4') // && AND FALSE only returns true if both are true
console.log('hello' == 'hello' || 5 > 4) // || OR retuens true if one side is true
console.log(5 === '5' && 'h' == 'h' || 5 > 4) // TRUE

// flipping a bool
console.log('pre flip', bool)
if (bool){
bool = false
} else {
bool = true
}

// shorter way (ternary)
bool = bool ? false : true

// speed run way
bool = !bool
since bool can not be true or false this says equal what you're not which is either true or false. flipping the bool

SECTION //Objects and Accessing Arrays
always use less than when writing for loop accessing arrays because it will always be one less than the lendth because arrays include 0

NOTE
.join() takes an array and converts it into a string
Ex.
const elements = ['Fire', 'Air', 'Water'];

console.log(elements.join());
// expected output: "Fire,Air,Water"

console.log(elements.join(''));
// expected output: "FireAirWater"

console.log(elements.join('-'));
// expected output: "Fire-Air-Water"

NOTE
.find
const array1 = [5, 12, 8, 130, 44];

const found = array1.find(element => element > 10);

console.log(found);
// expected output: 12

NOTE
.push
const animals = ['pigs', 'goats', 'sheep'];

const count = animals.push('cows');
console.log(count);
// expected output: 4
console.log(animals);
// expected output: Array ["pigs", "goats", "sheep", "cows"]

animals.push('chickens', 'cats', 'dogs');
console.log(animals);
// expected output: Array ["pigs", "goats", "sheep", "cows", "chickens", "cats", "dogs"]

SECTION // Thursday 2/10/2022
