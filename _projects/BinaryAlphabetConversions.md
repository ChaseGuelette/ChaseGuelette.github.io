---
layout:      projects
title:       Binary Alphabet Conversions C++ Project
date:        17 June 2024 
image:
  path:       /assets/img/projects/hyde-v2@0,25x.jpg
  srcset:
    1920w:   /assets/img/projects/hyde-v2.jpg
    960w:    /assets/img/projects/hyde-v2@0,5x.jpg
    480w:    /assets/img/projects/hyde-v2@0,25x.jpg
caption:     Hyde is a brazen two-column Jekyll theme.
description: 
  A program to convert between binary alphabet setup and integer values
links:

featured:    false
---

## Rock Paper Scissors 

This project is bascially a program that can work conversions between binary alphabet setups.  

The number theory this is based on is that a=2^0, b=2^1, c=2^2, running all the way to z.

The program takes an input of strings, and it can be any string or paragraph. It then converts that input to its intger value in the binary theory(This number can become astronomically large)

It has 4 major functions to acheive this result. The abbreviate function organizes the strings and returns them. The Loc to dec function calls abreviate and converts the input string to its integer value.  

DecToLoc will do the opposite, and convert an input integer to a sorted string output. AddLoc will append two letter strings to one another and output their value. 


# Code Example 

#include <iostream>
#include <random>
#include <cmath>
#include <string>
#include <algorithm>

using std::cout;
using std::cin;
using std::endl;
using std::string;

//required functions
std::int64_t LocToDec(string const & loc);
std::string Abbreviate(string const & loc);
std::string DecToLoc(std::int64_t dec);
std::int64_t AddLoc(string const & loc1, string const & loc2);

//added functions
unsigned GetNumberOfDigits (unsigned i);

int main () {
 
    string initalString, locStr1, locStr2;
    int initalInteger;

    cout << "Give me a location string: " << endl;
    cin >> initalString;

    cout << "Give me an integer: " << endl;
    cin >> initalInteger;

    cout << initalString << " to dec: " << LocToDec(initalString) << endl;
    cout << initalString << " abbreviated: " << Abbreviate(initalString) << endl;
    cout << initalInteger << " to loc: " << DecToLoc(initalInteger) << endl;

    cout << "Give me two more location strings: " << endl;
    cin >> locStr1;
    cin >> locStr2;
    cout << "Sum of " << locStr1 << " and " << locStr2 << " is: " << AddLoc(locStr1, locStr2) << endl;

    return 0;
}

//found on stack overflow 
//https://stackoverflow.com/questions/1489830/efficient-way-to-determine-number-of-digits-in-an-integer
unsigned GetNumberOfDigits (unsigned i){
return i > 0 ? (int) log10 ((double) i ) + 1 : 1;
}

//converts location arithmatic string to an integer --------------- DONE
std::int64_t LocToDec(string const & loc){

    int finalVal = 0;

    char currentChar;

    for (unsigned i = 0; i<loc.length(); i++){

        currentChar = loc.at(i);
        finalVal += pow(2,(currentChar - 'a'));
    }
    return finalVal;
}

//location string and reduces it to abbreviated form ----------------------- DONE
std::string Abbreviate(string const & loc){

    string local = loc;
    sort(local.begin(), local.end());

    char currentChar, nextChar, newChar;

    for (unsigned i = 0; i<local.length()-1; i++){

        sort(local.begin(), local.end());

        currentChar = local.at(i);
        nextChar = local.at(i+1);

        if (currentChar==nextChar){
            newChar = currentChar + 1;
            local.erase(i,2);
            local.insert(i, 1,newChar);
            i = -1;
        }

    }

    return local;
}

//integer to abbrevciated location stringb ------------------------------ DONE
std::string DecToLoc(std::int64_t dec){

    //need to use the method of converting letters to powers 
    //need to have a for loop that find the biggest number that can fit into the input, and add its letter compoenet to the final string

    int moddedDec = dec;
    int numLength = GetNumberOfDigits(dec);
    char valueChar = 0;
    string finalLocationString;

    while (moddedDec > 0){

        bool numFits = false;
        int increment = 0;
        while (numFits == false){
            if (moddedDec - pow(2,increment) < 0){
                numFits = true;
                increment--;
                break;
            }
            increment++;
        }
        valueChar = 'a' + increment;
        finalLocationString += valueChar;
        moddedDec = moddedDec - pow(2,increment);
    }
    sort(finalLocationString.begin(), finalLocationString.end());
    return finalLocationString;

}

//takes 2 location strings and provides integer result -------------------- DONE
std::int64_t AddLoc(string const & loc1, string const & loc2){

    int stringOne = LocToDec(loc1);
    int stringTwo = LocToDec(loc2);

    return (stringOne + stringTwo);
}