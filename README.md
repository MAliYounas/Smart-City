# Smart-City

#include<iostream>
using namespace std;
int external_menu(){
	int option;
	ask:
	cout<<"\n|---------------|\n";
	cout<<"|1.Login        |\n";
	cout<<"|2.Sign up      |\n";
	cout<<"|3.Exit         |\n";
	cout<<"|---------------|\n";
	cin>>option;
	if(option>3||option<1){
		cout<<"\nInvalid input try again <3"<<endl;
		goto ask;
	}
	
	
}
void Login(){
}
void sign_up(){
}
class Health_Departement{
};
class Educational_Departement{
};
class Finance_Departement{
};
class Transport_Departement{
};
class Construction_Departement{
};
class Maintainence_Departement{
};
class Environmental_Departement{
};
class Police_Departement{
};
class Resource_Managment{
};
void Mayor(){
	
}


int main(){
	switch(external_menu()){
		case 1:{
			Login();
			break;	
		}
		
		case 2:{
			sign_up();
			break;
		}
		case 3:{
			return 0;
		}
	}
	
	return 0;
}
