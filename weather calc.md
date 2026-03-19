#include <iostream>   // include standard input/output stream library
#include <cmath>      // include standard math library for functions like pow()
using namespace std; // too avoid repeating std:: before every statement 

// Function prototypes
void   calcWindChill(double& tempF, double& wsMph, double& windC); // function for windchill calculation
void   calcCloudBase(double& tempF, double& dewp, double& CBH);    // function for windchill claculation
bool   fail(const string& prompt, double& value);                  // function for fail statement 
double getInputs(double& tempF, double& wsMph, double& dewp);      // function to get all inputs 
double displayResults(double& tempF, double& wsMph, double& dewp, // function to display results
                      double& windC, double& CBH);

int main() {                                                       // start of main
    double tempF, wsMph, dewp, windC, CBH;                         // declare variables

    cout << "This program will calculate wind chill and cloud base" << endl; // intro

    double inputStatus = getInputs(tempF, wsMph, dewp);            // call function to read user inputs
    if (inputStatus != 0) {                                        // check if input operation failed
        cout << "Error getting inputs. Exiting program." << endl; // error message
        return 1;                                                  // nonzero status
    }

    calcWindChill(tempF, wsMph, windC);                            // calc wind chill

    calcCloudBase(tempF, dewp, CBH);                               // calc cloud base

    displayResults(tempF, wsMph, dewp, windC, CBH);                // output all values

    return 0;                                                      // end
}

void calcWindChill(double& tempF, double& wsMph, double& windC) {  // calcs windchill
    windC = 35.74                                                   
          + 0.6215 * tempF                                          
          - 35.75 * pow(wsMph, 0.16)                                
          + 0.4275 * tempF * pow(wsMph, 0.16);                     
}

void calcCloudBase(double& tempF, double& dewp, double& CBH) {     // calc cloud base
    CBH = 1000.0 * (tempF - dewp) / 4.4;                           // formula
}

bool fail(const string& prompt, double& value) {                   // fail statement
    while (true) {                                                  
        cout << prompt;                                             
        cin >> value;                                              

        if (!cin.fail()) {                                         
            return true;                                           
        }

        if (cin.eof()) {                                           
            return false;                                          
        }

        cout << "Invalid input. Please enter a number." << endl;  
        cin.clear();                                               
        cin.ignore(10000, '\n');                                   
    }
}

double getInputs(double& tempF, double& wsMph, double& dewp) {    // gets inputs
    if (!fail("Please enter temperature in Fahrenheit: ", tempF)) { // request temperature
        return -1.0;                                               // error
    }
    if (!fail("Enter the wind speed in mph: ", wsMph)) {         // request wind speed
        return -1.0;                                               // error
    }
    if (!fail("Finally, enter the dew point: ", dewp)) {         // request dew point
        return -1.0;                                               // error
    }

    return 0.0;                                                    // success
}

double displayResults(double& tempF, double& wsMph, double& dewp, // display message
                      double& windC, double& CBH) {
    cout << "\n===== Weather Results =====" << endl;           // header
    cout << "Temperature: " << tempF << " F" << endl;          // temperature
    cout << "Wind speed:  " << wsMph << " mph" << endl;        // wind speed
    cout << "Dew point:   " << dewp << " F" << endl;           // dew point
    cout << "Wind chill:  " << windC << " F" << endl;          // wind chill
    cout << "Cloud base height: " << CBH << " ft" << endl;     // cloud base height

    return 0.0;                                                    // finish code
}
