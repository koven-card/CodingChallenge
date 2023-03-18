# CodingChallenge

//I couldn't get my code to work for the decimal to roman numeral. With more time, I'd find my looping errors and fix them.
//I spent 4 and a half hours on this code. I had most of it done in 4 hours, but I wanted to find the bugs.

#include <iostream>
#include <string>
#include <map>
#include <cmath>

using namespace std;

//I'll use a map to pair the values
int romanToDec(string input){
    map<char, int> romanNumbers = {
        {'I', 1},
        {'V', 5},
        {'X', 10},
        {'L', 50},
        {'C', 100},
        {'D', 500},
        {'M', 1000}
};
    //going forward needs more variables than running through the numerals backwards
    int output = 0;
    int previousNumber = 0;
    for(int i = input.length(); i >= 0; i--){
        int currentNumber = romanNumbers[input[i]];
        if(currentNumber < previousNumber){
            output -= currentNumber;
        }else{
            output += currentNumber;
        }
        previousNumber = currentNumber;
    }
    return output;
}

string decToRoman(int input) {
    map<int, char> romanNumbers = {
            {1, 'I'},
            {2, 'V'},
            {3, 'X'},
            {4, 'L'},
            {5, 'C'},
            {6, 'D'},
            {7, 'M'}
    };
    string output = "";
    int counter = 1;
    int tempVar;
    int divider = 10;
    for(int i = input; i >= 0; i = input/(pow(10,counter))) {
        tempVar = input % divider*(pow(10,counter));
        if(tempVar > 4){
            while(tempVar != 0){
                output += romanNumbers[counter];
                tempVar--;
            }
        }else if(tempVar == 4){
                output += romanNumbers[counter];
                output += romanNumbers[counter+1];
        }else if(tempVar == 5){
                output += romanNumbers[counter+1];
        }else if(tempVar > 5 && tempVar < 9){
                output += romanNumbers[counter+1];
                tempVar -= 5;
                while(tempVar != 0){
                output += romanNumbers[counter];
                tempVar--;
                }
        }else if(tempVar == 9){
            output += romanNumbers[counter+2];
            tempVar -= 5;
            while(tempVar != 0){
                output += romanNumbers[counter];
                tempVar--;
            }
        }
        input -= divider;
        counter++;
    }
    return output;
}


int main() {

    int input;
    string rInput;

    cout << "If you are entering a Roman Numeral, press '1'.\nIf you are entering a Decimal Number, press '2'." << endl;
    cin >> input;
    //if it's a roman numeral, use a function that moves them to a decimal number
    //if it's a decimal number, use a function that moves them to a roman numeral
    if(input != 1 && input != 2){cout << "Invalid entry"; return -1;}
    if(input == 1){
        cout << "Enter the Roman Numeral." << endl;
        cin >> rInput;
        cout << rInput << " as a Roman Numeral is " << romanToDec(rInput);
    }
    else if(input == 2){
        cout << "Enter the Decimal Number." << endl;
        cin >> input;
        cout << input << " as a Decimal Number is " << decToRoman(input);
    }

    cout << endl << 1/10 << endl << 145%100;
    return 0;
}

//First I'll trade all the roman numerals into actual numbers.
//I'll enter the roman numerals into a map that will look through and find all the subtractions to do.
//Once the subtractions are done, I'll have it add all the remaining values together.
