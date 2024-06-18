---
layout:      project
title:       Tic Tac Toe C++ Project
date:        17 June 2024 
image:
  path:       /assets/img/projects/hyde-v2@0,25x.jpg
  srcset:
    1920w:   /assets/img/projects/hyde-v2.jpg
    960w:    /assets/img/projects/hyde-v2@0,5x.jpg
    480w:    /assets/img/projects/hyde-v2@0,25x.jpg
caption:     Hyde is a brazen two-column Jekyll theme.
description: 
  A simple tic tac toe game written in c++ - this program is designed to take an input of numbers and output which person side wins the game
links:

featured:    false
---

## Tic Tac Toe 

This program has a couple of major aspects  

The first is a function that decides is the entered number configuration is a valid tic tac toe combo.  

Once the validity is checked, the side that wins the game is decided.  

While this is currently a simple game, it wouldn't be hard to modify this to work on a website with a frontend UI that actaully plays tic tac toe

To do this, you would simply design a UI that could support a tic tac toe game. Once the game finishes, output the combo of X's and O's in the format of the number string taken by this program. 

## Code Example 

#include <iostream>
#include <random>
#include <cmath>

using std::cout;
using std::cin;
using std::endl; 

//Discovered unsigned function from:
//https://stackoverflow.com/questions/1489830/efficient-way-to-determine-number-of-digits-in-an-integer
unsigned GetNumberOfDigits (unsigned i)
{
    return i > 0 ? (int) log10 ((double) i) + 1 : 1;
}

std::string ValidateConfig(int config) {
    //code start
    //0 = o, 1 = x, 2= empty
    //some configs have leading 0's
    //how to tell when you have leading 0s?

    std::string returnString;
    char winningLetter;
    int length, numLeadingZeros, numX, numO;

    length = GetNumberOfDigits(config);

    std::string str = std::to_string(config);


    //makes sure config is 9 digits long and accounts for leading 0's
    if (length < 9 ){
        numLeadingZeros = 9-length;
        for (int i = 0; i < numLeadingZeros; i++){
            str.insert(0, "0");
        }
    }
    if (length > 9){
        return "Invalid configuration!";
    }

    //checks if configuration is valid
    for (int i = 0; i<length; i++){
        if(str[i]=='0'){
            numO++;
        }
        else if(str[i]=='1'){
            numX++;
        }
    }
    if ((numX > 5) || (numO > 5)){
        cout << "Invalid configuration!" << endl;
    }

    bool draw = true;

    //Checks for rows that match 
    for (int i = 0; i<=length; (i+=3)){
        if ((str[i]==str[i+1])&&( str[i]==str[i+2])){
            draw = false;
            winningLetter = str[i];
            switch (winningLetter){
                case '0':
                    returnString = "O wins!";
                    break;
                case '1':
                    returnString = "X wins!";
                    break;
                // case '2':
                //     returnString = "It's a draw!";
                //     break;
            }
        }
    }

    //Checks for columns that match
    for (int i = 0; i<=3; i++){
        if ((str[i]==str[i+3])&&(str[i]==str[i+6])){
            winningLetter = str[i];
            draw = false;
            switch (winningLetter){
                case '0':
                    returnString = "O wins!";
                    break;
                case '1':
                    returnString = "X wins!";
                    break;
                // case '2':
                //     returnString = "It's a draw!";
                //     break;
            }
        }
    }

    //checks for diagonals that match
    for (int i = 0; i<3; (i+=2)){
        if ((str[i]==str[i+4])&&( str[i]==str[i+8])){
            winningLetter = str[i];
            draw = false;
            switch (winningLetter){
                case '0':
                    returnString = "O wins!";
                    break;
                case '1':
                    returnString = "X wins!";
                    break;
                // case '2':
                //     returnString = "It's a draw!";
                //     break;
            }
        }
        else if ((str[i]==str[i+2])&&( str[i]==str[i+4])){
            winningLetter = str[i];
            draw = false;
            switch (winningLetter){
                case '0':
                    returnString = "O wins!";
                    break;
                case '1':
                    returnString = "X wins!";
                    break;
                // case '2':
                //     returnString = "It's a draw!";
                //     break;
            }
        }
        
    }

    if (draw == true){
        returnString = "It's a draw!";
    }
    return returnString;
}

int main () {

    int config{0};
    cout << "Enter configuration: ";
    cin >> config;
    cout << "Result: " << ValidateConfig(config) << endl;
    return 0;
}
