---
title: Illuminati Pyramid Generator C++ Project
description: Generates a Pyramid of a specificed 'height' that has an eye in the middle 
---

## Rock Paper Scissors 

This program is designed to use a series of cout prompts to build a pyramid of asteriks "*" of a certain height, specified by the user.  

The program takes the user input, and builds out a pyramid from left to right whose height is equal to the input.  

When the cout loops reach the center level of the pyramid (calculated based on user input. If no center, puts center one below where the center would be), it prints a "eye" symbol in the middle of the row, which looks like this: "<O>"

# Code Example

#include <iostream>
#include <random>

using std::cout;
using std::cin;
using std::endl;

int numMidSpaces = 1;

void GenImg(int height) {
    //code here
    //can't use string 

    int numMidSpaces = (height*2)-1;
    double middleNum;



    //runs for the provided height 
    for (int i = 1; i<= height; i++){

        //need height minus i leading spaces
        for (int j = 1; j<=(height-i); j++){
            cout << " ";
            numMidSpaces -= 2;
        }

        //finds middle number of height
        if (height%2 == 1){
            double conversion = height*1.0;
            middleNum = (conversion/2)+0.5;
        }
        if (height%2 == 0){
            middleNum = (height / 2)+1;
        }
        
        //when i is same as middle number, prints <O>
        // if (i==middleNum){
            
        // }


        //need i number of stars
        //numMidSpaces starts as the length of each row
        //after the j for loop it has the number of leading and trailing spaces subtracted
        //this leaves the number of spaces in the middle. This is always an uneven number.
        //if the index of the middle space is odd, it prints a *, if its odd it prints a " ".
        int counter = 0;
        
         for (int t = 1; t<=i+ i -1; t++){


//discovered floor function from:
//https://stackoverflow.com/questions/15181579/most-efficient-way-to-compare-a-variable-to-multiple-values

 double rowlenght = i + i -1;            
 double middlecolumn;
 double middlefloor = floor(rowlenght /2.0);
 double middle = rowlenght /2.0;

 if ( middlefloor == middle ) { middlecolumn = rowlenght /2.0; } else { middlecolumn = ( rowlenght /2.0 ) + .5; } ;

 double leftcolumn= middlecolumn-1;
 double rightcolumn= middlecolumn+1;


double tdouble = t;

//             //if t is even, print a space

    if (t == leftcolumn && i == middleNum) { cout <<"<"; }
    else if (t == middlecolumn && i == middleNum) { cout <<"O"; }
    else if (t == rightcolumn && i == middleNum) { cout <<">"; }
    else if ( floor(tdouble /2) == (tdouble/2) ) { cout << " " ; }
else {     cout <<"*";  }
     }

        //need height minus i trailing spaces
        for (int s = 0; s<=(height-i); s++){
            cout << " ";
        }

        cout << endl;
        numMidSpaces = (height*2)-1;
    }
}

int main () {
    int height{0};
    cin >> height;
    GenImg(height);
    return 0;
}