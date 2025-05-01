#include <iostream>
#include <fstream>
#include <string>
#include <cmath>
#include <iomanip>
#include <ctime>
#include<array>
using namespace std;
string filepath1 = "initial";//For login
string filepath2 = "initial";//For Overall status
string Username="initial";
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
//Forward Declaration 
class Health_Department{};
class Overall_Status{
    public:
    float satisfaction_level;
    float minimum_salaries;
    float Total_Resources;
    int population;
    int green_levels;
    float  sustainable_living;
    float  clean_energy;
    float money;
    Overall_Status(float satisfaction_level,float minimum_salaries,float Total_Resources,int population,int green_levels,float  sustainable_living,float  clean_energy,  float money){
        this->satisfaction_level=satisfaction_level;
        this->minimum_salaries=minimum_salaries;
        this->Total_Resources=Total_Resources;
        this->population=population;
        this->green_levels=green_levels;
        this->sustainable_living=sustainable_living;
        this->clean_energy=clean_energy;
        this->money=money;              
    }
    void Display(){
        beauty();
        cout<<"\n                           OVERALL STATUS                            "<<endl<<endl;
        cout<<"\n                                                                        TOTAL RESOURCES : "<<Total_Resources<<"$"<<endl;
        cout<<"\nSATISFACTION LEVEL : "<<satisfaction_level<<"%"<<endl;
        cout<<"\nMINIMUM SALARY : "<<minimum_salaries<<"$"<<endl;
        cout<<"\nPOPULATION : "<<population<<endl;
        cout<<"\nGREEEN LEVELS : "<<green_levels<<"%"<<endl;
        cout<<"\nSASTAINABLE LIVING :"<<sustainable_living<<endl;
        cout<<"\nCLEAN ENERGY :"<<clean_energy<<endl;
        beauty();
    }
        void UpdateCity() {
            // Population growth
            float growth = 0.01;
            if (satisfaction_level > 0.7) growth += 0.005;
            if (sustainable_living> 0.6) growth += 0.003;
            population += population * growth;
    
            // Economy
            float taxes = population * minimum_salaries * 0.1;
            if (sustainable_living > 0.7) taxes *= 1.1;
            float costs = population * 50;
            money += taxes - costs;
    
            // Happiness
            float new_happy = 0.5;
            new_happy += green_levels/500.0;
            new_happy += sustainable_living/10.0;
            new_happy += clean_energy/10.0;
            satisfaction_level = 0.7*satisfaction_level + 0.3*new_happy;
        
        if (satisfaction_level < 0) satisfaction_level = 0;
        if (satisfaction_level > 1) satisfaction_level = 1;
        if(money < 0)money = 0;
        if (population < 0) population = 0;
        green_levels = sustainable_living* 100;
    }


    
    friend class Health_Department;
};
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
        void update(Overall_Status & status) {
    beauty();
    cout << "\n========= Health Department Update Menu =========\n";
    cout << "1. Update Number of Doctors\n";
    cout << "2. Update Number of Nurses\n";
    cout << "3. Update Number of Beds\n";
    cout << "4. Increase Salaries (by % for N employees)\n";
    cout << "5. Update Number of Employees\n";
    cout << "6. Upgrade Department Level\n";
    cout << "7. Exit\n";
    cout << "=================================================\n";
    cout << "Enter your option (1-7): ";

    int option;
    cin >> option;

    switch(option) {
        case 1: {
            int new_doctors;
            cin >> new_doctors;
            int increase = new_doctors - doctors;
            if (increase > 0) {
                float cost = increase * 5000;
              if (status.Total_Resources >= cost) {
                   doctors = new_doctors;
                    status.Total_Resources -= cost;
                    status.satisfaction_level += 0.001 * increase;
                    cout << "✅ Doctors increased. Rs. " << cost << " spent.\n";
                } else {
                    cout << "❌ Not enough resources.\n"; 
                }
            } else {
                doctors = new_doctors;
            }
            break;
        }

        case 2: {
            int new_nurses;
            cin >> new_nurses;
            int increase = new_nurses - nurses;
            if (increase > 0) {
                float cost = increase * 3000;
                if (status.Total_Resources >= cost) {
                    nurses = new_nurses;
                    status.Total_Resources -= cost;
                    status.satisfaction_level += 0.0008 * increase;
                    cout << "✅ Nurses increased. Rs. " << cost << " spent.\n";
                } else {
                    cout << "❌ Not enough resources.\n";
                }
            } else {
                nurses = new_nurses;
            }
            break;
        }

        case 3: {
            int new_beds;
            cin >> new_beds;
            int increase = new_beds - no_of_beds;
            if (increase > 0) {
                float cost = increase * 2000;
                if (status.Total_Resources >= cost) {
                    no_of_beds = new_beds;
                    status.Total_Resources -= cost;
                    status.satisfaction_level += 0.0005 * increase;
                    cout << "✅ Beds increased. Rs. " << cost << " spent.\n";
                } else {
                    cout << "❌ Not enough resources.\n";
                }
            } else {
                no_of_beds = new_beds;
            }
            break;
        }

        case 4: {
            double percent;
            int num_employees;
            cin >> num_employees;
            if (num_employees > employees) {
                cout << "❌ Error: Number exceeds total employees.\n";
                break;
            }
            cin >> percent;

            double individual_salary = salaries / employees;
            double increment_per_person = individual_salary * percent / 100.0;
            double total_increment = increment_per_person * num_employees;

            if (status.Total_Resources >= total_increment) {
                salaries += total_increment;
                status.Total_Resources -= total_increment;
                status.satisfaction_level += 0.002 * num_employees;
                cout << "✅ Salaries increased. Rs. " << total_increment << " deducted from resources.\n";
            } else {
                cout << "❌ Not enough resources.\n";
            }
            break;
        }

        case 5: {
            int new_employees;
            cin >> new_employees;
            int increase = new_employees - employees;
            float cost = (increase > 0) ? increase * 4000 : 0;

            if (increase <= 0 || status.Total_Resources >= cost) {
                employees = new_employees;
                if (increase > 0) {
                    status.Total_Resources -= cost;
                    status.satisfaction_level += 0.001 * increase;
                    cout << "✅ Employees increased. Rs. " << cost << " spent.\n";
                }
                if (employees > 0)
                    status.minimum_salaries = salaries / employees;
            } else {
                cout << "❌ Not enough resources.\n";
            }
            break;
        }

        case 6: {
            int new_level;
            cin >> new_level;
            int increase = new_level - level;
            float cost = increase * 10000;

            if (increase > 0 && status.Total_Resources >= cost) {
                level = new_level;
                status.Total_Resources -= cost;
                status.satisfaction_level += 0.002 * increase;
                status.sustainable_living += 0.01 * increase;
                status.clean_energy += 0.01 * increase;
                cout << "✅ Level upgraded. Rs. " << cost << " spent.\n";
            } else if (increase <= 0) {
                level = new_level;
                cout << "Department downgraded or same.\n";
            } else {
                cout << "❌ Not enough resources.\n";
            }
            break;
        }

        case 7:
            cout << "Exiting update menu...\n";
            return;

        default:
            cout << "Invalid input.\n";
            return;
    }

    status.satisfaction_level = max(0.0f, min(1.0f, status.satisfaction_level));
    status.sustainable_living = max(0.0f, min(1.0f, status.sustainable_living));
    status.clean_energy = max(0.0f, min(1.0f, status.clean_energy));

    beauty();
    cout << "✅ Update completed successfully!\n";
    beauty();
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
			
            void update(Overall_Status &status) {
                beauty();
                cout << "\n========= Educational Department Update Menu =========\n";
                cout << "1. Update Number of Students\n";
                cout << "2. Update Number of Teachers\n";
                cout << "3. Update Number of Classrooms\n";
                cout << "4. Increase Salaries (by % for N employees)\n";
                cout << "5. Update Number of Employees\n";
                cout << "6. Upgrade Department Level\n";
                cout << "7. Exit\n";
                cout << "======================================================\n";
                cout << "Enter your option (1-7): ";
        
                int option;
                cin >> option;
        
                switch(option) {
                    case 1: {
                        int new_students;
                        cin >> new_students;
                        int increase = new_students - students;
                        float cost = (increase > 0) ? increase * 1000 : 0;
                        if (increase <= 0 || status.Total_Resources >= cost) {
                            students = new_students;
                            if (increase > 0) {
                                status.Total_Resources -= cost;
                                status.satisfaction_level += 0.0005f * increase;
                                cout << "✅ Students increased. Rs. " << cost << " spent.\n";
                            }
                        } else {
                            cout << "❌ Not enough resources.\n";
                        }
                        break;
                    }
        
                    case 2: {
                        int new_teachers;
                        cin >> new_teachers;
                        int increase = new_teachers - teachers;
                        float cost = (increase > 0) ? increase * 6000 : 0;
                        if (increase <= 0 || status.Total_Resources >= cost) {
                            teachers = new_teachers;
                            if (increase > 0) {
                                status.Total_Resources -= cost;
                                status.satisfaction_level += 0.001f * increase;
                                cout << "✅ Teachers increased. Rs. " << cost << " spent.\n";
                            }
                        } else {
                            cout << "❌ Not enough resources.\n";
                        }
                        break;
                    }
        
                    case 3: {
                        int new_rooms;
                        cin >> new_rooms;
                        int increase = new_rooms - no_of_classrooms;
                        float cost = (increase > 0) ? increase * 8000 : 0;
                        if (increase <= 0 || status.Total_Resources >= cost) {
                            no_of_classrooms = new_rooms;
                            if (increase > 0) {
                                status.Total_Resources -= cost;
                                status.satisfaction_level += 0.001f * increase;
                                cout << "✅ Classrooms increased. Rs. " << cost << " spent.\n";
                            }
                        } else {
                            cout << "❌ Not enough resources.\n";
                        }
                        break;
                    }
        
                    case 4: {
                        double percent;
                        int num_employees;
                        cin >> num_employees;
                        if (num_employees > employees) {
                            cout << "❌ Error: Number exceeds total employees.\n";
                            break;
                        }
                        cin >> percent;
                        double individual_salary = (employees > 0) ? salaries / employees : 0;
                        double increment_per_person = individual_salary * percent / 100.0;
                        double total_increment = increment_per_person * num_employees;
        
                        if (status.Total_Resources >= total_increment) {
                            salaries += total_increment;
                            status.Total_Resources -= total_increment;
                            status.satisfaction_level += 0.002f * num_employees;
                            cout << "✅ Salaries increased. Rs. " << total_increment << " deducted from resources.\n";
                        } else {
                            cout << "❌ Not enough resources.\n";
                        }
                        break;
                    }
        
                    case 5: {
                        int new_employees;
                        cin >> new_employees;
                        int increase = new_employees - employees;
                        float cost = (increase > 0) ? increase * 4000 : 0;
        
                        if (increase <= 0 || status.Total_Resources >= cost) {
                            employees = new_employees;
                            if (increase > 0) {
                                status.Total_Resources -= cost;
                                status.satisfaction_level += 0.001f * increase;
                                cout << "✅ Employees increased. Rs. " << cost << " spent.\n";
                            }
                            if (employees > 0)
                                status.minimum_salaries = salaries / employees;
                        } else {
                            cout << "❌ Not enough resources.\n";
                        }
                        break;
                    }
        
                    case 6: {
                        int new_level;
                        cin >> new_level;
                        int increase = new_level - level;
                        float cost = increase * 12000;
        
                        if (increase > 0 && status.Total_Resources >= cost) {
                            level = new_level;
                            status.Total_Resources -= cost;
                            status.satisfaction_level += 0.002f * increase;
                            status.sustainable_living += 0.01f * increase;
                            status.clean_energy += 0.005f * increase;
                            cout << "✅ Level upgraded. Rs. " << cost << " spent.\n";
                        } else if (increase <= 0) {
                            level = new_level;
                            cout << "Department downgraded or same.\n";
                        } else {
                            cout << "❌ Not enough resources.\n";
                        }
                        break;
                    }
        
                    case 7:
                        cout << "Exiting update menu...\n";
                        return;
        
                    default:
                        cout << "Invalid input.\n";
                        return;
                }
        
                status.satisfaction_level = max(0.0f, min(1.0f, status.satisfaction_level));
                status.sustainable_living = max(0.0f, min(1.0f, status.sustainable_living));
                status.clean_energy = max(0.0f, min(1.0f, status.clean_energy));
        
                beauty();
                cout << "✅ Update completed successfully!\n";
                beauty();
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
			void update(Overall_Status &status) {
                beauty();
                cout << "\n========= Transport Department Update Menu =========\n";
                cout << "1. Update Number of Electric Vehicles\n";
                cout << "2. Update Number of Petrol Vehicles\n";
                cout << "3. Update Number of Diesel Vehicles\n";
                cout << "4. Update Number of Traffic Lights\n";
                cout << "5. Increase Salaries (by % for N employees)\n";
                cout << "6. Update Number of Employees\n";
                cout << "7. Upgrade Department Level\n";
                cout << "8. Exit\n";
                cout << "=====================================================\n";
                cout << "Enter your option (1-8): ";
        
                int option;
                cin >> option;
        
                switch(option) {
                    case 1: {
                        int new_electric;
                        cin >> new_electric;
                        int increase = new_electric - no_of_electricvehicles;
                        float cost = increase * 10000;
        
                        if (increase <= 0 || status.Total_Resources >= cost) {
                            no_of_electricvehicles = new_electric;
                            if (increase > 0) {
                                status.Total_Resources -= cost;
                                status.clean_energy += 0.005 * increase;
                                status.sustainable_living += 0.002 * increase;
                                cout << "✅ Electric vehicles increased. Rs. " << cost << " spent.\n";
                            }
                        } else {
                            cout << "❌ Not enough resources.\n";
                        }
                        break;
                    }
        
                    case 2: {
                        int new_petrol;
                        cin >> new_petrol;
                        int increase = new_petrol - no_of_petrolvehicles;
                        float cost = increase * 7000;
        
                        if (increase <= 0 || status.Total_Resources >= cost) {
                            no_of_petrolvehicles = new_petrol;
                            if (increase > 0) {
                                status.Total_Resources -= cost;
                                cout << "✅ Petrol vehicles increased. Rs. " << cost << " spent.\n";
                            }
                        } else {
                            cout << "❌ Not enough resources.\n";
                        }
                        break;
                    }
        
                    case 3: {
                        int new_diesel;
                        cin >> new_diesel;
                        int increase = new_diesel - no_of_dieselvehicles;
                        float cost = increase * 8000;
        
                        if (increase <= 0 || status.Total_Resources >= cost) {
                            no_of_dieselvehicles = new_diesel;
                            if (increase > 0) {
                                status.Total_Resources -= cost;
                                cout << "✅ Diesel vehicles increased. Rs. " << cost << " spent.\n";
                            }
                        } else {
                            cout << "❌ Not enough resources.\n";
                        }
                        break;
                    }
        
                    case 4: {
                        int new_lights;
                        cin >> new_lights;
                        int increase = new_lights - trafficlights;
                        float cost = increase * 2000;
        
                        if (increase <= 0 || status.Total_Resources >= cost) {
                            trafficlights = new_lights;
                            if (increase > 0) {
                                status.Total_Resources -= cost;
                                status.satisfaction_level += 0.001 * increase;
                                cout << "✅ Traffic lights increased. Rs. " << cost << " spent.\n";
                            }
                        } else {
                            cout << "❌ Not enough resources.\n";
                        }
                        break;
                    }
        
                    case 5: {
                        int num_employees;
                        double percent;
                        cin >> num_employees;
        
                        if (num_employees > employees) {
                            cout << "❌ Error: Number exceeds total employees.\n";
                            break;
                        }
        
                        cin >> percent;
                        double individual_salary = (employees > 0) ? salaries / employees : 0;
                        double increment_per_person = individual_salary * percent / 100.0;
                        double total_increment = increment_per_person * num_employees;
        
                        if (status.Total_Resources >= total_increment) {
                            salaries += total_increment;
                            status.Total_Resources -= total_increment;
                            status.satisfaction_level += 0.002 * num_employees;
                            cout << "✅ Salaries increased. Rs. " << total_increment << " spent.\n";
                        } else {
                            cout << "❌ Not enough resources.\n";
                        }
                        break;
                    }
        
                    case 6: {
                        int new_employees;
                        cin >> new_employees;
                        int increase = new_employees - employees;
                        float cost = increase * 4000;
        
                        if (increase <= 0 || status.Total_Resources >= cost) {
                            employees = new_employees;
                            if (increase > 0) {
                                status.Total_Resources -= cost;
                                status.satisfaction_level += 0.001 * increase;
                                cout << "✅ Employees increased. Rs. " << cost << " spent.\n";
                            }
                            if (employees > 0)
                                status.minimum_salaries = salaries / employees;
                        } else {
                            cout << "❌ Not enough resources.\n";
                        }
                        break;
                    }
        
                    case 7: {
                        int new_level;
                        cin >> new_level;
                        int increase = new_level - level;
                        float cost = increase * 15000;
        
                        if (increase > 0 && status.Total_Resources >= cost) {
                            level = new_level;
                            status.Total_Resources -= cost;
                            status.satisfaction_level += 0.002 * increase;
                            status.clean_energy += 0.01 * increase;
                            cout << "✅ Level upgraded. Rs. " << cost << " spent.\n";
                        } else if (increase <= 0) {
                            level = new_level;
                            cout << "Department downgraded or same.\n";
                        } else {
                            cout << "❌ Not enough resources.\n";
                        }
                        break;
                    }
        
                    case 8:
                        cout << "Exiting update menu...\n";
                        return;
        
                    default:
                        cout << "Invalid input.\n";
                        return;
                }
        
                status.satisfaction_level = max(0.0f, min(1.0f, status.satisfaction_level));
                status.sustainable_living = max(0.0f, min(1.0f, status.sustainable_living));
                status.clean_energy = max(0.0f, min(1.0f, status.clean_energy));
        
                beauty();
                cout << "✅ Update completed successfully!\n";
                beauty();
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
		    void update(Overall_Status &status) {
                beauty();
                cout << "\n========= Construction Department Update Menu =========\n";
                cout << "1. Update Number of Residential Buildings\n";
                cout << "2. Update Number of Industrial Buildings\n";
                cout << "3. Update Number of Roads\n";
                cout << "4. Update Number of Parks\n";
                cout << "5. Update Salaries (by % for N employees)\n";
                cout << "6. Update Number of Employees\n";
                cout << "7. Upgrade Department Level\n";
                cout << "8. Exit\n";
                cout << "=========================================================\n";
                cout << "Enter your option (1-8): ";
            
                int option;
                cin >> option;
            
                switch(option) {
                    case 1: {
                        int new_residential;
                        cin >> new_residential;
                        int increase = new_residential - no_of_resedentialbuildings;
                        float cost = increase * 5000; // Cost per building
            
                        if (increase <= 0 || status.Total_Resources >= cost) {
                            no_of_resedentialbuildings = new_residential;
                            if (increase > 0) {
                                status.Total_Resources -= cost;
                                cout << "✅ Residential buildings increased. Rs. " << cost << " spent.\n";
                            }
                        } else {
                            cout << "❌ Not enough resources.\n";
                        }
                        break;
                    }
            
                    case 2: {
                        int new_industrial;
                        cin >> new_industrial;
                        int increase = new_industrial - no_of_industrialbuildings;
                        float cost = increase * 10000; // Cost per building
            
                        if (increase <= 0 || status.Total_Resources >= cost) {
                            no_of_industrialbuildings = new_industrial;
                            if (increase > 0) {
                                status.Total_Resources -= cost;
                                cout << "✅ Industrial buildings increased. Rs. " << cost << " spent.\n";
                            }
                        } else {
                            cout << "❌ Not enough resources.\n";
                        }
                        break;
                    }
            
                    case 3: {
                        int new_roads;
                        cin >> new_roads;
                        int increase = new_roads - no_of_roads;
                        float cost = increase * 2000; // Cost per road
            
                        if (increase <= 0 || status.Total_Resources >= cost) {
                            no_of_roads = new_roads;
                            if (increase > 0) {
                                status.Total_Resources -= cost;
                                cout << "✅ Roads increased. Rs. " << cost << " spent.\n";
                            }
                        } else {
                            cout << "❌ Not enough resources.\n";
                        }
                        break;
                    }
            
                    case 4: {
                        int new_parks;
                        cin >> new_parks;
                        int increase = new_parks - no_of_parks;
                        float cost = increase * 1500; // Cost per park
            
                        if (increase <= 0 || status.Total_Resources >= cost) {
                            no_of_parks = new_parks;
                            if (increase > 0) {
                                status.Total_Resources -= cost;
                                cout << "✅ Parks increased. Rs. " << cost << " spent.\n";
                            }
                        } else {
                            cout << "❌ Not enough resources.\n";
                        }
                        break;
                    }
            
                    case 5: {
                        int num_employees;
                        double percent;
                        cin >> num_employees;
            
                        if (num_employees > employees) {
                            cout << "❌ Error: Number exceeds total employees.\n";
                            break;
                        }
            
                        cin >> percent;
                        double individual_salary = (employees > 0) ? salaries / employees : 0;
                        double increment_per_person = individual_salary * percent / 100.0;
                        double total_increment = increment_per_person * num_employees;
            
                        if (status.Total_Resources >= total_increment) {
                            salaries += total_increment;
                            status.Total_Resources -= total_increment;
                            cout << "✅ Salaries increased. Rs. " << total_increment << " spent.\n";
                        } else {
                            cout << "❌ Not enough resources.\n";
                        }
                        break;
                    }
            
                    case 6: {
                        int new_employees;
                        cin >> new_employees;
                        int increase = new_employees - employees;
                        float cost = increase * 4000; // Cost per employee
            
                        if (increase <= 0 || status.Total_Resources >= cost) {
                            employees = new_employees;
                            if (increase > 0) {
                                status.Total_Resources -= cost;
                                cout << "✅ Employees increased. Rs. " << cost << " spent.\n";
                            }
                        } else {
                            cout << "❌ Not enough resources.\n";
                        }
                        break;
                    }
            
                    case 7: {
                        int new_level;
                        cin >> new_level;
                        int increase = new_level - level;
                        float cost = increase * 10000; // Cost per level upgrade
            
                        if (increase > 0 && status.Total_Resources >= cost) {
                            level = new_level;
                            status.Total_Resources -= cost;
                            cout << "✅ Level upgraded. Rs. " << cost << " spent.\n";
                        } else if (increase <= 0) {
                            level = new_level;
                            cout << "Department downgraded or same.\n";
                        } else {
                            cout << "❌ Not enough resources.\n";
                        }
                        break;
                    }
            
                    case 8:
                        cout << "Exiting update menu...\n";
                        return;
            
                    default:
                        cout << "Invalid input.\n";
                        return;
                }
            
                status.satisfaction_level = max(0.0f, min(1.0f, status.satisfaction_level));
                beauty();
                cout << "✅ Update completed successfully!\n";
                beauty();
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
			void update(Overall_Status &status) {
                beauty();
                cout << "\n               What do you want to update in Police Department?\n";
                cout << "1. Update Number of Stations\n";
                cout << "2. Update Salaries\n";
                cout << "3. Update Number of Employees\n";
                cout << "4. Update Department Level\n";
                cout << "5. Exit\n";
                beauty();
            
                int option;
                cout << "Enter your option (1-5): ";
                cin >> option;
            
                switch(option) {
                    case 1: {
                        int new_stations;
                        cout << "Enter the new number of stations: ";
                        cin >> new_stations;
                        int increase = new_stations - no_of_stations;
                        float cost = increase * 5000; // Cost per station
            
                        if (increase <= 0 || status.Total_Resources >= cost) {
                            no_of_stations = new_stations;
                            if (increase > 0) {
                                status.Total_Resources -= cost;
                                cout << "✅ Number of stations updated. Rs. " << cost << " spent.\n";
                            }
                        } else {
                            cout << "❌ Not enough resources.\n";
                        }
                        break;
                    }
            
                    case 2: {
                        float new_salaries;
                        cout << "Enter the new salaries: ";
                        cin >> new_salaries;
            
                        if (status.Total_Resources >= new_salaries - salaries) {
                            salaries = new_salaries;
                            status.Total_Resources -= new_salaries - salaries;
                            cout << "✅ Salaries updated. Rs. " << (new_salaries - salaries) << " spent.\n";
                        } else {
                            cout << "❌ Not enough resources.\n";
                        }
                        break;
                    }
            
                    case 3: {
                        int new_employees;
                        cout << "Enter the new number of employees: ";
                        cin >> new_employees;
                        int increase = new_employees - employees;
                        float cost = increase * 3000; // Cost per employee
            
                        if (increase <= 0 || status.Total_Resources >= cost) {
                            employees = new_employees;
                            if (increase > 0) {
                                status.Total_Resources -= cost;
                                cout << "✅ Number of employees updated. Rs. " << cost << " spent.\n";
                            }
                        } else {
                            cout << "❌ Not enough resources.\n";
                        }
                        break;
                    }
            
                    case 4: {
                        int new_level;
                        cout << "Enter the new department level: ";
                        cin >> new_level;
                        int increase = new_level - level;
                        float cost = increase * 10000; // Cost per level upgrade
            
                        if (increase > 0 && status.Total_Resources >= cost) {
                            level = new_level;
                            status.Total_Resources -= cost;
                            cout << "✅ Department level updated. Rs. " << cost << " spent.\n";
                        } else if (increase <= 0) {
                            level = new_level;
                            cout << "Department level downgraded or remained the same.\n";
                        } else {
                            cout << "❌ Not enough resources.\n";
                        }
                        break;
                    }
            
                    case 5:
                        cout << "Exiting update menu...\n";
                        return;
            
                    default:
                        cout << "Invalid input.\n";
                        return;
                }
            
                
                status.satisfaction_level = max(0.0f, min(1.0f, status.satisfaction_level));
            
                beauty();
                cout << "✅ Update completed successfully!\n";
                beauty();
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
			
			void update(Overall_Status &status) {
                beauty();
                cout << "\n                   What do you want to update in Maintenance department?\n";
                cout << "1. Update Pending Requests\n";
                cout << "2. Update Completed Tasks\n";
                cout << "3. Update Salaries\n";
                cout << "4. Update Number of Employees\n";
                cout << "5. Update Department Level\n";
                cout << "6. Exit\n";
                beauty();
            
                int option;
                cout << "Enter your option (1-6): ";
                cin >> option;
            
                switch(option) {
                    case 1: {
                        int new_pending_requests;
                        cout << "Enter the new number of pending requests: ";
                        cin >> new_pending_requests;
            
                        pending_requests = new_pending_requests;
                        cout << "✅ Pending requests updated.\n";
                        break;
                    }
            
                    case 2: {
                        int new_completed_tasks;
                        cout << "Enter the new number of completed tasks: ";
                        cin >> new_completed_tasks;
            
                        completed_tasks = new_completed_tasks;
                        cout << "✅ Completed tasks updated.\n";
                        break;
                    }
            
                    case 3: {
                        float new_salaries;
                        cout << "Enter the new salaries: ";
                        cin >> new_salaries;
            
                        if (status.Total_Resources >= new_salaries - salaries) {
                            salaries = new_salaries;
                            status.Total_Resources -= new_salaries - salaries;
                            cout << "✅ Salaries updated. Rs. " << (new_salaries - salaries) << " spent.\n";
                        } else {
                            cout << "❌ Not enough resources.\n";
                        }
                        break;
                    }
            
                    case 4: {
                        int new_employees;
                        cout << "Enter the new number of employees: ";
                        cin >> new_employees;
                        int increase = new_employees - employees;
                        float cost = increase * 3000; // Cost per employee
            
                        if (increase <= 0 || status.Total_Resources >= cost) {
                            employees = new_employees;
                            if (increase > 0) {
                                status.Total_Resources -= cost;
                                cout << "✅ Number of employees updated. Rs. " << cost << " spent.\n";
                            }
                        } else {
                            cout << "❌ Not enough resources.\n";
                        }
                        break;
                    }
            
                    case 5: {
                        int new_level;
                        cout << "Enter the new department level: ";
                        cin >> new_level;
                        int increase = new_level - level;
                        float cost = increase * 10000; // Cost per level upgrade
            
                        if (increase > 0 && status.Total_Resources >= cost) {
                            level = new_level;
                            status.Total_Resources -= cost;
                            cout << "✅ Department level updated. Rs. " << cost << " spent.\n";
                        } else if (increase <= 0) {
                            level = new_level;
                            cout << "Department level downgraded or remained the same.\n";
                        } else {
                            cout << "❌ Not enough resources.\n";
                        }
                        break;
                    }
            
                    case 6:
                        cout << "Exiting update menu...\n";
                        return;
            
                    default:
                        cout << "Invalid input.\n";
                        return;
                }
            
                
                status.satisfaction_level = max(0.0f, min(1.0f, status.satisfaction_level));
            
                beauty();
                cout << "✅ Update completed successfully!\n";
                beauty();
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
			
            void update(Overall_Status &status) {
                beauty();
                cout << "\n               What do you want to update in Environmental department?\n";
                cout << "1. Update Number of Parks\n";
                cout << "2. Update Renewable Resources\n";
                cout << "3. Update Salaries\n";
                cout << "4. Update Number of Employees\n";
                cout << "5. Update Department Level\n";
                cout << "6. Exit\n";
                beauty();
                cout << "Enter your option (1-6): ";
                
                int option;
                cin >> option;
                
                switch (option) {
                    case 1: {
                        int new_parks;
                        cout << "Enter the new number of parks: ";
                        cin >> new_parks;
                        no_of_parks = new_parks;
                        cout << "✅ Number of parks updated.\n";
                        break;
                    }
            
                    case 2: {
                        float new_renewable_resources;
                        cout << "Enter the new renewable resources: ";
                        cin >> new_renewable_resources;
                        renewableresources = new_renewable_resources;
                        cout << "✅ Renewable resources updated.\n";
                        break;
                    }
            
                    case 3: {
                        float new_salaries;
                        cout << "Enter the new salaries: ";
                        cin >> new_salaries;
            
                        if (status.Total_Resources >= new_salaries - salaries) {
                            salaries = new_salaries;
                            status.Total_Resources -= new_salaries - salaries;
                            cout << "✅ Salaries updated. Rs. " << (new_salaries - salaries) << " spent.\n";
                        } else {
                            cout << "❌ Not enough resources.\n";
                        }
                        break;
                    }
            
                    case 4: {
                        int new_employees;
                        cout << "Enter the new number of employees: ";
                        cin >> new_employees;
                        int increase = new_employees - employees;
                        float cost = increase * 3000; // Cost per employee
            
                        if (increase <= 0 || status.Total_Resources >= cost) {
                            employees = new_employees;
                            if (increase > 0) {
                                status.Total_Resources -= cost;
                                cout << "✅ Number of employees updated. Rs. " << cost << " spent.\n";
                            }
                        } else {
                            cout << "❌ Not enough resources.\n";
                        }
                        break;
                    }
            
                    case 5: {
                        int new_level;
                        cout << "Enter the new department level: ";
                        cin >> new_level;
                        int increase = new_level - level;
                        float cost = increase * 10000; // Cost per level upgrade
            
                        if (increase > 0 && status.Total_Resources >= cost) {
                            level = new_level;
                            status.Total_Resources -= cost;
                            cout << "✅ Department level updated. Rs. " << cost << " spent.\n";
                        } else if (increase <= 0) {
                            level = new_level;
                            cout << "Department level downgraded or remained the same.\n";
                        } else {
                            cout << "❌ Not enough resources.\n";
                        }
                        break;
                    }
            
                    case 6:
                        cout << "Exiting update menu...\n";
                        return;
            
                    default:
                        cout << "Invalid input.\n";
                        return;
                }
            
                
                status.satisfaction_level = max(0.0f, min(1.0f, status.satisfaction_level));
                
                beauty();
                cout << "✅ Update completed successfully!\n";
                beauty();
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
		
		void update(Overall_Status &status) {
            beauty();
            cout << "\n                   What do you want to update in Resource Management department?\n";
            cout << "1. Update Number of Water Reservoirs\n";
            cout << "2. Update Number of Power Plants\n";
            cout << "3. Update Salaries\n";
            cout << "4. Update Number of Employees\n";
            cout << "5. Update Department Level\n";
            cout << "6. Exit\n";
            beauty();
            cout << "Enter your option (1-6): ";
            
            int option;
            cin >> option;
            
            switch (option) {
                case 1: {
                    int new_water_reserviors;
                    cout << "Enter the new number of water reservoirs: ";
                    cin >> new_water_reserviors;
                    water_reserviors = new_water_reserviors;
                    cout << "✅ Water reservoirs updated.\n";
                    break;
                }
        
                case 2: {
                    int new_power_plant;
                    cout << "Enter the new number of power plants: ";
                    cin >> new_power_plant;
                    power_plant = new_power_plant;
                    cout << "✅ Power plants updated.\n";
                    break;
                }
        
                case 3: {
                    float new_salaries;
                    cout << "Enter the new salaries: ";
                    cin >> new_salaries;
        
                    if (status.Total_Resources >= new_salaries - salaries) {
                        salaries = new_salaries;
                        status.Total_Resources -= new_salaries - salaries;
                        cout << "✅ Salaries updated. Rs. " << (new_salaries - salaries) << " spent.\n";
                    } else {
                        cout << "❌ Not enough resources.\n";
                    }
                    break;
                }
        
                case 4: {
                    int new_employees;
                    cout << "Enter the new number of employees: ";
                    cin >> new_employees;
                    int increase = new_employees - employees;
                    float cost = increase * 3000; // Cost per employee
        
                    if (increase <= 0 || status.Total_Resources >= cost) {
                        employees = new_employees;
                        if (increase > 0) {
                            status.Total_Resources -= cost;
                            cout << "✅ Number of employees updated. Rs. " << cost << " spent.\n";
                        }
                    } else {
                        cout << "❌ Not enough resources.\n";
                    }
                    break;
                }
        
                case 5: {
                    int new_level;
                    cout << "Enter the new department level: ";
                    cin >> new_level;
                    int increase = new_level - level;
                    float cost = increase * 10000; // Cost per level upgrade
        
                    if (increase > 0 && status.Total_Resources >= cost) {
                        level = new_level;
                        status.Total_Resources -= cost;
                        cout << "✅ Department level updated. Rs. " << cost << " spent.\n";
                    } else if (increase <= 0) {
                        level = new_level;
                        cout << "Department level downgraded or remained the same.\n";
                    } else {
                        cout << "❌ Not enough resources.\n";
                    }
                    break;
                }
        
                case 6:
                    cout << "Exiting update menu...\n";
                    return;
        
                default:
                    cout << "Invalid input.\n";
                    return;
            }
        
            
            status.satisfaction_level = max(0.0f, min(1.0f, status.satisfaction_level));
            
            beauty();
            cout << "✅ Update completed successfully!\n";
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
                    Overall_Status city(0.0,0.0,100000.0,0,0,0.0,0.0,0.0);
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
    Username=user_data[0];
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
