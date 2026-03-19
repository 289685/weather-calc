#include <iostream>   // for input/output (cin, cout)
#include <cmath>      // for math functions like pow()
using namespace std;

// Function prototypes
void   calcWindChill(double tempF, double wsMph, double& windC);
void   calcCloudBase(double tempF, double dewp, double& CBH);
bool   fail(const string& prompt, double& value);
double getInputs(double& tempF, double& wsMph, double& dewp);
double displayResults(double tempF, double wsMph, double dewp,
                      double windC, double CBH);

int main() {
    double tempF, wsMph, dewp, windC, CBH; // variables for temperature, wind speed, dew point, results

    // Intro message
    cout << "This program will calculate wind chill and cloud base" << endl;

    // Get user input values
    double inputStatus = getInputs(tempF, wsMph, dewp);
    if (inputStatus != 0) {         // if input failed in some way
        cout << "Error getting inputs. Exiting program." << endl;
        return 1;
    }

    // Calculate wind chill using formula
    calcWindChill(tempF, wsMph, windC);

    // Calculate cloud base height
    calcCloudBase(tempF, dewp, CBH);

    // Display all results
    displayResults(tempF, wsMph, dewp, windC, CBH);

    return 0; // end program
}

// Function to calculate wind chill based on temperature and wind speed
void calcWindChill(double tempF, double wsMph, double& windC) {
    // Standard wind chill formula
    windC = 35.74
          + 0.6215 * tempF
          - 35.75 * pow(wsMph, 0.16)
          + 0.4275 * tempF * pow(wsMph, 0.16);
}

// Function to calculate cloud base height
void calcCloudBase(double tempF, double dewp, double& CBH) {
    // Cloud base formula (approximation in feet)
    CBH = 1000.0 * (tempF - dewp) / 4.4;
}

// Function to safely get numeric input from the user
// Returns true if a valid number was read, false if input failed (e.g., EOF)
bool fail(const string& prompt, double& value) {
    while (true) {
        cout << prompt;   // ask user for input
        cin >> value;     // attempt to read value

        if (!cin.fail()) {
            // valid number
            return true;
        }

        if (cin.eof()) {
            // user closed input stream
            return false;
        }

        // If input is invalid, show error and reset input stream
        cout << "Invalid input. Please enter a number." << endl;
        cin.clear();               // clear error flag
        cin.ignore(10000, '\n');  // discard bad input
    }
}

// Function to collect all user inputs
// Returns 0 on success, -1 if any input fails
double getInputs(double& tempF, double& wsMph, double& dewp) {
    if (!fail("Please enter temperature in Fahrenheit: ", tempF)) {
        return -1.0;
    }
    if (!fail("Enter the wind speed in mph: ", wsMph)) {
        return -1.0;
    }
    if (!fail("Finally, enter the dew point: ", dewp)) {
        return -1.0;
    }

    return 0.0; // success
}

// Function to display formatted results
// Returns 0 after displaying
double displayResults(double tempF, double wsMph, double dewp,
                      double windC, double CBH) {
    cout << "\n===== Weather Results =====" << endl;
    cout << "Temperature: " << tempF << " F" << endl;
    cout << "Wind speed:  " << wsMph << " mph" << endl;
    cout << "Dew point:   " << dewp << " F" << endl;
    cout << "Wind chill:  " << windC << " F" << endl;
    cout << "Cloud base height: " << CBH << " ft" << endl;

    return 0.0;
}
