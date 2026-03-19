#include <iostream>   // include standard input/output stream library
#include <cmath>      // include standard math library for functions like pow()
using namespace std;  // use the standard namespace to avoid std:: prefixes

// Function prototypes
void   calcWindChill(double tempF, double wsMph, double& windC); // declare wind chill calculation function
void   calcCloudBase(double tempF, double dewp, double& CBH);    // declare cloud base height calculation function
bool   fail(const string& prompt, double& value);                // declare input validation helper function
double getInputs(double& tempF, double& wsMph, double& dewp);   // declare function to gather all user inputs
double displayResults(double tempF, double wsMph, double dewp,  // declare function to print all results
                      double windC, double CBH);

int main() {                                                     // program entry point
    double tempF, wsMph, dewp, windC, CBH;                       // declare variables for temperature, wind speed, dew point, and outputs

    cout << "This program will calculate wind chill and cloud base" << endl; // print introductory message

    double inputStatus = getInputs(tempF, wsMph, dewp);          // call function to read user inputs
    if (inputStatus != 0) {                                     // check if input operation failed
        cout << "Error getting inputs. Exiting program." << endl; // print error message on failed input
        return 1;                                               // return nonzero status to indicate error
    }

    calcWindChill(tempF, wsMph, windC);                         // compute wind chill using input temperature and wind speed

    calcCloudBase(tempF, dewp, CBH);                            // compute cloud base height using temperature and dew point

    displayResults(tempF, wsMph, dewp, windC, CBH);             // output all the calculated values to the console

    return 0;                                                   // indicate successful program completion
}

void calcWindChill(double tempF, double wsMph, double& windC) { // define wind chill calculation function
    windC = 35.74                                               // start with constant term in wind chill formula
          + 0.6215 * tempF                                      // add term proportional to temperature
          - 35.75 * pow(wsMph, 0.16)                           // subtract term depending on wind speed to a power
          + 0.4275 * tempF * pow(wsMph, 0.16);                 // add mixed term involving temperature and wind speed
}

void calcCloudBase(double tempF, double dewp, double& CBH) {    // define cloud base height calculation function
    CBH = 1000.0 * (tempF - dewp) / 4.4;                        // apply approximate formula to compute height in feet
}

bool fail(const string& prompt, double& value) {                // define helper to safely read a numeric input
    while (true) {                                              // repeatedly attempt to get valid input
        cout << prompt;                                         // print the request message to the user
        cin >> value;                                           // read a numeric value from standard input

        if (!cin.fail()) {                                      // check if extraction succeeded
            return true;                                        // return success if value is valid
        }

        if (cin.eof()) {                                        // check if end-of-file or stream closure occurred
            return false;                                       // return failure if input stream is closed
        }

        cout << "Invalid input. Please enter a number." << endl; // notify user about invalid input
        cin.clear();                                             // clear input stream error state
        cin.ignore(10000, '\n');                                // discard remaining invalid characters in the buffer
    }
}

double getInputs(double& tempF, double& wsMph, double& dewp) { // define function to gather all needed inputs
    if (!fail("Please enter temperature in Fahrenheit: ", tempF)) { // request temperature and check success
        return -1.0;                                            // return error code if temperature input fails
    }
    if (!fail("Enter the wind speed in mph: ", wsMph)) {       // request wind speed and check success
        return -1.0;                                            // return error code if wind speed input fails
    }
    if (!fail("Finally, enter the dew point: ", dewp)) {       // request dew point and check success
        return -1.0;                                            // return error code if dew point input fails
    }

    return 0.0;                                                 // return success code when all inputs are valid
}

double displayResults(double tempF, double wsMph, double dewp, // define function to show input and computed values
                      double windC, double CBH) {
    cout << "\n===== Weather Results =====" << endl;          // print section header for results
    cout << "Temperature: " << tempF << " F" << endl;         // display the input temperature
    cout << "Wind speed:  " << wsMph << " mph" << endl;       // display the input wind speed
    cout << "Dew point:   " << dewp << " F" << endl;          // display the input dew point
    cout << "Wind chill:  " << windC << " F" << endl;         // display the calculated wind chill
    cout << "Cloud base height: " << CBH << " ft" << endl;    // display the calculated cloud base height

    return 0.0;                                                 // return value indicating function completed
}
