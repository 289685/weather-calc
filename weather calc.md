#include <iostream>
#include <string>
#include <sstream>
using namespace std;
void intro();
void getinput(int& father,int& mother, int& end);
void displaysquare(int& father,int& mother);
void loop(int& end);

int main()
{
	int father, mother, end;
	end = 1;
	do {
		intro();
		getinput(father,mother,end);
		displaysquare(father,mother);
		loop(end);
	} while (end != 1);


	return 0;
}
void intro() {
	cout<<"this program will calculate the chances of having colorblindness\n";
}
void getinput(int& father,int& mother, int& end) {
	cout<<"if the father is colorblind enter 1, if not press 2\n";
	cin>>father;
	cout<<"if the mother is colorblind press 1, if shes a silent carrier press 2, if not press 3\n";
	cin>>mother;
}
void displaysquare(int& father,int& mother) {
	if (father == 1 & mother == 1) {
		cout << "              Xc       |        Y\n";
		cout << "       ---------------------------------\n";
		cout << "   Xc  |     XcXc      |       XcY     |\n";
		cout << "----------------------------------------\n";
		cout << "   Xc  |     XcXc      |       XcY     |\n";
		cout << "       ---------------------------------\n";
	} else if (father == 1 & mother == 2) {
		cout << "              Xc       |        Y\n";
		cout << "       ---------------------------------\n";
		cout << "   Xc  |     XcXc      |       XcY     |\n";
		cout << "----------------------------------------\n";
		cout << "   X   |     XcX       |       XY      |\n";
		cout << "       ---------------------------------\n";
	} else if (father == 1 & mother == 3) {
		cout << "              Xc       |        Y\n";
		cout << "       ---------------------------------\n";
		cout << "   X   |      XcX      |        XY     |\n";
		cout << "----------------------------------------\n";
		cout << "   X   |      XcX      |        XY     |\n";
		cout << "       ---------------------------------\n";
	} else if (father == 2 & mother == 1) {
		cout << "               X       |        Y\n";
		cout << "       ---------------------------------\n";
		cout << "   Xc  |      XXc      |       XcY     |\n";
		cout << "----------------------------------------\n";
		cout << "   Xc  |      XXc      |       XcY     |\n";
		cout << "       ---------------------------------\n";
	} else if (father == 2 & mother == 2) {
		cout << "               X       |        Y\n";
		cout << "       ---------------------------------\n";
		cout << "   Xc  |      XXc      |       XcY     |\n";
		cout << "----------------------------------------\n";
		cout << "   X   |      XX       |       XY      |\n";
		cout << "       ---------------------------------\n";
	} else if (father == 2 & mother == 3) {
		cout << "               X       |        Y\n";
		cout << "       ---------------------------------\n";
		cout << "   X   |       XX      |        XY     |\n";
		cout << "----------------------------------------\n";
		cout << "   X   |       XX      |        XY     |\n";
		cout << "       ---------------------------------\n";
	} else {
		cout << "Invalid inputs\n";
	}
}
void loop(int& end) {
	cout << "Would you like to run another simulation press 1 for yes, for no press any other key \n";
	cin >> end;
	if (end == 1) {

	} else {
	}
}
