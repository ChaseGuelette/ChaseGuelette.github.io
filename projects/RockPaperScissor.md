---
layout:      project
title:       Rock Paper Scissors C++ Projects
date:        2 Jan 2014
image:
  path:       /assets/img/projects/hyde-v2@0,25x.jpg
  srcset:
    1920w:   /assets/img/projects/hyde-v2.jpg
    960w:    /assets/img/projects/hyde-v2@0,5x.jpg
    480w:    /assets/img/projects/hyde-v2@0,25x.jpg
caption:     Hyde is a brazen two-column Jekyll theme.
description: >
  A simple rock paper scissors game built in c++, runs between player and computer
links:

featured:    false
---


## Rock Paper Scissors 

This game is basically just a player vs. computer game.  

The computer has the option of choosing one of the three options, and its choice is facilitated through a random number generator. 

## Code Example

#include <iostream>
#include <random>

std::random_device rd;
std::mt19937 gen(rd());

using std::cout;
using std::cin;
using std::endl;

int RandNumGen() {

    std::uniform_int_distribution<> rng(1, 3);
    return rng(gen);
}

int main () {

    //variable setup 
    int choice, computerChoice;

    computerChoice = RandNumGen();

    cout << "Enter 1 (Rock), 2 (Paper), or 3 (Scissors): ";
    cin >> choice;

    //player choice output
    if (choice == 1){
        cout << "You picked: Rock" << endl;
    } else if (choice == 2){
        cout << "You picked: Paper" << endl;
    } else {
        cout << "You picked: Scissors" << endl;
    }

    //computer choice output 
    if (computerChoice == 1){
        cout << "The computer picked: Rock" << endl;
    } else if (computerChoice == 2){
        cout << "The computer picked: Paper" << endl;
    } else {
        cout << "The computer picked: Scissors" << endl;
    }

    //game decision calculation
    if (choice == 1){
        if (computerChoice == 1){
            cout << "It's a draw!" << endl;
        }
        else if (computerChoice == 2){
            cout << "You lose!" << endl;
        }
        else {
            cout << "You win!" << endl;
        }
    }
    else if (choice == 2){
        if (computerChoice == 1){
            cout << "You win!" << endl;
        }
        else if (computerChoice == 2){
            cout << "It's a draw!" << endl;
        }
        else {
            cout << "You lose!" << endl;
        }
    }
    else {
        if (computerChoice == 1){
            cout << "You lose!" << endl;
        }
        else if (computerChoice == 2){
            cout << "You win!" << endl;
        }
        else {
            cout << "It's a draw!" << endl;
        }
    }

    return 0;
}
