#include <iostream>   // For input and output (cin, cout)
#include <cmath>      // For math functions like pow
using namespace std;

// Function prototypes
// Calculates wind chill from temperature (F) and wind speed (mph)
void calcWindChill(double& tempF, double& wsMph, double& windC);

// Calculates cloud base height from temperature (F) and dew point (F)
void calcCloudBase(double& tempF, double& dewp, double& CBH);

// Prompts for a double value and validates the input
bool fail(const string& prompt, double& value);

// Gets all user inputs (temperature, wind speed, dew point)
// Returns temperature; wind speed and dew point are returned by reference
double getInputs(double& wsMph, double& dewp);

// Displays all the results
double displayResults(double tempF, double wsMph, double dewp,
                      double windC, double CBH);

int main() {
    // Variables for temperature, wind speed, dew point, wind chill, and cloud base height
    double tempF, wsMph, dewp, windC, CBH;

    // Intro message to the user
    cout << "This program will calculate wind chill and cloud base" << endl;

    // Get the user inputs (temperature, wind speed, dew point)
    tempF = getInputs(wsMph, dewp);

    // Calculate the wind chill using the given formula
    calcWindChill(tempF, wsMph, windC);

    // Calculate the cloud base height from temperature and dew point
    calcCloudBase(tempF, dewp, CBH);

    // Show all the results to the user
    displayResults(tempF, wsMph, dewp, windC, CBH);

    return 0;  // Program finished successfully
}

void calcWindChill(double& tempF, double& wsMph, double& windC) {
    // Standard wind chill formula (in Fahrenheit and mph)
    windC = 35.74
            + 0.6215 * tempF
            - 35.75 * pow(wsMph, 0.16)
            + 0.4275 * tempF * pow(wsMph, 0.16);
}

void calcCloudBase(double& tempF, double& dewp, double& CBH) {
    // Approximate cloud base height formula (in feet):
    // CBH = 1000 * (temperature - dew point) / 4.4
    CBH = 1000.0 * (tempF - dewp) / 4.4;
}

bool fail(const string& prompt, double& value) {
    // Ask the user for input with the given prompt
    cout << prompt;
    cin >> value;

    // If reading succeeded (no fail state), the input is valid
    if (!cin.fail()) {
        return true;
    }

    // Otherwise, input was invalid (e.g., not a number)
    cout << "Invalid input. Please enter a number." << endl;
    cin.clear();                // Clear the error flags on cin
    cin.ignore(10000, '\n');    // Discard the rest of the current line
    return false;
}

double getInputs(double& wsMph, double& dewp) {
    double tempF;

    // Keep asking until we get a valid temperature in Fahrenheit
    while (!fail("Please enter temperature in Fahrenheit: ", tempF)) {}

    // Keep asking until we get a valid wind speed in mph
    while (!fail("Enter the wind speed in mph: ", wsMph)) {}

    // Keep asking until we get a valid dew point in Fahrenheit
    while (!fail("Finally, enter the dew point: ", dewp)) {}

    // Return the valid temperature value
    return tempF;
}

double displayResults(double tempF, double wsMph, double dewp,
                      double windC, double CBH) {
    // Nicely formatted output of all input values and calculated results
    cout << "\n===== Weather Results =====" << endl;
    cout << "Temperature: " << tempF << " F" << endl;
    cout << "Wind speed: " << wsMph << " mph" << endl;
    cout << "Dew point: " << dewp << " F" << endl;
    cout << "Wind chill: " << windC << " F" << endl;
    cout << "Cloud base height: " << CBH << " ft" << endl;

    return 0.0;  // Dummy return value (not really used)
}
