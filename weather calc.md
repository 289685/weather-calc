#include <iostream>
#include <cmath>
using namespace std;

void calcWindChill(double& tempF, double& wsMph, double& windC) {
    windC = 35.74
            + 0.6215 * tempF
            - 35.75 * pow(wsMph, 0.16)
            + 0.4275 * tempF * pow(wsMph, 0.16);
}

void calcCloudBase(double& tempF, double& dewp, double& CBH) {
    CBH = 1000.0 * (tempF - dewp) / 4.4;
}

int main() {
    double tempF, wsMph, dewp;

    cout << "this program will calculate wind chill and cloud base\n";
    cout << "please enter temperature in fahrenheit\n";
    cin >> tempF;

    cout << "enter the wind speed in Mph\n";
    cin >> wsMph;

    cout << "finally enter the dew point\n";
    cin >> dewp;

    double windC, CBH;
	
    calcWindChill(tempF, wsMph, windC);
    calcCloudBase(tempF, dewp, CBH);

    cout << "the wind chill is " << windC << endl;
    cout << "the cloud base height " << CBH << endl;

    return 0;
}
