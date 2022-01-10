# code here

#include <iostream>
#include <string>
#include <array>
#include <algorithm>



using namespace std;

bool drinkChoice();
	
int drinkFlavor(bool drinktype);
	
int main() {

	string menu[4][4] = {

		{"Coffee", "   Price (AED)", "Tea", "   Price(AED)" },
		{"Ice Coffee", "3", "Ice Tea ", "3" },
		{"Milk Coffee", "2", "Milk Tea", "2" },
		{"Black Coffee", "1", "Black Tea", "1" },
	};

	for (int i = 0; i < 4; i++) {
		for (int j{ 0 }; j < 4; j++) {
			cout << menu[i][j] << "\t\t";
		}
		cout << endl;
	}
	

	int costOfDrink = drinkFlavor(drinkChoice());

	string withSugar;
	int moneyGiven;

	cout << endl << "Hey would you want sugar on your drink? yes or no" << endl;
	getline(cin, withSugar);
	while (!(withSugar == "yes" || withSugar == "no" )) {
		cout << "Seems the input you wrote is wrong, just write yes or no " << endl;
		getline(cin, withSugar);		
	}

	cout << endl  << "So your order comes up to " << costOfDrink << " AED " << endl << "Amount of Money to give: ";
	cin >> moneyGiven;
	while (cin.fail() || moneyGiven >1000 || moneyGiven < costOfDrink  ) {
		cout << "The input doesnt seem to be correct, either we dont have change for that amount right now or its not enough\nPlease enter another amount: ";
		cin.clear();
		cin.ignore(1000, '\n');
		cin >> moneyGiven;
	}

	if ((moneyGiven - costOfDrink) > 0) {
		cout << endl << "Here is your " << (moneyGiven - costOfDrink) << " AED change" ;
	}

	cout << endl << "Enjoy your drink and have a nice day!" << endl;
}

bool drinkChoice() {

	string coffeeOrTea{};

	cout << endl << "Hey what kind of drink do you want, Coffee or tea?" << endl;
	getline(cin, coffeeOrTea);
	transform(coffeeOrTea.begin(), coffeeOrTea.end(), coffeeOrTea.begin(), ::tolower); //to turn the string to lowercase

	while (!(coffeeOrTea == "coffee" || coffeeOrTea == "tea")) {
		cout << "Seems the input you wrote is wrong, the only choices is either coffee or tea " << endl;
		getline(cin, coffeeOrTea);
		transform(coffeeOrTea.begin(), coffeeOrTea.end(), coffeeOrTea.begin(), ::tolower);
	}

	if (coffeeOrTea == "coffee") {
		return true;
	}
	else if (coffeeOrTea == "tea") {
		return false;
	}
}

int drinkFlavor(bool drinktype) {

	string flavor;
	char useless;

	if (drinktype) {
		cout << endl << "Would that be Ice coffee, Milk coffee or Black coffee?" << endl;
		getline(cin, flavor);
		transform(flavor.begin(), flavor.end(), flavor.begin(), ::tolower);
		while (!(flavor == "ice coffee" || flavor == "milk coffee" || flavor == "black coffee")) {
			cout << "Seems the input you wrote is wrong, the only choices is Ice coffee, Milk coffee or Black coffee " << endl;
			getline(cin, flavor);
			transform(flavor.begin(), flavor.end(), flavor.begin(), ::tolower);
		}
	}
	else {
		cout << endl << "Would that be Ice tea, Milk tea or Black tea?" << endl;
		getline(cin, flavor);
		transform(flavor.begin(), flavor.end(), flavor.begin(), ::tolower);
		while (!(flavor == "ice tea" || flavor == "milk tea" || flavor == "black tea")) {
			cout << "Seems the input you wrote is wrong, the only choices is Ice tea, Milk tea or Black tea " << endl;
			getline(cin, flavor);
			transform(flavor.begin(), flavor.end(), flavor.begin(), ::tolower);
		}
	}

	useless = flavor.at(0);

	switch (useless)
	{
	case 'i': {
		return 3;
		break;
	}
	case 'm': {
		return 2;
		break;
	}
	case 'b': {
		return 1;
		break;
	}
	}
}
