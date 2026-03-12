#include <iostream>   // library for input/output (cout, cin)
#include <cmath>      // library for math functions like pow()
#include <limits>     // for std::numeric_limits
using namespace std;  // so we can write cout, cin without std:: prefix

// Function to calculate wind chill
// Parameters are passed by reference (&), and the result is written into windC
void calcWindChill(double& tempF, double& wsMph, double& windC) {
    // Wind chill formula (in Fahrenheit)
    windC = 35.74
            + 0.6215 * tempF
            - 35.75 * pow(wsMph, 0.16)
            + 0.4275 * tempF * pow(wsMph, 0.16);
}

// Function to calculate cloud base height
// tempF and dewp (dew point) are inputs, CBH is the output (passed by reference)
void calcCloudBase(double& tempF, double& dewp, double& CBH) {
    // Cloud base height in feet (approx), using common aviation formula
    CBH = 1000.0 * (tempF - dewp) / 4.4;
}

int main() {
    // Variables for temperature (F), wind speed (mph), and dew point (F)
    double tempF, wsMph, dewp;

    // Explain what the program does
    cout << "this program will calculate wind chill and cloud base\n";

    // Get air temperature from the user (with retry)
    while (true) {
        cout << "please enter temperature in fahrenheit\n";
        cin >> tempF;

        if (!cin.fail()) {
            break; // valid number entered
        }

        cout << "Invalid input for temperature. Please enter a number." << endl;
        cin.clear();
        cin.ignore(numeric_limits<streamsize>::max(), '\n');
    }

    // Get wind speed from the user (with retry)
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

    // Get dew point temperature from the user (with retry)
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

    // Variables to store the results from the functions
    double windC, CBH;

    // Call function to compute wind chill (result stored in windC)
    calcWindChill(tempF, wsMph, windC);

    // Call function to compute cloud base height (result stored in CBH)
    calcCloudBase(tempF, dewp, CBH);

    // Output the results to the user
    cout << "the wind chill is " << windC << " F" << endl;
    cout << "the cloud base height " << CBH << endl;

    // Indicate that the program ended successfully
    return 0;
}
