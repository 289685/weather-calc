#include <iostream>
#include <cmath>
#include <limits>
using namespace std;

// Function prototypes
// Calculates wind chill given temperature (F) and wind speed (mph)
void calcWindChill(double& tempF, double& wsMph, double& windC);

// Calculates cloud base height given temperature (F) and dew point (F)
void calcCloudBase(double& tempF, double& dewp, double& CBH);

int main() {
    // Variable declarations
    double tempF, wsMph, dewp, windC, CBH;

    cout << "this program will calculate wind chill and cloud base\n";

    // Get temperature input, with validation loop
    while (true) {
        cout << "please enter temperature in fahrenheit\n";
        cin >> tempF;

        // If extraction succeeded, break out of loop
        if (!cin.fail()) {
            break;
        }

        // If input failed, show error and clear input state
        cout << "Invalid input for temperature. Please enter a number." << endl;
        cin.clear(); // clear error flags
        cin.ignore(numeric_limits<streamsize>::max(), '\n'); // discard invalid input
    }

    // Get wind speed input, with validation loop
    while (true) {
        cout << "enter the wind speed in Mph\n";
        cin >> wsMph;

        if (!cin.fail()) {
            break;
        }

        cout << "Invalid input for wind speed. Please enter a number." << endl;
        cin.clear();
        cin.ignore(numeric_limits<streamsize>::max(), '\n');
    }

    // Get dew point input, with validation loop
    while (true) {
        cout << "finally enter the dew point\n";
        cin >> dewp;

        if (!cin.fail()) {
            break;
        }

        cout << "Invalid input for dew point. Please enter a number." << endl;
        cin.clear();
        cin.ignore(numeric_limits<streamsize>::max(), '\n');
    }

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
// tempF: air temperature in Fahrenheit
// wsMph: wind speed in miles per hour
// windC: resulting wind chill temperature in Fahrenheit
void calcWindChill(double& tempF, double& wsMph, double& windC) {
    windC = 35.74
            + 0.6215 * tempF
            - 35.75 * pow(wsMph, 0.16)
            + 0.4275 * tempF * pow(wsMph, 0.16);
}

// Calculates cloud base height (CBH) in feet
// using the approximation: CBH = 1000 * (T - Td) / 4.4
// tempF: air temperature in Fahrenheit
// dewp: dew point in Fahrenheit
// CBH: cloud base height in feet
void calcCloudBase(double& tempF, double& dewp, double& CBH) {
    CBH = 1000.0 * (tempF - dewp) / 4.4;
}
}
