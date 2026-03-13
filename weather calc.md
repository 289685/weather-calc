#include <iostream>
#include <cmath>
using namespace std;

void calcWindChill(double& tempF, double& wsMph, double& windC);
void calcCloudBase(double& tempF, double& dewp, double& CBH);
void fail(const string& prompt, double& value);
void getInputs(double& tempF, double& wsMph, double& dewp);
void displayResults(double tempF, double wsMph, double dewp,
                    double windC, double CBH);

int main() {
	double tempF, wsMph, dewp, windC, CBH;

	cout << "This program will calculate wind chill and cloud base" << endl;

	getInputs(tempF, wsMph, dewp);

	calcWindChill(tempF, wsMph, windC);

	calcCloudBase(tempF, dewp, CBH);

	displayResults(tempF, wsMph, dewp, windC, CBH);

	return 0;
}

void calcWindChill(double& tempF, double& wsMph, double& windC) {
	windC = 35.74
	        + 0.6215 * tempF
	        - 35.75 * pow(wsMph, 0.16)
	        + 0.4275 * tempF * pow(wsMph, 0.16);
}

void calcCloudBase(double& tempF, double& dewp, double& CBH) {
	CBH = 1000.0 * (tempF - dewp) / 4.4;
}

void fail(const string& prompt, double& value) {
	while (true) {
		cout << prompt;
		cin >> value;

		if (!cin.fail()) {
			return;
		}

		cout << "Invalid input. Please enter a number." << endl;
		cin.clear();
		cin.ignore(10000, '\n');
	}
}

void getInputs(double& tempF, double& wsMph, double& dewp) {
	fail("Please enter temperature in Fahrenheit: ", tempF);
	fail("Enter the wind speed in mph: ", wsMph);
	fail("Finally, enter the dew point: ", dewp);
}

void displayResults(double tempF, double wsMph, double dewp,
                    double windC, double CBH) {
	cout << "\n===== Weather Results =====" << endl;
	cout << "Temperature: " << tempF << " F" << endl;
	cout << "Wind speed:  " << wsMph << " mph" << endl;
	cout << "Dew point:   " << dewp << " F" << endl;
	cout << "Wind chill:  " << windC << " F" << endl;
	cout << "Cloud base height: " << CBH << " ft" << endl;
}
