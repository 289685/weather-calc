#include <iostream>   // include standard input/output stream library
#include <cmath>      // include standard math library for functions like pow()
using namespace std;  // use the standard namespace to avoid std:: prefixes

// Function prototypes
void   calcWindChill(double& tempF, double& wsMph, double& windC); // all params by reference
void   calcCloudBase(double& tempF, double& dewp, double& CBH);    // all params by reference
bool   fail(const string& prompt, double& value);                  // value already by reference
double getInputs(double& tempF, double& wsMph, double& dewp);      // all inputs by reference
double displayResults(double& tempF, double& wsMph, double& dewp, // all params by reference
                      double& windC, double& CBH);

int main() {                                                       // program entry point
    double tempF, wsMph, dewp, windC, CBH;                         // declare variables

    cout << "This program will calculate wind chill and cloud base" << endl; // intro

    double inputStatus = getInputs(tempF, wsMph, dewp);            // call function to read user inputs
    if (inputStatus != 0) {                                        // check if input operation failed
        cout << "Error getting inputs. Exiting program." << endl; // error message
        return 1;                                                  // nonzero status
    }

    calcWindChill(tempF, wsMph, windC);                            // compute wind chill

    calcCloudBase(tempF, dewp, CBH);                               // compute cloud base

    displayResults(tempF, wsMph, dewp, windC, CBH);                // output all values

    return 0;                                                      // success
}

void calcWindChill(double& tempF, double& wsMph, double& windC) {  // all by reference
    windC = 35.74                                                  // constant term
          + 0.6215 * tempF                                         // temperature term
          - 35.75 * pow(wsMph, 0.16)                               // wind-speed term
          + 0.4275 * tempF * pow(wsMph, 0.16);                     // mixed term
}

void calcCloudBase(double& tempF, double& dewp, double& CBH) {     // all by reference
    CBH = 1000.0 * (tempF - dewp) / 4.4;                           // height in feet
}

bool fail(const string& prompt, double& value) {                   // value by reference
    while (true) {                                                 // repeatedly attempt input
        cout << prompt;                                            // request message
        cin >> value;                                              // read numeric value

        if (!cin.fail()) {                                         // extraction succeeded
            return true;                                           // success
        }

        if (cin.eof()) {                                           // end-of-file / closure
            return false;                                          // failure
        }

        cout << "Invalid input. Please enter a number." << endl;  // invalid input message
        cin.clear();                                               // clear error state
        cin.ignore(10000, '\n');                                   // discard remaining input
    }
}

double getInputs(double& tempF, double& wsMph, double& dewp) {    // all by reference
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

double displayResults(double& tempF, double& wsMph, double& dewp, // all by reference
                      double& windC, double& CBH) {
    cout << "\n===== Weather Results =====" << endl;         // header
    cout << "Temperature: " << tempF << " F" << endl;          // temperature
    cout << "Wind speed:  " << wsMph << " mph" << endl;        // wind speed
    cout << "Dew point:   " << dewp << " F" << endl;           // dew point
    cout << "Wind chill:  " << windC << " F" << endl;          // wind chill
    cout << "Cloud base height: " << CBH << " ft" << endl;     // cloud base height

    return 0.0;                                                    // completed
}
