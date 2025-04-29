#include <iostream>
#include <fstream>
#include <string>
#include <cmath>
#include <iomanip>
#include <ctime>
#include<array>
using namespace std;
string filepath1 = "initial";
string filepath2 = "initial";
void beauty()
{
    cout << "\n\n******************************************************************************\n\n";
    return;
}
char menu_external()
{
ask:
    char option_exter;
    cout << endl
         << endl
         << endl
         << endl;
    cout << "                                            -----------------------------------------------------------------------        " << endl
         << endl;
    cout << "                                                                       Login(Enter:L)" << endl
         << endl;
    cout << "                                                                Openning new account (Enter:O)            " << endl
         << endl;
    cout << "                                                                         Exit (Enter:E)" << endl
         << endl;
    cout << "                                         Enter what you want to choose :";
    cin >> option_exter;
    cout << endl
         << endl;
    cout << "                                            -----------------------------------------------------------------------        " << endl
         << endl;
    

    if (option_exter !='L' && option_exter != 'O' && option_exter != 'E')
    {
        cout << "\nInvalid input try again <3" << endl;
        goto ask;
    }
    return option_exter;
}
array<string, 2> login(){
    string username;
    string password;
    string line;
    string user_data[2];
    int user_name_position=0;
    ask:
    int count=0;
    beauty();
    cout<<"ENTER YOUR USERNAME : ";
    cin>>username;
    beauty();
    cout<<endl;
    cin.ignore();
    cout<<"ENTER YOUR PASSWORD : ";
    cin>>password;
    beauty();
    cout<<endl;
     fstream passw;
     passw.open("passwords_username.txt",ios::in);
     while(getline(passw,line)){
        if(username==line){
            count++;
            goto checked_username;
        }
        user_name_position++;
     }
     checked_username:
      passw.close();
     passw.open("passwords_username.txt",ios::in);
     int password_check=0;
     while(getline(passw,line)){
        if(password==line ){
        if(password_check ==(user_name_position+1)){
            count++;
        }
        }
        password_check++;
     }
     passw.close();
    if(count<2){
        cout<<"DATA IS INVALID .ENTER CORRECT DATA"<<endl;
        goto ask;
    }
        if(count==2){
            array<string, 2> user_data = {username, password};
            return user_data;
        }
        array<string, 2> just = {"sjwdb", "wdnjkqn"};
        return just;
        
}

void sign_up()
{
    string name;
    int no_of_account = 0;
    int account_no_start = 1;
    string password;
    string line;
    string username;
    int account_no;
ask:
    beauty();
    cout << "ENTER YOUR NAME : ";
    cin.ignore();
    getline(cin, name);
    beauty();
    cout << "USERNAME SHOULD BE OF SINGLE WORD IF WITH SPACES THE FIRST WILL BE CONSIDERED BUT REST WILL BE ELIMINATED" << endl
         << endl;
    cout << "ENTER YOUR USERNAME : ";
    cin >> username;
    beauty();
    cout << "PASSWORD SHOULD BE OF SINGLE WORD IF WITH SPACES THE FIRST WILL BE CONSIDERED BUT REST WILL BE ELIMINATED" << endl
         << endl;
    cout << "ENTER YOUR PASSWORD : ";
    cin >> password;
    beauty();
    string check;
    fstream passw;
    passw.open("passwords_username.txt", ios::in);
    while (getline(passw, check))
    {
        if (check == username)
        {
            passw.close();
            cout << "\nUSERNAME ALREADY TAKEN PLEASE TRY ANOTHER ONE . <3" << endl;
            goto ask;
        }
        if (check == password)
        {
            passw.close();
            cout << "\nPASSWORD ALREADY TAKEN PLEASE TRY ANOTHER ONE . <3" << endl;
            goto ask;
        }
    }
    passw.close();
    if (name.empty() || password.empty() || username.empty())
    {
        cout << "Invalid Data" << endl;
        goto ask;
    }
    if (!name.empty() && !password.empty() && !username.empty())
    {
        fstream info;
        info.open("information.txt", ios::out | ios::app);
        info << name << endl;
        info.close();
        fstream opening;
        opening.open("accounts_no.txt", ios::in);
        while (getline(opening, line))
        {
            no_of_account++;
        }
        opening.close();
        opening.open("accounts_no.txt", ios::out | ios::app);
        account_no = (account_no_start + no_of_account);
        opening << account_no << endl;
        opening.close();
        cout << "YOUR ACCOUNT NO. IS : " << (account_no_start + no_of_account) << endl;

        passw.open("passwords_username.txt", ios::out | ios::app);
        passw << username << endl;
        passw << password << endl;
        passw.close();
    }
    cout <<"THANKS FOR OPENNING AN ACCOUNT <3" << endl;
    beauty();
}
class Health_Department
{
	private:
		int doctors;
		int nurses;
		int no_of_beds;
	protected:
		int level;
		int employees;
		double salaries;
	public:
		Health_Department(int level, double salaries, int employees,int doctors, int no_of_beds, int nurses){
        this->level=level;
		this->doctors=doctors;
		this->employees=employees;
		this->no_of_beds=no_of_beds;
		this->nurses=nurses;
		this->salaries=salaries;
		}
		Health_Department(int level, int employees, double salaries){
			this->employees=employees;
			this->level=level;
			this->salaries=salaries;
		}
		void update(){
            beauty();
            cout<<"\n                   What do you want to update in Health Department?"<<endl;
            cout<<"1.Doctors"<<endl;
            cout<<"2.Nurses"<<endl;
            cout<<"3.No of beds"<<endl;
            cout<<"4.Salaries"<<endl;
            cout<<"5.Employees"<<endl;
            cout<<"6.Level"<<endl;
            cout<<"7.Exit"<<endl;
            beauty();
            cout<<"Enter the option : ";
            int option;
            cin>>option;
            if(option ==1){
                cout<<"Enter the new number of doctors : ";
                cin>>doctors;
            }
            else if(option==2){
                cout<<"Enter the new number of nurses : ";
                cin>>nurses;
            }
            else if(option==3){
                cout<<"Enter the new number of beds : ";
                cin>>no_of_beds;
            }
            else if(option==4){
                cout<<"Enter the new salaries : ";
                cin>>salaries;
            }
            else if(option==5){
                cout<<"Enter the new number of employees : ";
                cin>>employees;
            }
            else if(option==6){
                cout<<"Enter the new level : ";
                cin>>level;
            }
            else if(option==7){
                return;
            }
            else{
                cout<<"Invalid input"<<endl;
            }
            beauty();
            cout<<"Updated successfully"<<endl;
            beauty();
		}
        void display_new(){
            cout<<"Level : "<<level<<endl;
            cout<<"Employees : "<<employees<<endl;
            cout<<"Salaries : "<<salaries<<endl;
            cout<<"Doctors : "<<doctors<<endl;
            cout<<"Nurses : "<<nurses<<endl;
            cout<<"No of beds : "<<no_of_beds<<endl;
        }
		
};
class Educational_Department:virtual public Health_Department
{
	private:
		int students;
		int teachers;
		int no_of_classrooms;
		public:
			Educational_Department(int level, double salaries, int employees,int students, int teachers, int no_of_classrooms):Health_Department( level, employees, salaries){
				this->students=students;
				this->teachers=teachers;
				this->no_of_classrooms=no_of_classrooms;
				
			}
			
			void update(){
                beauty();
                cout<<"\n               What do you want to update in Educational Department?"<<endl;
                cout<<"1.Students"<<endl;
                cout<<"2.Teachers"<<endl;
                cout<<"3.No of classrooms"<<endl;
                cout<<"4.Salaries"<<endl;
                cout<<"5.Employees"<<endl;
                cout<<"6.Level"<<endl;
                cout<<"7.Exit"<<endl;
                beauty();
                cout<<"Enter the option : ";
                int option;
                cin>>option;
              switch (option)
              {
              case 1:
                cout<<"Enter the new number of students : ";
                cin>>students;
                break;
                case 2:
                cout<<"Enter the new number of teachers: ";
                cin>>teachers;
                break;
                case 3:
                cout<<"Enter the new number of classrooms : ";
                cin>>no_of_classrooms;
                break;
                case 4:
                cout<<"Enter the new salaries : ";
                cin>>salaries;
                break;
                case 5:
                cout<<"Enter the new number of employees : ";
                cin>>employees;
                break;
                case 6:
                cout<<"Enter the new level : ";
                cin>>level;
                break;
                case 7:
                cout<<"Exit"<<endl;
               return ;
                break;
                default:
                cout<<"Invalid input"<<endl;
                break;

              }
                beauty();
                cout<<"Updated successfully"<<endl;
                beauty();
		}
        void display_new(){
            cout<<"Level : "<<level<<endl;
            cout<<"Employees : "<<employees<<endl;
            cout<<"Salaries : "<<salaries<<endl;
            cout<<"Students : "<<students<<endl;
            cout<<"Teachers : "<<teachers<<endl;
            cout<<"No of classrooms : "<<no_of_classrooms<<endl;
        }
			
			
		
};
class Finance_Department
{
	
		
};
class Transport_Department:virtual public Health_Department
{
	private:
		int no_of_electricvehicles;
		int no_of_petrolvehicles;
		int no_of_dieselvehicles;
		int trafficlights;
		public:
			Transport_Department(int level, double salaries, int employees,int no_of_electricvehicles, int no_of_petrolvehicles, int no_of_dieselvehicles, int trafficlights):Health_Department( level, employees, salaries){
				this->no_of_electricvehicles=no_of_electricvehicles;
				this->no_of_petrolvehicles=no_of_petrolvehicles;
				this->no_of_dieselvehicles=no_of_dieselvehicles;
				this->trafficlights=trafficlights;
				
			}
			void update(){
                beauty();
                cout<<"\n                   What do you want to update in Transport departement: ";
                cout<<"1.No of electric vehicles"<<endl;
                cout<<"2.No of petrol vehicles"<<endl;
                cout<<"3.No of diesel vehicles"<<endl;
                cout<<"4.Traffic lights"<<endl;
                cout<<"5.Salaries"<<endl;
                cout<<"6.Employees"<<endl;
                cout<<"7.Level"<<endl;
                cout<<"8.Exit"<<endl;
                beauty();
                int option;
                cout<<"\nEnter the option : ";
                cin>>option;
                switch (option)
                {
                case 1:
                cout<<"Enter the new number of electric vehicles : ";
                cin>>no_of_electricvehicles;
                break;
                case 2:
                cout<<"Enter the new number of petrol vehicles : ";
                cin>>no_of_petrolvehicles;
                break;
                case 3:
                cout<<"Enter the new number of diesel vehicles : ";
                cin>>no_of_dieselvehicles;
                break;
                case 4:
                cout<<"Enter the new number of traffic lights : ";
                cin>>trafficlights;
                break;
                case 5:
                cout<<"Enter the new salaries : ";
                cin>>salaries;
                break;
                case 6:
                cout<<"Enter the new number of employees: ";
                cin>>employees;
                break;
                case 7:
                cout<<"Enter the new level: ";
                cin>>level;
                break;
                case 8:
                cout<<"Exiting .....";
                return;
                break;
                default:
                cout<<"Invalid input"<<endl;
                break;
                }
                beauty();
                cout<<"Updated successfully"<<endl;
                beauty();
		}
        void display_new(){
            cout<<"Level : "<<level<<endl;
            cout<<"Employees : "<<employees<<endl;
            cout<<"Salaries : "<<salaries<<endl;
            cout<<"No of electric vehicles : "<<no_of_electricvehicles<<endl;
            cout<<"No of petrol vehicles : "<<no_of_petrolvehicles<<endl;
            cout<<"No of diesel vehicles : "<<no_of_dieselvehicles<<endl;
            cout<<"Traffic lights : "<<trafficlights<<endl;
        }
        
			
};
class Construction_Department:virtual public Health_Department
{
	private:
		int no_of_resedentialbuildings;
		int no_of_industrialbuildings;
		int no_of_roads;
		int no_of_parks;
		public:
			Construction_Department(int level, double salaries, int employees,int no_of_resedentialbuildings, int no_of_roads ,  int no_of_industrialbuildings, int no_of_parks ):Health_Department( level, employees, salaries){
				this-> no_of_industrialbuildings=no_of_industrialbuildings;
				this->no_of_roads= no_of_roads;
				this->no_of_parks=no_of_parks;
				this->no_of_resedentialbuildings=no_of_resedentialbuildings;
			}	
		void update(){
            beauty();
            cout<<"\n                   What do you want to update in Construction Department?"<<endl;
            cout<<"1.No of resedential buildings"<<endl;
            cout<<"2.No of industrial buildings"<<endl;
            cout<<"3.No of roads"<<endl;
            cout<<"4.No of parks"<<endl;
            cout<<"5.Salaries"<<endl;
            cout<<"6.Employees"<<endl;
            cout<<"7.Level"<<endl;
            cout<<"8.Exit"<<endl;
            beauty();
            int option;
            cout<<"Enter the option : ";
            cin>>option;
            switch (option)
            {
                case 1:
                cout<<"Enter the new number of resedential buildings : ";
                cin>>no_of_resedentialbuildings;
                break;
                case 2:
                cout<<"Enter the new number of industrial buildings : ";
                cin>>no_of_industrialbuildings;
                break;
                case 3:
                cout<<"Enter the new number of roads : ";
                cin>>no_of_roads;
                break;
                case 4:
                cout<<"Enter the new number of parks : ";
                cin>>no_of_parks;
                break;
                case 5:
                cout<<"Enter the new salaries : ";
                cin>>salaries;
                break;
                case 6:
                cout<<"Enter the new number of employees : ";
                cin>>employees;
                break;
                case 7:
                cout<<"Enter the new level : ";
                cin>>level;
                break;
                case 8:
                cout<<"Exiting .....";
                return;
                break;
                default:
                cout<<"Invalid input"<<endl;
                break;
		}
            beauty();
        cout<<"Updated successfully"<<endl;
        beauty();
        }
        void display_new(){
            cout<<"Level : "<<level<<endl;
            cout<<"Employees : "<<employees<<endl;
            cout<<"Salaries : "<<salaries<<endl;
            cout<<"No of resedential buildings : "<<no_of_resedentialbuildings<<endl;
            cout<<"No of industrial buildings : "<<no_of_industrialbuildings<<endl;
            cout<<"No of roads : "<<no_of_roads<<endl;
            cout<<"No of parks : "<<no_of_parks<<endl;
        }
};
class Police_Department:virtual public Health_Department
{
	
	private:
		int no_of_stations;
		
		public:
			Police_Department(int level, double salaries, int employees,int no_of_stations):Health_Department( level, employees, salaries){
				this->no_of_stations=no_of_stations;	
			}
			void update(){
                beauty();
                cout<<"\n               What do you want to update in Police department: ";
                cout<<"1.No of stations"<<endl;
                cout<<"2.Salaries"<<endl;
                cout<<"3.Employees"<<endl;
                cout<<"4.Level"<<endl;
                cout<<"5.Exit"<<endl;
                beauty();
                int option;
                cout<<"Enter the option : ";
                cin>>option;
                switch (option)
                {
                    case 1:
                    cout<<"Enter the new number of stations : ";
                    cin>>no_of_stations;
                    break;
                    case 2:
                    cout<<"Enter the new salaries : ";
                    cin>>salaries;
                    break;
                    case 3:
                    cout<<"Enter the new number of employees : ";
                    cin>>employees;
                    break;
                    case 4:
                    cout<<"Enter the new level : ";
                    cin>>level;
                    break;
                    case 5:
                    cout<<"Exiting .....";
                    return;
                    break;
                    default:
                    cout<<"Invalid input"<<endl;
                    break;
				
			}
            beauty();
            cout<<"Updated successfully"<<endl;
            beauty();
        }
        void display_new(){
            cout<<"Level : "<<level<<endl;
            cout<<"Employees : "<<employees<<endl;
            cout<<"Salaries : "<<salaries<<endl;
            cout<<"No of stations : "<<no_of_stations<<endl;
        }  
			
};
class Maintainence_Department:virtual public Health_Department
{
	private:
	int pending_requests;
	int completed_tasks;
	public:
		Maintainence_Department(int level, double salaries, int employees,int pending_requests, int completed_tasks):Health_Department( level, employees, salaries)
		{
			this->pending_requests=pending_requests;
			this->completed_tasks=completed_tasks;
			}
			
			void update(){
                beauty();
                cout<<"\n                   What do you want to update in Maintainence department: ";
                cout<<"1.Pending requests"<<endl;
                cout<<"2.Completed tasks"<<endl;
                cout<<"3.Salaries"<<endl;
                cout<<"4.Employees"<<endl;
                cout<<"5.Level"<<endl;
                cout<<"6.Exit"<<endl;
                beauty();
                int option;
                cout<<"Enter the option : ";
                cin>>option;
                switch (option)
                {
                    case 1:
                    cout<<"Enter the new number of pending requests : ";
                    cin>>pending_requests;
                    break;
                    case 2:
                    cout<<"Enter the new number of completed tasks : ";
                    cin>>completed_tasks;
                    break;
                    case 3:
                    cout<<"Enter the new salaries : ";
                    cin>>salaries;
                    break;
                    case 4:
                    cout<<"Enter the new number of employees : ";
                    cin>>employees;
                    break;
                    case 5:
                    cout<<"Enter the new level : ";
                    cin>>level;
                    break;
                    case 6:
                    cout<<"Exiting .....";
                    return;
                    break;
                    default:
                    cout<<"Invalid input"<<endl;
                    break;
			}
            beauty();
            cout<<"Updated successfully"<<endl;
            beauty();
        }
        void display_new(){
            cout<<"Level : "<<level<<endl;
            cout<<"Employees : "<<employees<<endl;
            cout<<"Salaries : "<<salaries<<endl;
            cout<<"Pending requests : "<<pending_requests<<endl;
            cout<<"Completed tasks : "<<completed_tasks<<endl;
        }
			
				
};
class Environmental_Department: virtual public Health_Department
{
	private:
		int no_of_parks;
		double renewableresources;
		public:
			Environmental_Department(int level, double salaries, int employees,int no_of_parks, double renewableresources):Health_Department(level, employees, salaries){
				this->no_of_parks=no_of_parks;
				this->renewableresources=renewableresources;
			}
			
				void update(){
                    beauty();
                    cout<<"\n               What do you want to update in Enviornmental department: ";
                    cout<<"1.No of parks"<<endl;
                    cout<<"2.Renewable resources"<<endl;
                    cout<<"3.Salaries"<<endl;
                    cout<<"4.Employees"<<endl;
                    cout<<"5.Level"<<endl;
                    cout<<"6.Exit"<<endl;
                    beauty();
                    cout<<"Enter the option : ";
                    int option;
                    cin>>option;
                    switch (option)
                    {
                        case 1:
                        cout<<"Enter the new number of parks : ";
                        cin>>no_of_parks;
                        break;
                        case 2:
                        cout<<"Enter the new renewable resources : ";
                        cin>>renewableresources;
                        break;
                        case 3:
                        cout<<"Enter the new salaries : ";
                        cin>>salaries;
                        break;
                        case 4:
                        cout<<"Enter the new number of employees : ";
                        cin>>employees;
                        break;
                        case 5:
                        cout<<"Enter the new level : ";
                        cin>>level;
                        break;
                        case 6:
                        cout<<"Exiting .....";
                        return;
                        break;
                        default:
                        cout<<"Invalid input"<<endl;
                        break;
			}
            beauty();
            cout<<"Updated successfully"<<endl;
            beauty();
        }
        void display_new(){
            cout<<"Level : "<<level<<endl;
            cout<<"Employees : "<<employees<<endl;
            cout<<"Salaries : "<<salaries<<endl;
            cout<<"No of parks : "<<no_of_parks<<endl;
            cout<<"Renewable resources : "<<renewableresources<<endl;
        }
			
			
};

class Resource_Managment: virtual public Health_Department
{ 
private:
	int water_reserviors;
	int power_plant;
	public:
		Resource_Managment(int level, double salaries, int employees,int water_reserviors, int power_plant):Health_Department(level,employees ,salaries){
			this->water_reserviors=water_reserviors;
			this->power_plant=power_plant;
		}
		
		void update(){
            beauty();
            cout<<"\n                   What do you want to update in Resource Managment department: ";
            cout<<"1.Water reserviors"<<endl;
            cout<<"2.Power plant"<<endl;
            cout<<"3.Salaries"<<endl;
            cout<<"4.Employees"<<endl;
            cout<<"5.Level"<<endl;
            cout<<"6.Exit"<<endl;
            beauty();
            cout<<"Enter the option : ";
            int option;
            cin>>option;
            switch (option)
            {
                case 1:
                cout<<"Enter the new number of water reserviors : ";
                cin>>water_reserviors;
                break;
                case 2:
                cout<<"Enter the new number of power plants : ";
                cin>>power_plant;
                break;
                case 3:
                cout<<"Enter the new salaries : ";
                cin>>salaries;
                break;
                case 4:
                cout<<"Enter the new number of employees : ";
                cin>>employees;
                break;
                case 5:
                cout<<"Enter the new level : ";
                cin>>level;
                break;
                case 6:
                cout<<"Exiting .....";
                return;
                break;
                default:
                cout<<"Invalid input"<<endl;
                break;
		}
            beauty();
        cout<<"Updated successfully"<<endl;
        beauty();
        }
        void display_new (){
            cout<<"Level : "<<level<<endl;
            cout<<"Employees : "<<employees<<endl;
            cout<<"Salaries : "<<salaries<<endl;
            cout<<"Water reserviors : "<<water_reserviors<<endl;
            cout<<"Power plant : "<<power_plant<<endl;
        }
		
	
};
class Overall_Status{
    public:
    float satisfaction_level;
    float minimum_salaries;
    float Total_Resorces;
    int population;
    int green_levels;
    float  sustainable_living;
    float  clean_energy;
    public:
    Overall_Status(float satisfaction_level,float minimum_salaries,float Total_Resorces,int population,int green_levels,float  sustainable_living,float  clean_energy){
        this->satisfaction_level=satisfaction_level;
        this->minimum_salaries=minimum_salaries;
        this->Total_Resorces=Total_Resorces;
        this->population=population;
        this->green_levels=green_levels;
        this->sustainable_living=sustainable_living;
        this->clean_energy=clean_energy;              
    }
    void Display(){
        beauty();
        cout<<"\n                           OVERALL STATUS                            "<<endl<<endl;
        cout<<"\n                                                                        TOTAL RESOURCES : "<<Total_Resorces<<"$"<<endl;
        cout<<"\nSATISFACTION LEVEL : "<<satisfaction_level<<"%"<<endl;
        cout<<"\nMINIMUM SALARY : "<<minimum_salaries<<"$"<<endl;
        cout<<"\nPOPULATION : "<<population<<endl;
        cout<<"\nGREEEN LEVELS : "<<green_levels<<"%"<<endl;
        cout<<"\nSASTAINABLE LIVING :"<<sustainable_living<<endl;
        cout<<"\nCLEAN ENERGY :"<<clean_energy<<endl;
        beauty();



    }
};
int interlinking_menu(){
    ask:
    int option;
    beauty();
    cout<<"\n1. SEE HOW OVERALL CITY IS DOING."<<endl;
    cout<<"\n2. EXERCISE YOUR POWERS TO MAKE CHANGES IN DEPARTMENTS"<<endl;
    cout<<"\n3. COLLABORATE IN VIRTUAL CLIMATE SUMMIT."<<endl;
    cout<<"\n4. EXIT."<<endl;
    cout<<"\nENTER : ";
    cin>>option;
    if (option<1 || option>4)
    {
        cout << "\nInvalid input try again <3" << endl;
        goto ask;
    }
    beauty();
    return(option);
}

int excercising_powers_menu(){
    int option;
    ask:
    beauty();
    cout<<"\n                          YOU CAN MAKE CHANGES IN THE RESPECTIVE DEPARTMENTS<3"<<endl;
    cout<<"\n1.Environment Department"<<endl;    
    cout<<"\n2.Construction Department"<<endl;    
    cout<<"\n3.Maintenance Department"<<endl;    
    cout<<"\n4.Finance Department"<<endl;
    cout<<"\n5.Education Department"<<endl;
    cout<<"\n6.Health Department"<<endl;
    cout<<"\n7.Transport Department"<<endl;
    cout<<"\n8.Police Department"<<endl;
    cout<<"\n9.Exit"<<endl;
    cin>>option;
    if (option<1 || option>9)
    {
        cout << "\nInvalid input try again <3" << endl;
        goto ask;
    }
    beauty();
    return(option);

}
void Setup()
{
    bool runnning=true;
    int option_interlinking_menu;
    while(runnning){
        option_interlinking_menu=interlinking_menu();
        switch (option_interlinking_menu)
        {
        case 1:{
            fstream my_file2;
            my_file2.open(filepath2,ios::in);
            if(!my_file2.is_open()){
               cout<<"Failed to Open File "<<endl;
            }
            else{
                if(my_file2.peek() == EOF){
                    Overall_Status city(0,0,100000,0,0,0,0);
                    city.Display();

            }
            my_file2.close();

            
            break;
        }}
        case 2:{
            int option;
            option=excercising_powers_menu();
            switch (option)
            {
            case 1:{
                
                break;
            }
            case 2:{
                
                break;
            }
            case 3:{
                
                break;
            }
            case 5:{
                
                break;
            }
            case 6:{
                
                break;
            }
            case 7:{
                
                break;
            }
            case 8:{
                
                break;
            }
            case 9:{
                
                break;
            }
            
        }
        case 3:{
            
            break;
        }
        case 4:{
            
            break;
        }

    }
			
    }
    }
}
void Mayor()
{
    int option;
    beauty();
    cout<<"\n                       WELCOME SIR BACK TO THE OFFICE .<3"<<endl;
    cout<<"\nMAY YOU SERVVE THE PEOPLE OF CITY AND MAKE DESICIONS ACCORDING TO THE WELFARE OF SOCIETY"<<endl;
    beauty();
    Setup();
}

int main()
{
    bool  close_external=true;
    array<string, 2> user_data;
    do{
        char option_external;
        option_external = menu_external();
        switch (option_external)
        {
        case 'L':{
             user_data=login();
             filepath1=(user_data[0] +"_current_Balance.txt");
             fstream my_file1;
             my_file1.open(filepath1,ios::app);
             if(!my_file1.is_open()){
                cout<<"Failed to Open File "<<endl;
             }
             my_file1.close();
             filepath2=(user_data[0] +"_Overall_status.txt");
             fstream my_file2;
             my_file2.open(filepath2,ios::app);
             if(!my_file2.is_open()){
                cout<<"Failed to Open File "<<endl;
             }
             my_file2.close();

            close_external=false;
            break;
        }
        case 'O':{
            sign_up();
            break;
        }
        case 'E':{
            return 0;
        }   
    }
    }while(close_external==true);
return 0;
}
