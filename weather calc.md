#include <iostream>
#include <cmath>
using namespace std;

// Function prototypes
void calcWindChill(double& tempF, double& wsMph, double& windC);
void calcCloudBase(double& tempF, double& dewp, double& CBH);
void fail(const string& prompt, double& value);

int main() {
    // Variable declarations
    double tempF, wsMph, dewp, windC, CBH;

    cout << "this program will calculate wind chill and cloud base\n";

    // Get temperature input
    fail("please enter temperature in fahrenheit\n", tempF);

    // Get wind speed input
    fail("enter the wind speed in Mph\n", wsMph);

    // Get dew point input
    fail("finally enter the dew point\n", dewp);

    // Call function to compute wind chill
    calcWindChill(tempF, wsMph, windC);

    // Call function to compute cloud base height
    calcCloudBase(tempF, dewp, CBH);

    // Display results
    cout << "the wind chill is " << windC << " F" << endl;
    cout << "the cloud base height " << CBH << endl;

    return 0;
}

// Calculates wind chill using the standard wind chill formula
void calcWindChill(double& tempF, double& wsMph, double& windC) {
    windC = 35.74
          + 0.6215 * tempF
          - 35.75 * pow(wsMph, 0.16)
          + 0.4275 * tempF * pow(wsMph, 0.16);
}

// Calculates cloud base height (CBH) in feet
void calcCloudBase(double& tempF, double& dewp, double& CBH) {
    CBH = 1000.0 * (tempF - dewp) / 4.4;
}

// Reads a double with validation (no bool)
void fail(const string& prompt, double& value) {
    while (true) {
        cout << prompt;
        cin >> value;

        if (!cin.fail()) {
            // valid number read; exit the function
            return;
        }

        cout << "Invalid input. Please enter a number." << endl;
        cin.clear();
        cin.ignore(10000, '\n'); // discard bad input
    }
}
