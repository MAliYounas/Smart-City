#include <iostream>
#include <fstream>
#include <string>
#include <cmath>
#include <iomanip>
#include <ctime>
#include <array>
#include <chrono>
#include <Windows.h>
#include<vector>
#include<algorithm>
using namespace std;
string filepath1 = "initial"; // For login
string filepath2 = "initial"; // For Overall status
string Username = "initial";
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
cout << "                                            🎉-----------------------------------------------------------------------🎉" << endl
     << endl;
cout << "                                                                       🔐 Login (Enter: L)" << endl
     << endl;
cout << "                                                                🆕 Open new account (Enter: O)" << endl
     << endl;
cout << "                                                                         ❌ Exit (Enter: E)" << endl
     << endl;
cout << "                                         👉 Enter what you want to choose: ";
cin >> option_exter;
cout << endl
     << endl;
cout << "                                            🎉-----------------------------------------------------------------------🎉" << endl
     << endl;


    if (option_exter != 'L' && option_exter != 'O' && option_exter != 'E')
    {
        cout << "\nInvalid input try again <3" << endl;
        goto ask;
    }
    return option_exter;
}
array<string, 2> login()
{
    string username;
    string password;
    string line;
    string user_data[2];

ask:
    int user_name_position = 0;
    int count = 0;

    beauty();
    cout << "🔐 ENTER YOUR USERNAME: ";
    cin >> username;
    beauty();
    cout << endl;

    cin.ignore();
    cout << "🔐 ENTER YOUR PASSWORD: ";
    cin >> password;
    beauty();
    cout << endl;

    fstream passw;
    passw.open("passwords_username.txt", ios::in);
    while (getline(passw, line))
    {
        if (username == line)
        {
            count++;
            goto checked_username;
        }
        user_name_position++;
    }

checked_username:
    passw.close();
    passw.open("passwords_username.txt", ios::in);
    int password_check = 0;
    while (getline(passw, line))
    {
        if (password == line)
        {
            if (password_check == (user_name_position + 1))
            {
                count++;
            }
        }
        password_check++;
    }
    passw.close();

    if (count < 2)
    {
        cout << "\n❌ Invalid credentials. Please try again.\n\n";
        goto ask;
    }

    if (count == 2)
    {
        cout << "\n✅ Login successful! Welcome, " << username << "!\n\n";
        array<string, 2> user_data = {username, password};
        return user_data;
    }

    array<string, 2> just = {"sjwdb", "wdnjkqn"};  // fallback (should not be reached)
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
    cout << "👤 ENTER YOUR FULL NAME: ";
    cin.ignore();
    getline(cin, name);
    beauty();

    cout << "📛 NOTE: Username should be a single word (no spaces). If entered with spaces, only the first word will be used.\n";
    cout << "👉 ENTER YOUR USERNAME: ";
    cin >> username;
    beauty();

    cout << "🔐 NOTE: Password should be a single word (no spaces). If entered with spaces, only the first word will be used.\n";
    cout << "🔒 ENTER YOUR PASSWORD: ";
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
            cout << "\n❌ USERNAME ALREADY TAKEN. PLEASE TRY ANOTHER ONE.\n\n";
            goto ask;
        }
        if (check == password)
        {
            passw.close();
            cout << "\n❌ PASSWORD ALREADY TAKEN. PLEASE TRY ANOTHER ONE.\n\n";
            goto ask;
        }
    }
    passw.close();

    if (name.empty() || password.empty() || username.empty())
    {
        cout << "\n❗ INVALID DATA. ALL FIELDS ARE REQUIRED.\n\n";
        goto ask;
    }

    // Save user information
    fstream info;
    info.open("information.txt", ios::out | ios::app);
    info << name << endl;
    info.close();

    // Assign and save account number
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

    cout << "\n✅ YOUR ACCOUNT NUMBER IS: " << account_no << "\n";

    // Save username and password
    passw.open("passwords_username.txt", ios::out | ios::app);
    passw << username << endl;
    passw << password << endl;
    passw.close();

    cout << "\n🎉 THANK YOU FOR OPENING AN ACCOUNT! 💚\n";
    beauty();
}

// Forward Declaration
class Health_Department;
class Overall_Status
{
public:
    float satisfaction_level=0;
    float minimum_salaries=200;
    float Total_Resources=20000;
    int population=500;
    int green_levels=0;
    float sustainable_living=0;
    float clean_energy=0;

   

    void Display()
{
    beauty();
    cout << "\n🌍================= OVERALL STATUS =================🌍\n\n";
    cout << "💰 TOTAL RESOURCES     : $" << Total_Resources << "\n";
    cout << "😊 SATISFACTION LEVEL  : " << satisfaction_level * 100 << "%\n";
    cout << "💼 MINIMUM SALARY      : $" << minimum_salaries << "\n";
    cout << "👥 POPULATION          : " << population << "\n";
    cout << "🌿 GREEN LEVELS        : " << green_levels << "\n";
    cout << "🏡 SUSTAINABLE LIVING  : " << sustainable_living * 100 << "%\n";
    cout << "⚡ CLEAN ENERGY        : " << clean_energy * 100 << "%\n";
    cout << "\n🌍===================================================🌍\n";
    beauty();
}


    // Save state to file
    void save_to_file(const string &filename)
    {
        ofstream out_file(filename);
        if (out_file)
        {
            out_file << satisfaction_level << "\n"
                     << minimum_salaries << "\n"
                     << Total_Resources << "\n"
                     << population << "\n"
                     << green_levels << "\n"
                     << sustainable_living << "\n"
                     << clean_energy;
        }
    }

    // Load state from file
    void load_from_file(const string &filename)
    {
        ifstream in_file(filename);
        if (in_file)
        {
            string line;
            getline(in_file, line);
            satisfaction_level = stof(line);
            getline(in_file, line);
            minimum_salaries = stof(line);
            getline(in_file, line);
            Total_Resources = stof(line);
            getline(in_file, line);
            population = stoi(line);
            getline(in_file, line);
            green_levels = stoi(line);
            getline(in_file, line);
            sustainable_living = stof(line);
            getline(in_file, line);
            clean_energy = stof(line);
        }
    }

    friend class Health_Department;
};

class Health_Department
{
private:
    int doctors;
    int nurses;
    int no_of_beds;
    string filename;

protected:
    int level;
    int employees;
    double salaries;

public:
    // Constructor with file loading
    Health_Department(string username) : filename(username + "_health.dat")
    {
        ifstream file(filename);
        if (file.good())
        {
            load_from_file();
        }
        else
        {
            // Default initialization
            level = 1;
            doctors = 5;
            nurses = 10;
            no_of_beds = 20;
            employees = 15;
            salaries = 50000;
            save_to_file();
        }
    }

    // Display current department status
    void Display()
    {
        beauty();
        cout << "\n🏥 HEALTH DEPARTMENT STATUS\n";
        cout << "├─ Department Level: " << level << "\n";
        cout << "├─ Number of Doctors: " << doctors << "\n";
        cout << "├─ Number of Nurses: " << nurses << "\n";
        cout << "├─ Available Beds: " << no_of_beds << "\n";
        cout << "├─ Total Employees: " << employees << "\n";
        cout << "└─ Monthly Salary Budget: $" << fixed << setprecision(2) << salaries << "\n";
        beauty();
    }

    // Save state to file
    void save_to_file()
    {
        ofstream file(filename);
        file << level << "\n"
             << doctors << "\n"
             << nurses << "\n"
             << no_of_beds << "\n"
             << employees << "\n"
             << salaries;
    }

    // Load state from file
    void load_from_file()
    {
        ifstream file(filename);
        string line;

        getline(file, line);
        level = stoi(line);
        getline(file, line);
        doctors = stoi(line);
        getline(file, line);
        nurses = stoi(line);
        getline(file, line);
        no_of_beds = stoi(line);
        getline(file, line);
        employees = stoi(line);
        getline(file, line);
        salaries = stod(line);
    }

    void update(Overall_Status &status)
    {
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

        switch (option)
        {
        case 1:
            handle_doctors(status);
            break;
        case 2:
            handle_nurses(status);
            break;
        case 3:
            handle_beds(status);
            break;
        case 4:
            handle_salaries(status);
            break;
        case 5:
            handle_employees(status);
            break;
        case 6:
            handle_upgrade(status);
            break;
        case 7:
            cout << "Exiting...\n";
            return;
        default:
            cout << "Invalid option!\n";
        }

        clamp_values(status);
        save_to_file();
        status.save_to_file(filename);

        beauty();
        cout << "✅ Update completed successfully!\n";
        beauty();
    }

private:
    void handle_doctors(Overall_Status &status)
    {
        cout << "👨‍⚕️ Current doctors: " << doctors << "\n";
        cout << "🔢 Enter new total number of doctors: ";
        int new_doctors;
        cin >> new_doctors;
        int increase = new_doctors - doctors;

        if (increase > 0)
        {
            float cost = increase * 5000;
            cout << "💰 Hiring cost: $" << cost << "\n";
            cout << "Proceed? (y/n): ";
            char confirm;
            cin >> confirm;
            if ((confirm == 'y' || confirm == 'Y') && status.Total_Resources >= cost)
            {
                doctors = new_doctors;
                status.Total_Resources -= cost;
                status.satisfaction_level += 0.001f * increase;
                status.population += increase * 100;
                status.green_levels -= increase;
                cout << "✅ Hired " << increase << " doctor(s).\n";
            }
            else if (confirm == 'y')
            {
                cout << "❌ Insufficient funds!\n";
            }
            else
            {
                cout << "ℹ️ Operation cancelled.\n";
            }
        }
        else
        {
            doctors = new_doctors;
            cout << "ℹ️ Set doctors to " << new_doctors << ".\n";
        }
    }

    void handle_nurses(Overall_Status &status)
    {
        cout << "👩‍⚕️ Current nurses: " << nurses << "\n";
        cout << "🔢 Enter new total number of nurses: ";
        int new_nurses;
        cin >> new_nurses;
        int increase = new_nurses - nurses;

        if (increase > 0)
        {
            float cost = increase * 3000;
            cout << "💰 Hiring cost: $" << cost << "\n";
            cout << "Proceed? (y/n): ";
            char confirm;
            cin >> confirm;
            if ((confirm == 'y' || confirm == 'Y') && status.Total_Resources >= cost)
            {
                nurses = new_nurses;
                status.Total_Resources -= cost;
                status.satisfaction_level += 0.0008f * increase;
                status.population += increase * 50;
                status.green_levels -= increase;
                cout << "✅ Hired " << increase << " nurse(s).\n";
            }
            else if (confirm == 'y')
            {
                cout << "❌ Insufficient funds!\n";
            }
            else
            {
                cout << "ℹ️ Operation cancelled.\n";
            }
        }
        else
        {
            nurses = new_nurses;
            cout << "ℹ️ Set nurses to " << new_nurses << ".\n";
        }
    }

    void handle_beds(Overall_Status &status)
    {
        cout << "🛏️ Current beds: " << no_of_beds << "\n";
        cout << "🔢 Enter new total number of hospital beds: ";
        int new_beds;
        cin >> new_beds;
        int increase = new_beds - no_of_beds;

        if (increase > 0)
        {
            float cost = increase * 2000;
            cout << "💰 Addition cost: $" << cost << "\n";
            cout << "Proceed? (y/n): ";
            char confirm;
            cin >> confirm;
            if ((confirm == 'y' || confirm == 'Y') && status.Total_Resources >= cost)
            {
                no_of_beds = new_beds;
                status.Total_Resources -= cost;
                status.satisfaction_level += 0.0005f * increase;
                status.population += increase * 10;
                status.green_levels -= increase;
                cout << "✅ Added " << increase << " bed(s).\n";
            }
            else if (confirm == 'y')
            {
                cout << "❌ Insufficient funds!\n";
            }
            else
            {
                cout << "ℹ️ Operation cancelled.\n";
            }
        }
        else
        {
            no_of_beds = new_beds;
            cout << "ℹ️ Set beds to " << new_beds << ".\n";
        }
    }

    void handle_salaries(Overall_Status &status)
    {
        cout << "💼 Current total salaries: $" << salaries << "\n";
        cout << "🔢 Enter number of employees to raise: ";
        int num_employees;
        cin >> num_employees;
        cout << "📈 Enter raise percentage: ";
        double percent;
        cin >> percent;
        if (num_employees > employees)
        {
            cout << "❌ Exceeds employee count!\n";
            return;
        }
        double increment = (salaries / employees) * (percent / 100) * num_employees;
        cout << "💰 Raise cost: $" << increment << "\nProceed? (y/n): ";
        char confirm;
        cin >> confirm;
        if ((confirm == 'y' || confirm == 'Y') && status.Total_Resources >= increment)
        {
            salaries += increment;
            status.Total_Resources -= increment;
            status.satisfaction_level += 0.002f * num_employees;
            status.minimum_salaries = salaries / employees;
            cout << "✅ Salaries updated.\n";
        }
        else if (confirm == 'y')
        {
            cout << "❌ Insufficient funds!\n";
        }
        else
        {
            cout << "ℹ️ Operation cancelled.\n";
        }
    }

    void handle_employees(Overall_Status &status)
    {
        cout << "👷 Current employees: " << employees << "\n";
        cout << "🔢 Enter new total employees: ";
        int new_employees;
        cin >> new_employees;
        int increase = new_employees - employees;
        float cost = increase * 4000;

        if (increase > 0)
        {
            cout << "💰 Hiring cost: $" << cost << "\nProceed? (y/n): ";
            char confirm;
            cin >> confirm;
            if ((confirm == 'y' || confirm == 'Y') && status.Total_Resources >= cost)
            {
                employees = new_employees;
                status.Total_Resources -= cost;
                status.satisfaction_level += 0.001f * increase;
                status.population += increase * 20;
                status.green_levels -= increase;
                cout << "✅ Hired " << increase << " employee(s).\n";
            }
            else if (confirm == 'y')
            {
                cout << "❌ Insufficient funds!\n";
            }
            else
            {
                cout << "ℹ️ Operation cancelled.\n";
            }
        }
        else
        {
            employees = new_employees;
            cout << "ℹ️ Set employees to " << new_employees << ".\n";
        }
        status.minimum_salaries = salaries / max(employees, 1);
    }

    void handle_upgrade(Overall_Status &status)
    {
        cout << "🏗️ Current level: " << level << "\n";
        cout << "🔢 Enter new upgrade level: ";
        int new_level;
        cin >> new_level;
        int increase = new_level - level;
        float cost = increase * 10000;

        if (increase > 0)
        {
            cout << "💰 Upgrade cost: $" << cost << "\nProceed? (y/n): ";
            char confirm;
            cin >> confirm;
            if ((confirm == 'y' || confirm == 'Y') && status.Total_Resources >= cost)
            {
                level = new_level;
                status.Total_Resources -= cost;
                status.satisfaction_level += 0.002f * increase;
                status.sustainable_living += 0.01f * increase;
                status.clean_energy += 0.01f * increase;
                status.population += increase * 200;
                status.green_levels += increase * 5;
                cout << "✅ Upgraded to level " << new_level << ".\n";
            }
            else if (confirm == 'y')
            {
                cout << "❌ Insufficient funds!\n";
            }
            else
            {
                cout << "ℹ️ Operation cancelled.\n";
            }
        }
        else
        {
            level = new_level;
            cout << "ℹ️ Set level to " << new_level << ".\n";
        }
    }

    void clamp_values(Overall_Status &status)
    {
        status.satisfaction_level = clamp(status.satisfaction_level, 0.0f, 1.0f);
        status.sustainable_living = clamp(status.sustainable_living, 0.0f, 1.0f);
        status.clean_energy = clamp(status.clean_energy, 0.0f, 1.0f);
    }

    template <typename T>
    T clamp(T value, T min, T max)
    {
        return std::max(min, std::min(value, max));
    }
};
class Educational_Department : public Health_Department
{
private:
    int students;
    int teachers;
    int no_of_classrooms;
    string filename;

public:
    Educational_Department(string username)
        : Health_Department(username), filename(username + "_education.dat")
    {
        ifstream file(filename);
        if (file.good())
        {
            load_from_file();
        }
        else
        {
            // Default initialization
            students = 100;
            teachers = 10;
            no_of_classrooms = 20;
            level = 1;
            employees = 15;
            salaries = 40000;
            save_to_file();
        }
    }

    void Display()
    {
        beauty();
        cout << "\n📚 EDUCATIONAL DEPARTMENT STATUS\n";
        cout << "├─ Department Level: " << level << "\n";
        cout << "├─ Number of Students: " << students << "\n";
        cout << "├─ Number of Teachers: " << teachers << "\n";
        cout << "├─ Classrooms Available: " << no_of_classrooms << "\n";
        cout << "├─ Total Employees: " << employees << "\n";
        cout << "└─ Monthly Salary Budget: $" << fixed << setprecision(2) << salaries << "\n";
        beauty();
    }

    void save_to_file()
    {
        ofstream file(filename);
        file << level << "\n"
             << employees << "\n"
             << salaries << "\n"
             << students << "\n"
             << teachers << "\n"
             << no_of_classrooms;
    }

    void load_from_file()
    {
        ifstream file(filename);
        string line;

        getline(file, line);
        level = stoi(line);
        getline(file, line);
        employees = stoi(line);
        getline(file, line);
        salaries = stod(line);
        getline(file, line);
        students = stoi(line);
        getline(file, line);
        teachers = stoi(line);
        getline(file, line);
        no_of_classrooms = stoi(line);
    }

    void update(Overall_Status &status)
    {
        beauty();
        cout << "\n========= Educational Department Update Menu =========\n";
        cout << "1. Update Number of Students\n";
        cout << "2. Update Number of Teachers\n";
        cout << "3. Update Number of Classrooms\n";
        cout << "4. Increase Salaries\n";
        cout << "5. Update Staff Count\n";
        cout << "6. Upgrade Department\n";
        cout << "7. Exit\n";
        cout << "======================================================\n";
        cout << "Enter your option (1-7): ";

        int option;
        cin >> option;

        switch (option)
        {
        case 1:
            handle_students(status);
            break;
        case 2:
            handle_teachers(status);
            break;
        case 3:
            handle_classrooms(status);
            break;
        case 4:
            handle_salaries(status);
            break;
        case 5:
            handle_staff(status);
            break;
        case 6:
            handle_upgrade(status);
            break;
        case 7:
            cout << "Exiting...\n";
            return;
        default:
            cout << "Invalid option!\n";
        }

        clamp_values(status);
        save_to_file();
        status.save_to_file(filename);

        beauty();
        cout << "✅ Update completed successfully!\n";
        beauty();
    }

private:
    void handle_students(Overall_Status &status)
    {
        cout << "👩‍🎓 Current students: " << students << "\n";
        cout << "🔢 Enter new total students: ";
        int new_students;
        cin >> new_students;
        int increase = new_students - students;

        if (increase > 0)
        {
            float cost = increase * 1000;
            cout << "💰 Cost to add " << increase << " students: " << cost << "\n";
            cout << "Proceed? (y/n): ";
            char confirm;
            cin >> confirm;
            if ((confirm == 'y' || confirm == 'Y') && status.Total_Resources >= cost)
            {
                students = new_students;
                status.Total_Resources -= cost;
                status.satisfaction_level += 0.0005f * increase;
                status.population += increase * 50;
                status.green_levels -= increase * 2;
                cout << "✅ Added " << increase << " students.\n";
            }
            else if (confirm == 'y')
            {
                cout << "❌ Insufficient funds!\n";
            }
            else
            {
                cout << "ℹ️ Operation cancelled.\n";
            }
        }
        else
        {
            students = new_students;
            cout << "ℹ️ Student count set to " << new_students << ".\n";
        }
    }

    void handle_teachers(Overall_Status &status)
    {
        cout << "👨‍🏫 Current teachers: " << teachers << "\n";
        cout << "🔢 Enter new total teachers: ";
        int new_teachers;
        cin >> new_teachers;
        int increase = new_teachers - teachers;

        if (increase > 0)
        {
            float cost = increase * 6000;
            cout << "💰 Cost to hire " << increase << " teachers: " << cost << "\n";
            cout << "Proceed? (y/n): ";
            char confirm;
            cin >> confirm;
            if ((confirm == 'y' || confirm == 'Y') && status.Total_Resources >= cost)
            {
                teachers = new_teachers;
                status.Total_Resources -= cost;
                status.satisfaction_level += 0.001f * increase;
                status.population += increase * 30;
                status.green_levels -= increase;
                cout << "✅ Hired " << increase << " teachers.\n";
            }
            else if (confirm == 'y')
            {
                cout << "❌ Insufficient funds!\n";
            }
            else
            {
                cout << "ℹ️ Operation cancelled.\n";
            }
        }
        else
        {
            teachers = new_teachers;
            cout << "ℹ️ Teacher count set to " << new_teachers << ".\n";
        }
    }

    void handle_classrooms(Overall_Status &status)
    {
        cout << "🏫 Current classrooms: " << no_of_classrooms << "\n";
        cout << "🔢 Enter new total classrooms: ";
        int new_rooms;
        cin >> new_rooms;
        int increase = new_rooms - no_of_classrooms;

        if (increase > 0)
        {
            float cost = increase * 8000;
            cout << "💰 Cost to add " << increase << " classrooms: " << cost << "\n";
            cout << "Proceed? (y/n): ";
            char confirm;
            cin >> confirm;
            if ((confirm == 'y' || confirm == 'Y') && status.Total_Resources >= cost)
            {
                no_of_classrooms = new_rooms;
                status.Total_Resources -= cost;
                status.satisfaction_level += 0.001f * increase;
                status.population += increase * 20;
                status.green_levels -= increase * 2;
                cout << "✅ Added " << increase << " classrooms.\n";
            }
            else if (confirm == 'y')
            {
                cout << "❌ Insufficient funds!\n";
            }
            else
            {
                cout << "ℹ️ Operation cancelled.\n";
            }
        }
        else
        {
            no_of_classrooms = new_rooms;
            cout << "ℹ️ Classroom count set to " << new_rooms << ".\n";
        }
    }

    void handle_salaries(Overall_Status &status)
    {
        cout << "💼 Current average salary: " << (employees ? salaries / employees : 0) << "\n";
        cout << "🔢 Enter number of employees for raise: ";
        int num_employees;
        cin >> num_employees;
        cout << "📈 Enter raise percentage: ";
        double percent;
        cin >> percent;

        if (num_employees > employees)
        {
            cout << "❌ Cannot exceed total employees!\n";
            return;
        }
        double increment = (salaries / employees) * (percent / 100) * num_employees;
        cout << "💰 Total raise cost: " << increment << "\n";
        cout << "Proceed? (y/n): ";
        char confirm;
        cin >> confirm;
        if ((confirm == 'y' || confirm == 'Y') && status.Total_Resources >= increment)
        {
            salaries += increment;
            status.Total_Resources -= increment;
            status.satisfaction_level += 0.002f * num_employees;
            status.minimum_salaries = salaries / employees;
            cout << "✅ Salaries increased for " << num_employees << " employees.\n";
        }
        else if (confirm == 'y')
        {
            cout << "❌ Insufficient funds!\n";
        }
        else
        {
            cout << "ℹ️ Operation cancelled.\n";
        }
    }

    void handle_staff(Overall_Status &status)
    {
        cout << "👥 Current staff count: " << employees << "\n";
        cout << "🔢 Enter new total staff: ";
        int new_employees;
        cin >> new_employees;
        int increase = new_employees - employees;
        float cost = increase * 4000;

        if (increase > 0)
        {
            cout << "💰 Cost to hire " << increase << " staff: " << cost << "\n";
            cout << "Proceed? (y/n): ";
            char confirm;
            cin >> confirm;
            if ((confirm == 'y' || confirm == 'Y') && status.Total_Resources >= cost)
            {
                employees = new_employees;
                status.Total_Resources -= cost;
                status.satisfaction_level += 0.001f * increase;
                status.population += increase * 10;
                status.green_levels -= increase;
                cout << "✅ Hired " << increase << " staff.\n";
            }
            else if (confirm == 'y')
            {
                cout << "❌ Insufficient funds!\n";
            }
            else
            {
                cout << "ℹ️ Operation cancelled.\n";
            }
        }
        else
        {
            employees = new_employees;
            cout << "ℹ️ Staff count set to " << new_employees << ".\n";
        }
        status.minimum_salaries = salaries / max(employees, 1);
    }

    void handle_upgrade(Overall_Status &status)
    {
        cout << "🏗️ Current level: " << level << "\n";
        cout << "🔢 Enter new upgrade level: ";
        int new_level;
        cin >> new_level;
        int increase = new_level - level;
        float cost = increase * 12000;

        if (increase > 0)
        {
            cout << "💰 Upgrade cost: " << cost << "\n";
            cout << "Proceed? (y/n): ";
            char confirm;
            cin >> confirm;
            if ((confirm == 'y' || confirm == 'Y') && status.Total_Resources >= cost)
            {
                level = new_level;
                status.Total_Resources -= cost;
                status.satisfaction_level += 0.002f * increase;
                status.sustainable_living += 0.01f * increase;
                status.clean_energy += 0.005f * increase;
                status.population += increase * 100;
                status.green_levels += increase * 3;
                cout << "✅ Upgraded to level " << new_level << ".\n";
            }
            else if (confirm == 'y')
            {
                cout << "❌ Insufficient funds!\n";
            }
            else
            {
                cout << "ℹ️ Operation cancelled.\n";
            }
        }
        else
        {
            level = new_level;
            cout << "ℹ️ Level set to " << new_level << ".\n";
        }
    }

    void clamp_values(Overall_Status &status)
    {
        status.satisfaction_level = clamp(status.satisfaction_level, 0.0f, 1.0f);
        status.sustainable_living = clamp(status.sustainable_living, 0.0f, 1.0f);
        status.clean_energy = clamp(status.clean_energy, 0.0f, 1.0f);
        status.population = max(status.population, 0);
        status.green_levels = max(status.green_levels, 0);
    }

    template <typename T>
    T clamp(T value, T min, T max)
    {
        return std::max(min, std::min(value, max));
    }
};
class FinanceDepartment : public Health_Department
{
private:
    float base_income;
    std::chrono::system_clock::time_point last_update;
    string filename;

    float calculate_current_income()
    {
        return base_income * level * (1 + 0.15f * level);
    }

    float calculate_upgrade_cost()
    {
        return 80000.0f * pow(1.5f, level);
    }

    void clamp_values(Overall_Status &status)
    {
        status.satisfaction_level = clamp(status.satisfaction_level, 0.0f, 1.0f);
        status.sustainable_living = clamp(status.sustainable_living, 0.0f, 1.0f);
    }

public:
    FinanceDepartment(string username)
        : Health_Department(username), filename(username + "_finance.dat")
    {
        ifstream file(filename);
        if (file.good())
        {
            load_from_file();
        }
        else
        {
            // Default initialization
            base_income = 100.0f;
            level = 1;
            employees = 15;
            salaries = 50000;
            last_update = std::chrono::system_clock::now();
            save_to_file();
        }
    }

    void Display()
    {
        beauty();
        cout << "\n💰 FINANCE DEPARTMENT STATUS\n";
        cout << "├─ Department Level: " << level << "\n";
        cout << "├─ Base Income Rate: $" << fixed << setprecision(2) << calculate_current_income() << "/sec\n";
        cout << "├─ Employees: " << employees << "\n";
        cout << "└─ Salary Budget: $" << salaries << "\n";
        beauty();
    }

    void save_to_file()
    {
        ofstream file(filename);
        file << level << "\n"
             << employees << "\n"
             << salaries << "\n"
             << base_income << "\n"
             << std::chrono::system_clock::to_time_t(last_update);
    }

    void load_from_file()
    {
        ifstream file(filename);
        string line;

        getline(file, line);
        level = stoi(line);
        getline(file, line);
        employees = stoi(line);
        getline(file, line);
        salaries = stod(line);
        getline(file, line);
        base_income = stof(line);
        getline(file, line);
        time_t timestamp = stoll(line);
        last_update = std::chrono::system_clock::from_time_t(timestamp);
    }

    void update(Overall_Status &status)
    {
        // Calculate passive income since last update
        auto now = std::chrono::system_clock::now();
        std::chrono::duration<double> elapsed = now - last_update;
        status.Total_Resources += elapsed.count() * calculate_current_income();
        last_update = now;

        beauty();
        cout << "Income Per Second Updated.You Can Exit If You Dont Want Any Changes." << endl;
        cout << "\n========= FINANCE DEPARTMENT UPDATE =========\n";
        cout << "1. Upgrade Department (+15% income)\n";
        cout << "2. Adjust Staff Count\n";
        cout << "3. Modify Salaries\n";
        cout << "4. Exit\n";
        cout << "Enter choice (1-4): ";

        int option;
        cin >> option;

        switch (option)
        {
        case 1:
            handle_upgrade(status);
            break;
        case 2:
            handle_staff(status);
            break;
        case 3:
            handle_salaries(status);
            break;
        case 4:
            cout << "Exiting...\n";
            break;
        default:
            cout << "Invalid option!\n";
        }

        clamp_values(status);
        save_to_file();
        status.save_to_file(filename);
    }

private:
    void handle_upgrade(Overall_Status &status)
    {
        cout << "🏗️ Current level: " << level << "\n";
        float cost = calculate_upgrade_cost();
        cout << "💰 Upgrade cost to level " << (level + 1) << ": " << cost << "\n";
        cout << "Proceed with upgrade? (y/n): ";
        char confirm;
        cin >> confirm;
        if ((confirm == 'y' || confirm == 'Y'))
        {
            if (status.Total_Resources >= cost)
            {
                status.Total_Resources -= cost;
                level++;
                status.satisfaction_level += 0.005f;
                status.sustainable_living += 0.01f;
                cout << "✅ Upgraded to level " << level << "!\n";
            }
            else
            {
                cout << "❌ Need $" << (cost - status.Total_Resources) << " more to upgrade!\n";
            }
        }
        else
        {
            cout << "ℹ️ Upgrade cancelled.\n";
        }
    }

    void handle_staff(Overall_Status &status)
    {
        cout << "👥 Current staff: " << employees << "\n";
        cout << "🔢 Enter new employee count: ";
        int new_count;
        cin >> new_count;
        int difference = new_count - employees;
        if (difference > 0)
        {
            float cost = difference * 8000;
            cout << "💰 Cost to hire " << difference << " staff: " << cost << "\n";
            cout << "Proceed with hiring? (y/n): ";
            char confirm;
            cin >> confirm;
            if ((confirm == 'y' || confirm == 'Y'))
            {
                if (status.Total_Resources >= cost)
                {
                    employees = new_count;
                    status.Total_Resources -= cost;
                    status.satisfaction_level += 0.001f * difference;
                    cout << "✅ Hired " << difference << " new staff.\n";
                }
                else
                {
                    cout << "❌ Insufficient funds for hiring!\n";
                }
            }
            else
            {
                cout << "ℹ️ Hiring cancelled.\n";
            }
        }
        else
        {
            employees = new_count;
            status.satisfaction_level -= 0.002f;
            cout << "ℹ️ Staff count reduced to " << new_count << ". Satisfaction decreased.\n";
        }
    }

    void handle_salaries(Overall_Status &status)
    {
        cout << "💼 Current total salaries: " << salaries << "\n";
        cout << "🔢 Enter new salary budget: ";
        double new_salaries;
        cin >> new_salaries;
        double difference = new_salaries - salaries;
        if (difference > 0)
        {
            cout << "💰 Additional funds needed for raises: " << difference << "\n";
            cout << "Proceed with salary increase? (y/n): ";
            char confirm;
            cin >> confirm;
            if ((confirm == 'y' || confirm == 'Y'))
            {
                if (status.Total_Resources >= difference)
                {
                    salaries = new_salaries;
                    status.Total_Resources -= difference;
                    status.satisfaction_level += 0.005f;
                    cout << "✅ Salary budget increased to " << new_salaries << ".Satisfaction increased.\n";
                }
                else
                {
                    cout << "❌ Insufficient funds for raises!\n";
                }
            }
            else
            {
                cout << "ℹ️ Salary update cancelled.\n";
            }
        }
        else
        {
            salaries = new_salaries;
            status.satisfaction_level -= 0.01f;
            cout << "ℹ️ Salary budget decreased to " << new_salaries << ". Satisfaction decreased.\n";
        }
    }

    template <typename T>
    T clamp(T value, T min, T max)
    {
        return std::max(min, std::min(value, max));
    }
};
class Transport_Department : public Health_Department
{
private:
    int no_of_electricvehicles;
    int no_of_petrolvehicles;
    int no_of_dieselvehicles;
    int trafficlights;
    string filename;

    void clamp_values(Overall_Status &status)
    {
        status.satisfaction_level = clamp(status.satisfaction_level, 0.0f, 1.0f);
        status.sustainable_living = clamp(status.sustainable_living, 0.0f, 1.0f);
        status.clean_energy = clamp(status.clean_energy, 0.0f, 1.0f);
        status.green_levels = max(status.green_levels, 0);
    }

public:
    Transport_Department(string username)
        : Health_Department(username), filename(username + "_transport.dat")
    {
        ifstream file(filename);
        if (file.good())
        {
            load_from_file();
        }
        else
        {
            // Default initialization
            no_of_electricvehicles = 5;
            no_of_petrolvehicles = 20;
            no_of_dieselvehicles = 15;
            trafficlights = 50;
            level = 1;
            employees = 25;
            salaries = 60000;
            save_to_file();
        }
    }

    void Display()
    {
        beauty();
        cout << "\n🚦 TRANSPORT DEPARTMENT STATUS\n";
        cout << "├─ Department Level: " << level << "\n";
        cout << "├─ Electric Vehicles: " << no_of_electricvehicles << "\n";
        cout << "├─ Petrol Vehicles: " << no_of_petrolvehicles << "\n";
        cout << "├─ Diesel Vehicles: " << no_of_dieselvehicles << "\n";
        cout << "├─ Traffic Lights: " << trafficlights << "\n";
        cout << "├─ Maintenance Staff: " << employees << "\n";
        cout << "└─ Salary Budget: $" << fixed << setprecision(2) << salaries << "\n";
        beauty();
    }

    void save_to_file()
    {
        ofstream file(filename);
        file << level << "\n"
             << employees << "\n"
             << salaries << "\n"
             << no_of_electricvehicles << "\n"
             << no_of_petrolvehicles << "\n"
             << no_of_dieselvehicles << "\n"
             << trafficlights;
    }

    void load_from_file()
    {
        ifstream file(filename);
        string line;

        getline(file, line);
        level = stoi(line);
        getline(file, line);
        employees = stoi(line);
        getline(file, line);
        salaries = stod(line);
        getline(file, line);
        no_of_electricvehicles = stoi(line);
        getline(file, line);
        no_of_petrolvehicles = stoi(line);
        getline(file, line);
        no_of_dieselvehicles = stoi(line);
        getline(file, line);
        trafficlights = stoi(line);
    }

    void update(Overall_Status &status)
    {
        beauty();
        cout << "\n========= TRANSPORT DEPARTMENT UPDATE =========\n";
        cout << "1. Update Electric Vehicles\n";
        cout << "2. Update Petrol Vehicles\n";
        cout << "3. Update Diesel Vehicles\n";
        cout << "4. Update Traffic Lights\n";
        cout << "5. Adjust Salaries\n";
        cout << "6. Modify Staff Count\n";
        cout << "7. Upgrade Department\n";
        cout << "8. Exit\n";
        cout << "================================================\n";
        cout << "Enter your option (1-8): ";

        int option;
        cin >> option;

        switch (option)
        {
        case 1:
            handle_electric_vehicles(status);
            break;
        case 2:
            handle_petrol_vehicles(status);
            break;
        case 3:
            handle_diesel_vehicles(status);
            break;
        case 4:
            handle_traffic_lights(status);
            break;
        case 5:
            handle_salaries(status);
            break;
        case 6:
            handle_staff(status);
            break;
        case 7:
            handle_upgrade(status);
            break;
        case 8:
            cout << "Exiting...\n";
            return;
        default:
            cout << "Invalid option!\n";
        }

        clamp_values(status);
        save_to_file();
        status.save_to_file(filename);

        beauty();
        cout << "✅ Update completed successfully!\n";
        beauty();
    }

private:
    void handle_electric_vehicles(Overall_Status &status)
    {
        cout << "🔌 Current electric vehicles: " << no_of_electricvehicles << "\n";
        cout << "🔢 Enter new total electric vehicles: ";
        int new_count;
        cin >> new_count;
        int increase = new_count - no_of_electricvehicles;

        if (increase > 0)
        {
            float cost = increase * 10000;
            cout << "💰 Cost to add " << increase << " EV(s): $" << cost << "\n";
            cout << "Proceed? (y/n): ";
            char confirm;
            cin >> confirm;
            if ((confirm == 'y' || confirm == 'Y') && status.Total_Resources >= cost)
            {
                no_of_electricvehicles = new_count;
                status.Total_Resources -= cost;
                status.clean_energy += 0.005f * increase;
                status.sustainable_living += 0.002f * increase;
                status.population += increase * 80;
                status.green_levels += increase * 2;
                cout << "✅ Added " << increase << " EV(s).\n";
            }
            else if (confirm == 'y')
            {
                cout << "❌ Need $" << (cost - status.Total_Resources) << " more\n";
            }
            else
            {
                cout << "ℹ️ Operation cancelled.\n";
            }
        }
        else
        {
            no_of_electricvehicles = new_count;
            cout << "ℹ️ EV count set to " << new_count << ".\n";
        }
    }

    void handle_petrol_vehicles(Overall_Status &status)
    {
        cout << "⛽ Current petrol vehicles: " << no_of_petrolvehicles << "\n";
        cout << "🔢 Enter new total petrol vehicles: ";
        int new_count;
        cin >> new_count;
        int increase = new_count - no_of_petrolvehicles;

        if (increase > 0)
        {
            float cost = increase * 7000;
            cout << "💰 Cost to add " << increase << " petrol vehicle(s): $" << cost << "\n";
            cout << "Proceed? (y/n): ";
            char confirm;
            cin >> confirm;
            if ((confirm == 'y' || confirm == 'Y') && status.Total_Resources >= cost)
            {
                no_of_petrolvehicles = new_count;
                status.Total_Resources -= cost;
                status.population += increase * 40;
                status.green_levels -= increase * 3;
                status.clean_energy -= 0.003f * increase;
                status.sustainable_living -= 0.001f * increase;
                cout << "✅ Added " << increase << " petrol vehicle(s).\n";
            }
            else if (confirm == 'y')
            {
                cout << "❌ Need $" << (cost - status.Total_Resources) << " more\n";
            }
            else
            {
                cout << "ℹ️ Operation cancelled.\n";
            }
        }
        else
        {
            no_of_petrolvehicles = new_count;
            cout << "ℹ️ Petrol vehicle count set to " << new_count << ".\n";
        }
    }

    void handle_diesel_vehicles(Overall_Status &status)
    {
        cout << "🚛 Current diesel vehicles: " << no_of_dieselvehicles << "\n";
        cout << "🔢 Enter new total diesel vehicles: ";
        int new_count;
        cin >> new_count;
        int increase = new_count - no_of_dieselvehicles;

        if (increase > 0)
        {
            float cost = increase * 8000;
            cout << "💰 Cost to add " << increase << " diesel vehicle(s): $" << cost << "\n";
            cout << "Proceed? (y/n): ";
            char confirm;
            cin >> confirm;
            if ((confirm == 'y' || confirm == 'Y') && status.Total_Resources >= cost)
            {
                no_of_dieselvehicles = new_count;
                status.Total_Resources -= cost;
                status.population += increase * 30;
                status.green_levels -= increase * 5;
                status.clean_energy -= 0.005f * increase;
                status.sustainable_living -= 0.002f * increase;
                cout << "✅ Added " << increase << " diesel vehicle(s).\n";
            }
            else if (confirm == 'y')
            {
                cout << "❌ Need $" << (cost - status.Total_Resources) << " more\n";
            }
            else
            {
                cout << "ℹ️ Operation cancelled.\n";
            }
        }
        else
        {
            no_of_dieselvehicles = new_count;
            cout << "ℹ️ Diesel vehicle count set to " << new_count << ".\n";
        }
    }

    void handle_traffic_lights(Overall_Status &status)
    {
        cout << "🚦 Current traffic lights: " << trafficlights << "\n";
        cout << "🔢 Enter new total traffic lights: ";
        int new_count;
        cin >> new_count;
        int increase = new_count - trafficlights;

        if (increase > 0)
        {
            float cost = increase * 2000;
            cout << "💰 Cost to add " << increase << " light(s): $" << cost << "\n";
            cout << "Proceed? (y/n): ";
            char confirm;
            cin >> confirm;
            if ((confirm == 'y' || confirm == 'Y') && status.Total_Resources >= cost)
            {
                trafficlights = new_count;
                status.Total_Resources -= cost;
                status.satisfaction_level += 0.001f * increase;
                status.population += increase * 20;
                status.green_levels -= increase;
                cout << "✅ Added " << increase << " traffic light(s).\n";
            }
            else if (confirm == 'y')
            {
                cout << "❌ Need $" << (cost - status.Total_Resources) << " more\n";
            }
            else
            {
                cout << "ℹ️ Operation cancelled.\n";
            }
        }
        else
        {
            trafficlights = new_count;
            cout << "ℹ️ Traffic light count set to " << new_count << ".\n";
        }
    }

    void handle_salaries(Overall_Status &status)
    {
        cout << "💼 Current total salaries: $" << salaries << "\n";
        cout << "🔢 Enter new salary budget: ";
        double new_salaries;
        cin >> new_salaries;
        double diff = new_salaries - salaries;

        if (diff > 0)
        {
            cout << "💰 Additional needed: $" << diff << "\n";
            cout << "Proceed? (y/n): ";
            char confirm;
            cin >> confirm;
            if ((confirm == 'y' || confirm == 'Y') && status.Total_Resources >= diff)
            {
                salaries = new_salaries;
                status.Total_Resources -= diff;
                status.satisfaction_level += 0.002f * (diff / (salaries / employees));
                status.minimum_salaries = salaries / employees;
                cout << "✅ Salary budget increased to $" << new_salaries << ".\n";
            }
            else if (confirm == 'y')
            {
                cout << "❌ Insufficient funds!\n";
            }
            else
            {
                cout << "ℹ️ Operation cancelled.\n";
            }
        }
        else
        {
            salaries = new_salaries;
            status.satisfaction_level -= 0.01f;
            status.minimum_salaries = salaries / max(employees, 1);
            cout << "ℹ️ Salary budget decreased to $" << new_salaries << ".\n";
        }
    }

    void handle_staff(Overall_Status &status)
    {
        cout << "👥 Current staff: " << employees << "\n";
        cout << "🔢 Enter new total staff: ";
        int new_count;
        cin >> new_count;
        int increase = new_count - employees;

        if (increase > 0)
        {
            float cost = increase * 4000;
            cout << "💰 Cost to hire " << increase << " staff: $" << cost << "\n";
            cout << "Proceed? (y/n): ";
            char confirm;
            cin >> confirm;
            if ((confirm == 'y' || confirm == 'Y') && status.Total_Resources >= cost)
            {
                employees = new_count;
                status.Total_Resources -= cost;
                status.satisfaction_level += 0.001f * increase;
                status.population += increase * 15;
                status.green_levels -= increase * 2;
                cout << "✅ Hired " << increase << " staff.\n";
            }
            else if (confirm == 'y')
            {
                cout << "❌ Need $" << (cost - status.Total_Resources) << " more\n";
            }
            else
            {
                cout << "ℹ️ Operation cancelled.\n";
            }
        }
        else
        {
            employees = new_count;
            status.satisfaction_level -= 0.002f;
            cout << "ℹ️ Staff count set to " << new_count << ".\n";
        }
        status.minimum_salaries = salaries / max(employees, 1);
    }

    void handle_upgrade(Overall_Status &status)
    {
        cout << "🏗️ Current level: " << level << "\n";
        cout << "🔢 Enter new level: ";
        int new_level;
        cin >> new_level;
        int increase = new_level - level;

        if (increase > 0)
        {
            float cost = increase * 15000;
            cout << "💰 Cost to upgrade by " << increase << " level(s): $" << cost << "\n";
            cout << "Proceed? (y/n): ";
            char confirm;
            cin >> confirm;
            if ((confirm == 'y' || confirm == 'Y') && status.Total_Resources >= cost)
            {
                level = new_level;
                status.Total_Resources -= cost;
                status.satisfaction_level += 0.002f * increase;
                status.clean_energy += 0.01f * increase;
                status.population += increase * 150;
                status.green_levels += increase * 8;
                status.sustainable_living += 0.005f * increase;
                cout << "✅ Upgraded to level " << new_level << ".\n";
            }
            else if (confirm == 'y')
            {
                cout << "❌ Need $" << (cost - status.Total_Resources) << " more\n";
            }
            else
            {
                cout << "ℹ️ Operation cancelled.\n";
            }
        }
        else
        {
            level = new_level;
            cout << "ℹ️ Level set to " << new_level << ".\n";
        }
    }

    template <typename T>
    T clamp(T value, T min, T max)
    {
        return std::max(min, std::min(value, max));
    }
};
class Construction_Department : public Health_Department
{
private:
    int no_of_residentialbuildings;
    int no_of_industrialbuildings;
    int no_of_roads;
    int no_of_parks;
    string filename;

    void clamp_values(Overall_Status &status)
    {
        status.satisfaction_level = clamp(status.satisfaction_level, 0.0f, 1.0f);
        status.sustainable_living = clamp(status.sustainable_living, 0.0f, 1.0f);
        status.clean_energy = clamp(status.clean_energy, 0.0f, 1.0f);
        status.green_levels = max(status.green_levels, 0);
    }

public:
    Construction_Department(string username)
        : Health_Department(username), filename(username + "_construction.dat")
    {

        ifstream file(filename);
        if (file.good())
        {
            load_from_file();
        }
        else
        {
            // Default initialization
            no_of_residentialbuildings = 50;
            no_of_industrialbuildings = 10;
            no_of_roads = 20;
            no_of_parks = 5;
            level = 1;
            employees = 30;
            salaries = 75000;
            save_to_file();
        }
    }

    void Display()
    {
        beauty();
        cout << "\n🏗️ CONSTRUCTION DEPARTMENT STATUS\n";
        cout << "├─ Department Level: " << level << "\n";
        cout << "├─ Residential Buildings: " << no_of_residentialbuildings << "\n";
        cout << "├─ Industrial Buildings: " << no_of_industrialbuildings << "\n";
        cout << "├─ Road Networks: " << no_of_roads << "\n";
        cout << "├─ Public Parks: " << no_of_parks << "\n";
        cout << "├─ Construction Workers: " << employees << "\n";
        cout << "└─ Salary Budget: $" << fixed << setprecision(2) << salaries << "\n";
        beauty();
    }

    void save_to_file()
    {
        ofstream file(filename);
        file << level << "\n"
             << employees << "\n"
             << salaries << "\n"
             << no_of_residentialbuildings << "\n"
             << no_of_industrialbuildings << "\n"
             << no_of_roads << "\n"
             << no_of_parks;
    }

    void load_from_file()
    {
        ifstream file(filename);
        string line;

        getline(file, line);
        level = stoi(line);
        getline(file, line);
        employees = stoi(line);
        getline(file, line);
        salaries = stod(line);
        getline(file, line);
        no_of_residentialbuildings = stoi(line);
        getline(file, line);
        no_of_industrialbuildings = stoi(line);
        getline(file, line);
        no_of_roads = stoi(line);
        getline(file, line);
        no_of_parks = stoi(line);
    }

    void update(Overall_Status &status)
    {
        beauty();
        cout << "\n========= CONSTRUCTION DEPARTMENT UPDATE =========\n";
        cout << "1. Update Residential Buildings\n";
        cout << "2. Update Industrial Buildings\n";
        cout << "3. Update Road Networks\n";
        cout << "4. Update Public Parks\n";
        cout << "5. Adjust Salaries\n";
        cout << "6. Modify Workforce\n";
        cout << "7. Upgrade Department\n";
        cout << "8. Exit\n";
        cout << "==================================================\n";
        cout << "Enter your option (1-8): ";

        int option;
        cin >> option;

        switch (option)
        {
        case 1:
            handle_residential(status);
            break;
        case 2:
            handle_industrial(status);
            break;
        case 3:
            handle_roads(status);
            break;
        case 4:
            handle_parks(status);
            break;
        case 5:
            handle_salaries(status);
            break;
        case 6:
            handle_staff(status);
            break;
        case 7:
            handle_upgrade(status);
            break;
        case 8:
            cout << "Exiting...\n";
            return;
        default:
            cout << "Invalid option!\n";
        }

        clamp_values(status);
        save_to_file();
        status.save_to_file(filename);

        beauty();
        cout << "✅ Update completed successfully!\n";
        beauty();
    }

private:
    void handle_residential(Overall_Status &status)
    {
        cout << "🏠 Current residential buildings: " << no_of_residentialbuildings << "\n";
        cout << "🔢 Enter new total residential buildings: ";
        int new_count;
        cin >> new_count;
        int increase = new_count - no_of_residentialbuildings;

        if (increase > 0)
        {
            float cost = increase * 5000;
            cout << "💰 Cost to add " << increase << " building(s): $" << cost << "\n";
            cout << "Proceed? (y/n): ";
            char confirm;
            cin >> confirm;
            if ((confirm == 'y' || confirm == 'Y') && status.Total_Resources >= cost)
            {
                no_of_residentialbuildings = new_count;
                status.Total_Resources -= cost;
                status.population += increase * 200;
                status.green_levels -= increase * 3;
                status.sustainable_living += 0.001f * increase;
                status.satisfaction_level += 0.002f * increase;
                cout << "✅ Added " << increase << " residential building(s).\n";
            }
            else if (confirm == 'y')
            {
                cout << "❌ Need $" << (cost - status.Total_Resources) << " more\n";
            }
            else
            {
                cout << "ℹ️ Operation cancelled.\n";
            }
        }
        else
        {
            no_of_residentialbuildings = new_count;
            cout << "ℹ️ Residential buildings set to " << new_count << ".\n";
        }
    }

    void handle_industrial(Overall_Status &status)
    {
        cout << "🏭 Current industrial buildings: " << no_of_industrialbuildings << "\n";
        cout << "🔢 Enter new total industrial buildings: ";
        int new_count;
        cin >> new_count;
        int increase = new_count - no_of_industrialbuildings;

        if (increase > 0)
        {
            float cost = increase * 10000;
            cout << "💰 Cost to add " << increase << " building(s): $" << cost << "\n";
            cout << "Proceed? (y/n): ";
            char confirm;
            cin >> confirm;
            if ((confirm == 'y' || confirm == 'Y') && status.Total_Resources >= cost)
            {
                no_of_industrialbuildings = new_count;
                status.Total_Resources -= cost;
                status.population += increase * 50;
                status.green_levels -= increase * 5;
                status.clean_energy -= 0.003f * increase;
                status.sustainable_living -= 0.002f * increase;
                cout << "✅ Added " << increase << " industrial building(s).\n";
            }
            else if (confirm == 'y')
            {
                cout << "❌ Need $" << (cost - status.Total_Resources) << " more\n";
            }
            else
            {
                cout << "ℹ️ Operation cancelled.\n";
            }
        }
        else
        {
            no_of_industrialbuildings = new_count;
            cout << "ℹ️ Industrial buildings set to " << new_count << ".\n";
        }
    }

    void handle_roads(Overall_Status &status)
    {
        cout << "🛣️ Current roads: " << no_of_roads << "\n";
        cout << "🔢 Enter new total roads: ";
        int new_count;
        cin >> new_count;
        int increase = new_count - no_of_roads;

        if (increase > 0)
        {
            float cost = increase * 2000;
            cout << "💰 Cost to add " << increase << " road(s): $" << cost << "\n";
            cout << "Proceed? (y/n): ";
            char confirm;
            cin >> confirm;
            if ((confirm == 'y' || confirm == 'Y') && status.Total_Resources >= cost)
            {
                no_of_roads = new_count;
                status.Total_Resources -= cost;
                status.population += increase * 100;
                status.green_levels -= increase * 2;
                status.satisfaction_level += 0.0015f * increase;
                cout << "✅ Added " << increase << " road(s).\n";
            }
            else if (confirm == 'y')
            {
                cout << "❌ Need $" << (cost - status.Total_Resources) << " more\n";
            }
            else
            {
                cout << "ℹ️ Operation cancelled.\n";
            }
        }
        else
        {
            no_of_roads = new_count;
            cout << "ℹ️ Roads set to " << new_count << ".\n";
        }
    }

    void handle_parks(Overall_Status &status)
    {
        cout << "🌳 Current parks: " << no_of_parks << "\n";
        cout << "🔢 Enter new total parks: ";
        int new_count;
        cin >> new_count;
        int increase = new_count - no_of_parks;

        if (increase > 0)
        {
            float cost = increase * 1500;
            cout << "💰 Cost to add " << increase << " park(s): $" << cost << "\n";
            cout << "Proceed? (y/n): ";
            char confirm;
            cin >> confirm;
            if ((confirm == 'y' || confirm == 'Y') && status.Total_Resources >= cost)
            {
                no_of_parks = new_count;
                status.Total_Resources -= cost;
                status.green_levels += increase * 4;
                status.sustainable_living += 0.003f * increase;
                status.satisfaction_level += 0.003f * increase;
                status.population += increase * 30;
                cout << "✅ Added " << increase << " park(s).\n";
            }
            else if (confirm == 'y')
            {
                cout << "❌ Need $" << (cost - status.Total_Resources) << " more\n";
            }
            else
            {
                cout << "ℹ️ Operation cancelled.\n";
            }
        }
        else
        {
            no_of_parks = new_count;
            cout << "ℹ️ Parks set to " << new_count << ".\n";
        }
    }

    void handle_salaries(Overall_Status &status)
    {
        cout << "💼 Current total salaries: $" << salaries << "\n";
        cout << "🔢 Enter number of employees for raise and percentage: ";
        int num_employees;
        double percent;
        cin >> num_employees >> percent;
        if (num_employees > employees)
        {
            cout << "❌ Exceeds employee count!\n";
            return;
        }
        double increment = (salaries / employees) * (percent / 100) * num_employees;
        cout << "💰 Raise cost: $" << increment << "\nProceed? (y/n): ";
        char confirm;
        cin >> confirm;
        if ((confirm == 'y' || confirm == 'Y') && status.Total_Resources >= increment)
        {
            salaries += increment;
            status.Total_Resources -= increment;
            status.satisfaction_level += 0.002f * num_employees;
            status.minimum_salaries = salaries / employees;
            cout << "✅ Salaries updated.\n";
        }
        else if (confirm == 'y')
        {
            cout << "❌ Insufficient funds!\n";
        }
        else
        {
            cout << "ℹ️ Operation cancelled.\n";
        }
    }

    void handle_staff(Overall_Status &status)
    {
        cout << "👥 Current staff: " << employees << "\n";
        cout << "🔢 Enter new total staff: ";
        int new_count;
        cin >> new_count;
        int increase = new_count - employees;
        if (increase > 0)
        {
            float cost = increase * 4000;
            cout << "💰 Cost to hire " << increase << " staff: $" << cost << "\nProceed? (y/n): ";
            char confirm;
            cin >> confirm;
            if ((confirm == 'y' || confirm == 'Y') && status.Total_Resources >= cost)
            {
                employees = new_count;
                status.Total_Resources -= cost;
                status.population += increase * 20;
                status.green_levels -= increase * 1;
                status.satisfaction_level += 0.001f * increase;
                cout << "✅ Staff hired.\n";
            }
            else if (confirm == 'y')
            {
                cout << "❌ Need $" << (cost - status.Total_Resources) << " more\n";
            }
            else
            {
                cout << "ℹ️ Operation cancelled.\n";
            }
        }
        else
        {
            employees = new_count;
            cout << "ℹ️ Staff set to " << new_count << ".\n";
        }
        status.minimum_salaries = salaries / max(employees, 1);
    }

    void handle_upgrade(Overall_Status &status)
    {
        cout << "🏗️ Current level: " << level << "\n";
        cout << "🔢 Enter new level: ";
        int new_level;
        cin >> new_level;
        int increase = new_level - level;
        if (increase > 0)
        {
            float cost = increase * 10000;
            cout << "💰 Upgrade cost: $" << cost << "\nProceed? (y/n): ";
            char confirm;
            cin >> confirm;
            if ((confirm == 'y' || confirm == 'Y') && status.Total_Resources >= cost)
            {
                level = new_level;
                status.Total_Resources -= cost;
                status.sustainable_living += 0.01f * increase;
                status.green_levels += increase * 3;
                status.clean_energy += 0.005f * increase;
                status.population += increase * 300;
                status.satisfaction_level += 0.003f * increase;
                cout << "✅ Upgraded to level " << new_level << ".\n";
            }
            else if (confirm == 'y')
            {
                cout << "❌ Need $" << (cost - status.Total_Resources) << " more\n";
            }
            else
            {
                cout << "ℹ️ Operation cancelled.\n";
            }
        }
        else
        {
            level = new_level;
            cout << "ℹ️ Level set to " << new_level << ".\n";
        }
    }

    template <typename T>
    T clamp(T value, T min, T max)
    {
        return std::max(min, std::min(value, max));
    }
};
class Police_Department : public Health_Department
{
private:
    int no_of_stations;
    string filename;

    void clamp_values(Overall_Status &status)
    {
        status.satisfaction_level = clamp(status.satisfaction_level, 0.0f, 1.0f);
        status.sustainable_living = clamp(status.sustainable_living, 0.0f, 1.0f);
        status.clean_energy = clamp(status.clean_energy, 0.0f, 1.0f);
        status.green_levels = max(status.green_levels, 0);
    }

public:
    Police_Department(string username)
        : Health_Department(username), filename(username + "_police.dat")
    {
        ifstream file(filename);
        if (file.good())
        {
            load_from_file();
        }
        else
        {
            // Default initialization
            no_of_stations = 5;
            level = 1;
            employees = 50;
            salaries = 80000;
            save_to_file();
        }
    }

    void Display()
    {
        beauty();
        cout << "\n🚨 POLICE DEPARTMENT STATUS\n";
        cout << "├─ Department Level: " << level << "\n";
        cout << "├─ Police Stations: " << no_of_stations << "\n";
        cout << "├─ Officers: " << employees << "\n";
        cout << "└─ Salary Budget: $" << fixed << setprecision(2) << salaries << "\n";
        beauty();
    }

    void save_to_file()
    {
        ofstream file(filename);
        file << level << "\n"
             << employees << "\n"
             << salaries << "\n"
             << no_of_stations;
    }

    void load_from_file()
    {
        ifstream file(filename);
        string line;

        getline(file, line);
        level = stoi(line);
        getline(file, line);
        employees = stoi(line);
        getline(file, line);
        salaries = stod(line);
        getline(file, line);
        no_of_stations = stoi(line);
    }

    void update(Overall_Status &status)
    {
        beauty();
        cout << "\n========= POLICE DEPARTMENT UPDATE =========\n";
        cout << "1. Update Police Stations\n";
        cout << "2. Adjust Salaries\n";
        cout << "3. Modify Workforce\n";
        cout << "4. Upgrade Department\n";
        cout << "5. Exit\n";
        cout << "============================================\n";
        cout << "Enter your option (1-5): ";

        int option;
        cin >> option;

        switch (option)
        {
        case 1:
            handle_stations(status);
            break;
        case 2:
            handle_salaries(status);
            break;
        case 3:
            handle_staff(status);
            break;
        case 4:
            handle_upgrade(status);
            break;
        case 5:
            cout << "Exiting...\n";
            return;
        default:
            cout << "Invalid option!\n";
        }

        clamp_values(status);
        save_to_file();
        status.save_to_file(filename);

        beauty();
        cout << "✅ Update completed successfully!\n";
        beauty();
    }

private:
    void handle_stations(Overall_Status &status)
    {
        cout << "🚉 Current stations: " << no_of_stations << "\n";
        cout << "🔢 Enter new total stations: ";
        int new_count;
        cin >> new_count;
        int increase = new_count - no_of_stations;

        if (increase > 0)
        {
            float cost = increase * 5000;
            cout << "💰 Cost to add " << increase << " station(s): $" << cost << "\n";
            cout << "Proceed? (y/n): ";
            char confirm;
            cin >> confirm;
            if ((confirm == 'y' || confirm == 'Y') && status.Total_Resources >= cost)
            {
                no_of_stations = new_count;
                status.Total_Resources -= cost;
                status.satisfaction_level += 0.003f * increase;
                status.population += increase * 150;
                status.green_levels -= increase * 2;
                status.sustainable_living += 0.001f * increase;
                cout << "✅ Added " << increase << " station(s).\n";
            }
            else if (confirm == 'y')
            {
                cout << "❌ Need $" << (cost - status.Total_Resources) << " more\n";
            }
            else
            {
                cout << "ℹ️ Operation cancelled.\n";
            }
        }
        else
        {
            no_of_stations = new_count;
            cout << "ℹ️ Station count set to " << new_count << ".\n";
        }
    }

    void handle_salaries(Overall_Status &status)
    {
        cout << "💼 Current total salaries: $" << salaries << "\n";
        cout << "🔢 Enter new total salary budget: ";
        double new_salaries;
        cin >> new_salaries;
        double difference = new_salaries - salaries;

        if (difference > 0)
        {
            cout << "💰 Additional needed: $" << difference << "\n";
            cout << "Proceed with increase? (y/n): ";
            char confirm;
            cin >> confirm;
            if ((confirm == 'y' || confirm == 'Y') && status.Total_Resources >= difference)
            {
                salaries = new_salaries;
                status.Total_Resources -= difference;
                status.satisfaction_level += 0.002f * (difference / 1000);
                status.minimum_salaries = salaries / employees;
                cout << "✅ Salaries increased to $" << new_salaries << ".\n";
            }
            else if (confirm == 'y')
            {
                cout << "❌ Insufficient funds for salary increase!\n";
            }
            else
            {
                cout << "ℹ️ Operation cancelled.\n";
            }
        }
        else
        {
            salaries = new_salaries;
            status.satisfaction_level -= 0.01f;
            status.minimum_salaries = salaries / max(employees, 1);
            cout << "ℹ️ Salaries decreased to $" << new_salaries << ". Satisfaction decreased.\n";
        }
    }

    void handle_staff(Overall_Status &status)
    {
        cout << "👥 Current staff count: " << employees << "\n";
        cout << "🔢 Enter new total staff: ";
        int new_count;
        cin >> new_count;
        int increase = new_count - employees;

        if (increase > 0)
        {
            float cost = increase * 3000;
            cout << "💰 Cost to hire " << increase << " staff: $" << cost << "\n";
            cout << "Proceed? (y/n): ";
            char confirm;
            cin >> confirm;
            if ((confirm == 'y' || confirm == 'Y') && status.Total_Resources >= cost)
            {
                employees = new_count;
                status.Total_Resources -= cost;
                status.satisfaction_level += 0.0015f * increase;
                status.population += increase * 25;
                status.green_levels -= increase * 1;
                cout << "✅ Hired " << increase << " staff.\n";
            }
            else if (confirm == 'y')
            {
                cout << "❌ Need $" << (cost - status.Total_Resources) << " more\n";
            }
            else
            {
                cout << "ℹ️ Operation cancelled.\n";
            }
        }
        else
        {
            employees = new_count;
            cout << "ℹ️ Staff count set to " << new_count << ".\n";
        }
        status.minimum_salaries = salaries / max(employees, 1);
    }

    void handle_upgrade(Overall_Status &status)
    {
        cout << "🏗️ Current level: " << level << "\n";
        cout << "🔢 Enter new upgrade level: ";
        int new_level;
        cin >> new_level;
        int increase = new_level - level;

        if (increase > 0)
        {
            float cost = increase * 10000;
            cout << "💰 Cost to upgrade by " << increase << " level(s): $" << cost << "\n";
            cout << "Proceed? (y/n): ";
            char confirm;
            cin >> confirm;
            if ((confirm == 'y' || confirm == 'Y') && status.Total_Resources >= cost)
            {
                level = new_level;
                status.Total_Resources -= cost;
                status.satisfaction_level += 0.005f * increase;
                status.sustainable_living += 0.003f * increase;
                status.clean_energy += 0.002f * increase;
                status.green_levels += increase * 2;
                status.population += increase * 200;
                cout << "✅ Upgraded to level " << new_level << ".\n";
            }
            else if (confirm == 'y')
            {
                cout << "❌ Need $" << (cost - status.Total_Resources) << " more\n";
            }
            else
            {
                cout << "ℹ️ Operation cancelled.\n";
            }
        }
        else
        {
            level = new_level;
            cout << "ℹ️ Level set to " << new_level << ".\n";
        }
    }

    template <typename T>
    T clamp(T value, T min, T max)
    {
        return std::max(min, std::min(value, max));
    }
};
class Maintenance_Department : public Health_Department
{
private:
    int pending_requests;
    int completed_tasks;
    string filename;

    void clamp_values(Overall_Status &status)
    {
        status.satisfaction_level = clamp(status.satisfaction_level, 0.0f, 1.0f);
        status.sustainable_living = clamp(status.sustainable_living, 0.0f, 1.0f);
        status.clean_energy = clamp(status.clean_energy, 0.0f, 1.0f);
        status.green_levels = max(status.green_levels, 0);
    }

public:
    Maintenance_Department(string username)
        : Health_Department(username), filename(username + "_maintenance.dat")
    {
        ifstream file(filename);
        if (file.good())
        {
            load_from_file();
        }
        else
        {
            // Default initialization
            pending_requests = 20;
            completed_tasks = 50;
            level = 1;
            employees = 40;
            salaries = 65000;
            save_to_file();
        }
    }

    void Display()
    {
        beauty();
        cout << "\n🔧 MAINTENANCE DEPARTMENT STATUS\n";
        cout << "├─ Department Level: " << level << "\n";
        cout << "├─ Pending Requests: " << pending_requests << "\n";
        cout << "├─ Completed Tasks: " << completed_tasks << "\n";
        cout << "├─ Maintenance Crew: " << employees << "\n";
        cout << "└─ Salary Budget: $" << fixed << setprecision(2) << salaries << "\n";
        beauty();
    }

    void save_to_file()
    {
        ofstream file(filename);
        file << level << "\n"
             << employees << "\n"
             << salaries << "\n"
             << pending_requests << "\n"
             << completed_tasks;
    }

    void load_from_file()
    {
        ifstream file(filename);
        string line;

        getline(file, line);
        level = stoi(line);
        getline(file, line);
        employees = stoi(line);
        getline(file, line);
        salaries = stod(line);
        getline(file, line);
        pending_requests = stoi(line);
        getline(file, line);
        completed_tasks = stoi(line);
    }

    void update(Overall_Status &status)
    {
        beauty();
        cout << "\n========= MAINTENANCE DEPARTMENT UPDATE =========\n";
        cout << "1. Manage Pending Requests\n";
        cout << "2. Update Completed Tasks\n";
        cout << "3. Adjust Salaries\n";
        cout << "4. Modify Workforce\n";
        cout << "5. Upgrade Department\n";
        cout << "6. Exit\n";
        cout << "==================================================\n";
        cout << "Enter your option (1-6): ";

        int option;
        cin >> option;

        switch (option)
        {
        case 1:
            handle_requests(status);
            break;
        case 2:
            handle_tasks(status);
            break;
        case 3:
            handle_salaries(status);
            break;
        case 4:
            handle_staff(status);
            break;
        case 5:
            handle_upgrade(status);
            break;
        case 6:
            cout << "Exiting...\n";
            return;
        default:
            cout << "Invalid option!\n";
        }

        clamp_values(status);
        save_to_file();
        status.save_to_file(filename);

        beauty();
        cout << "✅ Update completed successfully!\n";
        beauty();
    }

private:
    void handle_requests(Overall_Status &status)
    {
        cout << "📨 Current pending requests: " << pending_requests << "\n";
        cout << "🔢 Enter new total pending requests: ";
        int new_count;
        cin >> new_count;
        int delta = new_count - pending_requests;

        pending_requests = new_count;
        if (delta > 0)
        {
            status.satisfaction_level -= 0.001f * delta;
            status.sustainable_living -= 0.0005f * delta;
            status.green_levels -= delta * 2;
            cout << "⚠️ " << delta << " new requests added; satisfaction decreased.\n";
        }
        else
        {
            status.satisfaction_level += 0.001f * abs(delta);
            status.sustainable_living += 0.0005f * abs(delta);
            cout << "✅ " << abs(delta) << " requests resolved; satisfaction increased.\n";
        }
    }

    void handle_tasks(Overall_Status &status)
    {
        cout << "📝 Current completed tasks: " << completed_tasks << "\n";
        cout << "🔢 Enter new total completed tasks: ";
        int new_count;
        cin >> new_count;
        int delta = new_count - completed_tasks;

        completed_tasks = new_count;
        if (delta > 0)
        {
            status.satisfaction_level += 0.002f * delta;
            status.green_levels += delta * 3;
            status.sustainable_living += 0.001f * delta;
            status.clean_energy += 0.0005f * delta;
            status.population += delta * 50;
            cout << "✅ " << delta << " tasks completed; satisfaction increased.\n";
        }
        else
        {
            cout << "ℹ️ No new tasks completed.\n";
        }
    }

    void handle_salaries(Overall_Status &status)
    {
        cout << "💼 Current total salaries: $" << salaries << "\n";
        cout << "🔢 Enter new total salary budget: ";
        double new_salaries;
        cin >> new_salaries;
        double diff = new_salaries - salaries;

        if (diff > 0)
        {
            cout << "💰 Additional needed: $" << diff << "\n";
            cout << "Proceed with salary increase? (y/n): ";
            char confirm;
            cin >> confirm;
            if ((confirm == 'y' || confirm == 'Y') && status.Total_Resources >= diff)
            {
                salaries = new_salaries;
                status.Total_Resources -= diff;
                status.satisfaction_level += 0.001f * (diff / 1000);
                status.minimum_salaries = salaries / employees;
                cout << "✅ Salaries increased to $" << new_salaries << ".\n";
            }
            else if (confirm == 'y')
            {
                cout << "❌ Insufficient funds!\n";
            }
            else
            {
                cout << "ℹ️ Operation cancelled.\n";
            }
        }
        else
        {
            salaries = new_salaries;
            status.satisfaction_level -= 0.002f * abs(diff / 1000);
            status.minimum_salaries = salaries / max(employees, 1);
            cout << "ℹ️ Salary budget decreased to $" << new_salaries << ".\n";
        }
    }

    void handle_staff(Overall_Status &status)
    {
        cout << "👥 Current staff: " << employees << "\n";
        cout << "🔢 Enter new total staff: ";
        int new_count;
        cin >> new_count;
        int increase = new_count - employees;

        if (increase > 0)
        {
            float cost = increase * 3000;
            cout << "💰 Cost to hire " << increase << " staff: $" << cost << "\n";
            cout << "Proceed with hiring? (y/n): ";
            char confirm;
            cin >> confirm;
            if ((confirm == 'y' || confirm == 'Y') && status.Total_Resources >= cost)
            {
                employees = new_count;
                status.Total_Resources -= cost;
                status.population += increase * 15;
                status.green_levels -= increase * 1;
                status.satisfaction_level += 0.0008f * increase;
                cout << "✅ Hired " << increase << " staff.\n";
            }
            else if (confirm == 'y')
            {
                cout << "❌ Need $" << (cost - status.Total_Resources) << " more\n";
            }
            else
            {
                cout << "ℹ️ Operation cancelled.\n";
            }
        }
        else
        {
            employees = new_count;
            cout << "ℹ️ Staff count set to " << new_count << ".\n";
        }
        status.minimum_salaries = salaries / max(employees, 1);
    }

    void handle_upgrade(Overall_Status &status)
    {
        cout << "🏗️ Current level: " << level << "\n";
        cout << "🔢 Enter new upgrade level: ";
        int new_level;
        cin >> new_level;
        int increase = new_level - level;

        if (increase > 0)
        {
            float cost = increase * 10000;
            cout << "💰 Cost to upgrade by " << increase << " level(s): $" << cost << "\n";
            cout << "Proceed with upgrade? (y/n): ";
            char confirm;
            cin >> confirm;
            if ((confirm == 'y' || confirm == 'Y') && status.Total_Resources >= cost)
            {
                level = new_level;
                status.Total_Resources -= cost;
                status.satisfaction_level += 0.003f * increase;
                status.sustainable_living += 0.002f * increase;
                status.clean_energy += 0.0015f * increase;
                status.green_levels += increase * 4;
                status.population += increase * 100;
                cout << "✅ Upgraded to level " << new_level << ".\n";
            }
            else if (confirm == 'y')
            {
                cout << "❌ Need $" << (cost - status.Total_Resources) << " more\n";
            }
            else
            {
                cout << "ℹ️ Operation cancelled.\n";
            }
        }
        else
        {
            level = new_level;
            cout << "ℹ️ Level set to " << new_level << ".\n";
        }
    }

    template <typename T>
    T clamp(T value, T min, T max)
    {
        return std::max(min, std::min(value, max));
    }
};
class Environmental_Department : public Health_Department
{
private:
    int no_of_parks;
    double renewable_resources;
    string filename;

    void clamp_values(Overall_Status &status)
    {
        status.satisfaction_level = clamp(status.satisfaction_level, 0.0f, 1.0f);
        status.sustainable_living = clamp(status.sustainable_living, 0.0f, 1.0f);
        status.clean_energy = clamp(status.clean_energy, 0.0f, 1.0f);
        status.green_levels = max(status.green_levels, 0);
    }

public:
    Environmental_Department(string username)
        : Health_Department(username), filename(username + "_environment.dat")
    {
        ifstream file(filename);
        if (file.good())
        {
            load_from_file();
        }
        else
        {
            // Default initialization
            no_of_parks = 8;
            renewable_resources = 5000.0;
            level = 1;
            employees = 25;
            salaries = 70000;
            save_to_file();
        }
    }

    void Display()
    {
        beauty();
        cout << "\n🌿 ENVIRONMENTAL DEPARTMENT STATUS\n";
        cout << "├─ Department Level: " << level << "\n";
        cout << "├─ Public Parks: " << no_of_parks << "\n";
        cout << "├─ Renewable Resources: " << fixed << setprecision(2) << renewable_resources << " MW\n";
        cout << "├─ Environmental Officers: " << employees << "\n";
        cout << "└─ Salary Budget: $" << salaries << "\n";
        beauty();
    }

    void save_to_file()
    {
        ofstream file(filename);
        file << level << "\n"
             << employees << "\n"
             << salaries << "\n"
             << no_of_parks << "\n"
             << renewable_resources;
    }

    void load_from_file()
    {
        ifstream file(filename);
        string line;

        getline(file, line);
        level = stoi(line);
        getline(file, line);
        employees = stoi(line);
        getline(file, line);
        salaries = stod(line);
        getline(file, line);
        no_of_parks = stoi(line);
        getline(file, line);
        renewable_resources = stod(line);
    }

    void update(Overall_Status &status)
    {
        beauty();
        cout << "\n========= ENVIRONMENTAL DEPARTMENT UPDATE =========\n";
        cout << "1. Manage Public Parks\n";
        cout << "2. Update Renewable Resources\n";
        cout << "3. Adjust Salaries\n";
        cout << "4. Modify Workforce\n";
        cout << "5. Upgrade Department\n";
        cout << "6. Exit\n";
        cout << "====================================================\n";
        cout << "Enter your option (1-6): ";

        int option;
        cin >> option;

        switch (option)
        {
        case 1:
            handle_parks(status);
            break;
        case 2:
            handle_resources(status);
            break;
        case 3:
            handle_salaries(status);
            break;
        case 4:
            handle_staff(status);
            break;
        case 5:
            handle_upgrade(status);
            break;
        case 6:
            cout << "Exiting...\n";
            return;
        default:
            cout << "Invalid option!\n";
        }

        clamp_values(status);
        save_to_file();
        status.save_to_file(filename);

        beauty();
        cout << "✅ Update completed successfully!\n";
        beauty();
    }

private:
    void handle_parks(Overall_Status &status)
    {
        cout << "🌳 Current parks: " << no_of_parks << "\n";
        cout << "🔢 Enter new total parks: ";
        int new_count;
        cin >> new_count;
        int increase = new_count - no_of_parks;

        if (increase > 0)
        {
            float cost = increase * 4000;
            cout << "💰 Cost to add " << increase << " park(s): $" << cost << "\n";
            cout << "Proceed? (y/n): ";
            char confirm;
            cin >> confirm;
            if ((confirm == 'y' || confirm == 'Y') && status.Total_Resources >= cost)
            {
                no_of_parks = new_count;
                status.Total_Resources -= cost;
                status.green_levels += increase * 5;
                status.population += increase * 100;
                status.sustainable_living += 0.003f * increase;
                status.clean_energy += 0.002f * increase;
                status.satisfaction_level += 0.002f * increase;
                cout << "✅ Added " << increase << " park(s).\n";
            }
            else if (confirm == 'y')
            {
                cout << "❌ Need $" << (cost - status.Total_Resources) << " more\n";
            }
            else
            {
                cout << "ℹ️ Operation cancelled.\n";
            }
        }
        else
        {
            no_of_parks = new_count;
            cout << "ℹ️ Park count set to " << new_count << ".\n";
        }
    }

    void handle_resources(Overall_Status &status)
    {
        cout << "🔋 Current renewable resources: " << renewable_resources << "\n";
        cout << "🔢 Enter new renewable resource value: ";
        double new_value;
        cin >> new_value;
        double delta = new_value - renewable_resources;

        if (delta > 0)
        {
            status.clean_energy += 0.005f * delta;
            status.sustainable_living += 0.003f * delta;
            status.green_levels += static_cast<int>(delta * 2);
            status.Total_Resources += delta * 500;
            cout << "✅ Resources increased by " << delta << ".\n";
        }
        else
        {
            cout << "ℹ️ Resources set to " << new_value << ".\n";
        }
        renewable_resources = new_value;
    }

    void handle_salaries(Overall_Status &status)
    {
        cout << "💼 Current total salaries: $" << salaries << "\n";
        cout << "🔢 Enter new total salary budget: ";
        double new_salaries;
        cin >> new_salaries;
        double difference = new_salaries - salaries;

        if (difference > 0)
        {
            cout << "💰 Additional needed: $" << difference << "\nProceed? (y/n): ";
            char confirm;
            cin >> confirm;
            if ((confirm == 'y' || confirm == 'Y') && status.Total_Resources >= difference)
            {
                salaries = new_salaries;
                status.Total_Resources -= difference;
                status.satisfaction_level += 0.0015f * (difference / 1000);
                status.minimum_salaries = salaries / employees;
                cout << "✅ Salaries increased to $" << new_salaries << ".\n";
            }
            else if (confirm == 'y')
            {
                cout << "❌ Insufficient funds for salary increase!\n";
            }
            else
            {
                cout << "ℹ️ Operation cancelled.\n";
            }
        }
        else
        {
            salaries = new_salaries;
            status.satisfaction_level -= 0.003f * abs(difference / 1000);
            status.minimum_salaries = salaries / max(employees, 1);
            cout << "ℹ️ Salaries decreased to $" << new_salaries << ". Satisfaction decreased.\n";
        }
    }

    void handle_staff(Overall_Status &status)
    {
        cout << "👥 Current staff: " << employees << "\n";
        cout << "🔢 Enter new total staff: ";
        int new_count;
        cin >> new_count;
        int increase = new_count - employees;

        if (increase > 0)
        {
            float cost = increase * 3000;
            cout << "💰 Cost to hire " << increase << " staff: $" << cost << "\nProceed? (y/n): ";
            char confirm;
            cin >> confirm;
            if ((confirm == 'y' || confirm == 'Y') && status.Total_Resources >= cost)
            {
                employees = new_count;
                status.Total_Resources -= cost;
                status.population += increase * 20;
                status.green_levels -= increase * 1;
                status.satisfaction_level += 0.001f * increase;
                cout << "✅ Hired " << increase << " staff.\n";
            }
            else if (confirm == 'y')
            {
                cout << "❌ Need $" << (cost - status.Total_Resources) << " more\n";
            }
            else
            {
                cout << "ℹ️ Operation cancelled.\n";
            }
        }
        else
        {
            employees = new_count;
            cout << "ℹ️ Staff count set to " << new_count << ".\n";
        }
        status.minimum_salaries = salaries / max(employees, 1);
    }

    void handle_upgrade(Overall_Status &status)
    {
        cout << "🏗️ Current level: " << level << "\n";
        cout << "🔢 Enter new level: ";
        int new_level;
        cin >> new_level;
        int increase = new_level - level;

        if (increase > 0)
        {
            float cost = increase * 10000;
            cout << "💰 Cost to upgrade by " << increase << " level(s): $" << cost << "\nProceed? (y/n): ";
            char confirm;
            cin >> confirm;
            if ((confirm == 'y' || confirm == 'Y') && status.Total_Resources >= cost)
            {
                level = new_level;
                status.Total_Resources -= cost;
                status.sustainable_living += 0.01f * increase;
                status.clean_energy += 0.008f * increase;
                status.green_levels += increase * 10;
                status.population += increase * 150;
                status.satisfaction_level += 0.004f * increase;
                cout << "✅ Upgraded to level " << new_level << ".\n";
            }
            else if (confirm == 'y')
            {
                cout << "❌ Need $" << (cost - status.Total_Resources) << " more\n";
            }
            else
            {
                cout << "ℹ️ Operation cancelled.\n";
            }
        }
        else
        {
            level = new_level;
            cout << "ℹ️ Level set to " << new_level << ".\n";
        }
    }

    template <typename T>
    T clamp(T value, T min, T max)
    {
        return std::max(min, std::min(value, max));
    }
};
class Resource_Management : public Health_Department
{
private:
    int water_reservoirs;
    int power_plants;
    string filename;

    void clamp_values(Overall_Status &status)
    {
        status.satisfaction_level = clamp(status.satisfaction_level, 0.0f, 1.0f);
        status.sustainable_living = clamp(status.sustainable_living, 0.0f, 1.0f);
        status.clean_energy = clamp(status.clean_energy, 0.0f, 1.0f);
        status.green_levels = max(status.green_levels, 0);
    }

public:
    Resource_Management(string username)
        : Health_Department(username), filename(username + "_resource.dat")
    {
        ifstream file(filename);
        if (file.good())
        {
            load_from_file();
        }
        else
        {
            // Default initialization
            water_reservoirs = 5;
            power_plants = 3;
            level = 1;
            employees = 40;
            salaries = 85000;
            save_to_file();
        }
    }

    void Display()
    {
        beauty();
        cout << "\n⚡ RESOURCE MANAGEMENT STATUS\n";
        cout << "├─ Department Level: " << level << "\n";
        cout << "├─ Water Reservoirs: " << water_reservoirs << "\n";
        cout << "├─ Power Plants: " << power_plants << "\n";
        cout << "├─ Technicians: " << employees << "\n";
        cout << "└─ Salary Budget: $" << fixed << setprecision(2) << salaries << "\n";
        beauty();
    }

    void save_to_file()
    {
        ofstream file(filename);
        file << level << "\n"
             << employees << "\n"
             << salaries << "\n"
             << water_reservoirs << "\n"
             << power_plants;
    }

    void load_from_file()
    {
        ifstream file(filename);
        string line;

        getline(file, line);
        level = stoi(line);
        getline(file, line);
        employees = stoi(line);
        getline(file, line);
        salaries = stod(line);
        getline(file, line);
        water_reservoirs = stoi(line);
        getline(file, line);
        power_plants = stoi(line);
    }

    void update(Overall_Status &status)
    {
        beauty();
        cout << "\n========= RESOURCE MANAGEMENT UPDATE =========\n";
        cout << "1. Manage Water Reservoirs\n";
        cout << "2. Manage Power Plants\n";
        cout << "3. Adjust Salaries\n";
        cout << "4. Modify Workforce\n";
        cout << "5. Upgrade Department\n";
        cout << "6. Exit\n";
        cout << "===============================================\n";
        cout << "Enter your option (1-6): ";

        int option;
        cin >> option;

        switch (option)
        {
        case 1:
            handle_water_reservoirs(status);
            break;
        case 2:
            handle_power_plants(status);
            break;
        case 3:
            handle_salaries(status);
            break;
        case 4:
            handle_staff(status);
            break;
        case 5:
            handle_upgrade(status);
            break;
        case 6:
            cout << "Exiting...\n";
            return;
        default:
            cout << "Invalid option!\n";
        }

        clamp_values(status);
        save_to_file();
        status.save_to_file(filename);

        beauty();
        cout << "✅ Update completed successfully!\n";
        beauty();
    }

private:
    void handle_water_reservoirs(Overall_Status &status)
    {
        cout << "💧 Current water reservoirs: " << water_reservoirs << "\n";
        cout << "🔢 Enter new total reservoirs: ";
        int new_count;
        cin >> new_count;
        int increase = new_count - water_reservoirs;

        if (increase > 0)
        {
            float cost = increase * 8000;
            cout << "💰 Cost to add " << increase << " reservoir(s): $" << cost << "\n";
            cout << "Proceed? (y/n): ";
            char confirm;
            cin >> confirm;
            if ((confirm == 'y' || confirm == 'Y') && status.Total_Resources >= cost)
            {
                water_reservoirs = new_count;
                status.Total_Resources -= cost;
                status.population += increase * 200;
                status.sustainable_living += 0.002f * increase;
                status.green_levels -= increase * 3;
                status.satisfaction_level += 0.001f * increase;
                cout << "✅ Added " << increase << " reservoir(s).\n";
            }
            else if (confirm == 'y')
            {
                cout << "❌ Need $" << (cost - status.Total_Resources) << " more\n";
            }
            else
            {
                cout << "ℹ️ Operation cancelled.\n";
            }
        }
        else
        {
            water_reservoirs = new_count;
            cout << "ℹ️ Reservoir count set to " << new_count << ".\n";
        }
    }

    void handle_power_plants(Overall_Status &status)
    {
        cout << "⚡ Current power plants: " << power_plants << "\n";
        cout << "🔢 Enter new total power plants: ";
        int new_count;
        cin >> new_count;
        int increase = new_count - power_plants;

        if (increase > 0)
        {
            float cost = increase * 15000;
            cout << "💰 Cost to add " << increase << " plant(s): $" << cost << "\n";
            cout << "Proceed? (y/n): ";
            char confirm;
            cin >> confirm;
            if ((confirm == 'y' || confirm == 'Y') && status.Total_Resources >= cost)
            {
                power_plants = new_count;
                status.Total_Resources -= cost;
                status.Total_Resources += increase * 5000; // revenue
                status.clean_energy -= 0.005f * increase;
                status.green_levels -= increase * 5;
                status.sustainable_living -= 0.003f * increase;
                status.population += increase * 150;
                cout << "✅ Added " << increase << " power plant(s).\n";
            }
            else if (confirm == 'y')
            {
                cout << "❌ Need $" << (cost - status.Total_Resources) << " more\n";
            }
            else
            {
                cout << "ℹ️ Operation cancelled.\n";
            }
        }
        else
        {
            power_plants = new_count;
            cout << "ℹ️ Power plant count set to " << new_count << ".\n";
        }
    }

    void handle_salaries(Overall_Status &status)
    {
        cout << "💼 Current total salaries: $" << salaries << "\n";
        cout << "🔢 Enter new salary budget: ";
        double new_salaries;
        cin >> new_salaries;
        double diff = new_salaries - salaries;

        if (diff > 0)
        {
            cout << "💰 Additional needed: $" << diff << "\nProceed? (y/n): ";
            char confirm;
            cin >> confirm;
            if ((confirm == 'y' || confirm == 'Y') && status.Total_Resources >= diff)
            {
                salaries = new_salaries;
                status.Total_Resources -= diff;
                status.minimum_salaries = salaries / employees;
                status.satisfaction_level += 0.001f * (diff / 1000);
                cout << "✅ Salaries increased to $" << new_salaries << ".\n";
            }
            else if (confirm == 'y')
            {
                cout << "❌ Insufficient funds!\n";
            }
            else
            {
                cout << "ℹ️ Operation cancelled.\n";
            }
        }
        else
        {
            salaries = new_salaries;
            status.minimum_salaries = salaries / max(employees, 1);
            status.satisfaction_level -= 0.002f * abs(diff / 1000);
            cout << "ℹ️ Salaries decreased to $" << new_salaries << ".\n";
        }
    }

    void handle_staff(Overall_Status &status)
    {
        cout << "👥 Current staff: " << employees << "\n";
        cout << "🔢 Enter new total staff: ";
        int new_count;
        cin >> new_count;
        int increase = new_count - employees;

        if (increase > 0)
        {
            float cost = increase * 3000;
            cout << "💰 Cost to hire " << increase << " staff: $" << cost << "\nProceed? (y/n): ";
            char confirm;
            cin >> confirm;
            if ((confirm == 'y' || confirm == 'Y') && status.Total_Resources >= cost)
            {
                employees = new_count;
                status.Total_Resources -= cost;
                status.population += increase * 25;
                status.green_levels -= increase;
                status.satisfaction_level += 0.0008f * increase;
                cout << "✅ Hired " << increase << " staff.\n";
            }
            else if (confirm == 'y')
            {
                cout << "❌ Need $" << (cost - status.Total_Resources) << " more\n";
            }
            else
            {
                cout << "ℹ️ Operation cancelled.\n";
            }
        }
        else
        {
            employees = new_count;
            cout << "ℹ️ Staff count set to " << new_count << ".\n";
        }
        status.minimum_salaries = salaries / max(employees, 1);
    }

    void handle_upgrade(Overall_Status &status)
    {
        cout << "🏗️ Current level: " << level << "\n";
        cout << "🔢 Enter new level: ";
        int new_level;
        cin >> new_level;
        int increase = new_level - level;

        if (increase > 0)
        {
            float cost = increase * 10000;
            cout << "💰 Cost to upgrade by " << increase << " level(s): $" << cost << "\nProceed? (y/n): ";
            char confirm;
            cin >> confirm;
            if ((confirm == 'y' || confirm == 'Y') && status.Total_Resources >= cost)
            {
                level = new_level;
                status.Total_Resources -= cost;
                status.sustainable_living += 0.01f * increase;
                status.clean_energy += 0.005f * increase;
                status.green_levels += increase * 2;
                status.population += increase * 150;
                status.Total_Resources += increase * 10000; // bonus resources
                status.satisfaction_level += 0.002f * increase;
                cout << "✅ Upgraded to level " << new_level << ".\n";
            }
            else if (confirm == 'y')
            {
                cout << "❌ Need $" << (cost - status.Total_Resources) << " more\n";
            }
            else
            {
                cout << "ℹ️ Operation cancelled.\n";
            }
        }
        else
        {
            level = new_level;
            cout << "ℹ️ Level set to " << new_level << ".\n";
        }
    }

    template <typename T>
    T clamp(T value, T min, T max)
    {
        return std::max(min, std::min(value, max));
    }
};
class Climate_Summit
{
public:
    vector<string> users;
    vector<Overall_Status> statuses;
    string me;

    Climate_Summit()
    {
        load_users("passwords_username.txt");
    }

    void run()
    {
        cout << "🌍 Welcome to Climate Summit 🌍\n";
        me=filepath1;

        while (true)
        {
            cout << "\n📊 Menu 📊\n";
            cout << "1️⃣ Show Dashboard\n";
            cout << "2️⃣ Donate Resources\n";
            cout << "3️⃣ Exit\n";
            cout << "Choose (1-3): ";
            int choice;
            cin >> choice;

            if (choice == 1)
                show_dashboard(me);
            else if (choice == 2)
            {
                cout << "➡️ Donate to: ";
                string to;
                float amt;
                cin >> to;
                cout << "💰 Amount: $";
                cin >> amt;
                donate(me, to, amt);
            }
            else if (choice == 3)
            {
                cout << "👋 Goodbye!\n";
                break;
            }
            else
                cout << "❌ Invalid choice\n";
        }
    }

    void show_dashboard(const string &username)
    {
        int idx = find_user(username);
        if (idx < 0)
        {
            cout << "❌ User not found\n";
            return;
        }
        statuses[idx].Display();

        float mySat = statuses[idx].satisfaction_level;
        float myRes = statuses[idx].Total_Resources;
        float myCE  = statuses[idx].clean_energy;
        float mySL  = statuses[idx].sustainable_living;

        int rSat = 1, rRes = 1, rCE = 1, rSL = 1;
        for (auto &s : statuses)
        {
            if (s.satisfaction_level   > mySat) ++rSat;
            if (s.Total_Resources      > myRes) ++rRes;
            if (s.clean_energy         > myCE)  ++rCE;
            if (s.sustainable_living   > mySL)  ++rSL;
        }

        cout << "\n🏅 Your Rankings 🏅\n";
        cout << "😊 Satisfaction:    #" << rSat << "\n";
        cout << "💰 Resources:       #" << rRes << "\n";
        cout << "⚡ Clean Energy:    #" << rCE << "\n";
        cout << "🌱 Sustainability:  #" << rSL << "\n";
    }

    void donate(const string &from, const string &to, float amount)
    {
        int iFrom = find_user(from);
        int iTo   = find_user(to);
        if (iFrom < 0 || iTo < 0)
        {
            cout << "❌ User not found\n";
            return;
        }
        if (statuses[iFrom].Total_Resources < amount)
        {
            cout << "❌ Not enough resources\n";
            return;
        }

        statuses[iFrom].Total_Resources -= amount;
        statuses[iTo].Total_Resources   += amount;
        statuses[iFrom].save_to_file(users[iFrom] + "_Overall_status.txt");
        statuses[iTo].save_to_file(users[iTo]   + "_Overall_status.txt");

        cout << "✅ $" << amount << " sent from " << from << " to " << to << "\n";
    }

private:
    void load_users(const string &credentials_file)
    {
        ifstream in(credentials_file);
        vector<string> lines;
        string line;
        while (getline(in, line))
            if (!line.empty())
                lines.push_back(line);

        for (size_t i = 0; i < lines.size(); i += 2)
        {
            users.push_back(lines[i]);
            Overall_Status st;
            st.load_from_file(lines[i] + "_Overall_status.txt");
            statuses.push_back(st);
        }
    }

    int find_user(const string &username) const
    {
        for (int i = 0; i < (int)users.size(); ++i){
            if (users[i] == username)
                return i;
                }
        return -1;
    }
};
int interlinking_menu()
{
ask:
    int option;
    beauty();
    cout << "\n🌆 ====== CITY INTERLINKING MENU ====== 🌆\n";
    cout << "1️⃣  SEE HOW OVERALL CITY IS DOING\n";
    cout << "2️⃣  EXERCISE YOUR POWERS TO MAKE CHANGES IN DEPARTMENTS\n";
    cout << "3️⃣  COLLABORATE IN VIRTUAL CLIMATE SUMMIT\n";
    cout << "4️⃣  EXIT\n";
    cout << "\n👉 ENTER CHOICE (1-4): ";
    cin >> option;
    if (option < 1 || option > 4)
    {
        cout << "\n❌ Invalid input. Please try again <3\n";
        goto ask;
    }
    beauty();
    return option;
}


int excercising_powers_menu()
{
    int option;
ask:
    beauty();
    cout << "\n✨================= YOU CAN MAKE CHANGES IN THE RESPECTIVE DEPARTMENTS ❤️=================\n";
    cout << "🔄 0. Update Resources And Make Changes\n\n";
    cout << "🌿 1. Environment Department\n";
    cout << "🏗️ 2. Construction Department\n";
    cout << "🛠️ 3. Maintenance Department\n";
    cout << "💰 4. Finance Department\n";
    cout << "🎓 5. Education Department\n";
    cout << "🏥 6. Health Department\n";
    cout << "🚍 7. Transport Department\n";
    cout << "👮 8. Police Department\n";
    cout << "❌ 9. Exit\n";
    cout << "🔢 Enter your choice (0–9): ";
    cin >> option;
    if (option < 0 || option > 9)
    {
        cout << "\nInvalid input try again <3" << endl;
        goto ask;
    }
    beauty();
    return (option);
}
int display_Things()
{
    int option;
ask:
    beauty();
    cout << "\n🚀✨================= DISPLAY PROGRESS OF DEPARTMENTS 💖=================\n";
    cout << "💎 0. Resources Department\n";
    cout << "🌱 1. Environment Department\n";
    cout << "🏗️ 2. Construction Department\n";
    cout << "🔧 3. Maintenance Department\n";
    cout << "💵 4. Finance Department\n";
    cout << "📚 5. Education Department\n";
    cout << "🩺 6. Health Department\n";
    cout << "🚌 7. Transport Department\n";
    cout << "🚔 8. Police Department\n";
    cout << "❌ 9. Exit\n";
    cout << "🔢 Enter your choice (0–9): ";

    cin >> option;
    if (option < 0 || option > 9)
    {
        cout << "\nInvalid input try again <3" << endl;
        goto ask;
    }
    beauty();
    return (option);
}
void Setup()
{
    bool running = true;
    Overall_Status status;

    // Load existing status
    Overall_Status sta;
    sta.load_from_file(filepath2);

    while (running)
    {
        int option = interlinking_menu();

        switch (option)
        {
        case 1:
        {
            Overall_Status stats;
            stats.load_from_file(filepath2);
            stats.Display();
            beauty();

            int op = display_Things();
            switch (op)
            {
            case 0:
            {
                FinanceDepartment fin(filepath1);
                fin.load_from_file();
                fin.Display();
                break;
            }
            case 1:
            {
                Environmental_Department envio(filepath1);
                envio.load_from_file();
                envio.Display();
                break;
            }
            case 2:
            {
                Construction_Department cons(filepath1);
                cons.load_from_file();
                cons.Display();
                break;
            }
            case 3:
            {
                Maintenance_Department maint(filepath1);
                maint.load_from_file();
                maint.Display();
                break;
            }
            case 4:
            {
                FinanceDepartment finance(filepath1);
                finance.load_from_file();
                finance.Display();

                break;
            }
            case 5:
            {
                Educational_Department edu(filepath1);
                edu.load_from_file();
                edu.Display();
                break;
            }
            case 6:
            {
                Health_Department health(filepath1);
                health.load_from_file();
                health.Display();
                break;
            }
            case 7:
            {
                Transport_Department trans(filepath1);
                trans.load_from_file();
                trans.Display();
                break;
            }
            case 8:
            {
                Police_Department police(filepath1);
                police.load_from_file();
                police.Display();
                break;
            }
            }

            break;
        }

        case 2:
        {
            int dept = excercising_powers_menu();
            switch (dept)
            {
            case 1:
            {
                Environmental_Department envio(filepath1);
                envio.load_from_file();
                envio.update(status);
                envio.save_to_file();
                break;
            }
            case 2:
            {
                Construction_Department cons(filepath1);
                cons.load_from_file();
                cons.update(status);
                cons.save_to_file();
                break;
            }
            case 3:
            {
                Maintenance_Department maint(filepath1);
                maint.load_from_file();
                maint.update(status);
                maint.save_to_file();
                break;
            }
            case 4:
            {
                FinanceDepartment finance(filepath1);
                finance.load_from_file();
                finance.update(status);
                finance.save_to_file();
                break;
            }
            case 5:
            {
                Educational_Department edu(filepath1);
                edu.load_from_file();
                edu.update(status);
                edu.save_to_file();
                break;
            }
            case 6:
            {
                Health_Department health(filepath1);
                health.load_from_file();
                health.update(status);
                health.save_to_file();
                break;
            }
            case 7:
            {
                Transport_Department trans(filepath1);
                trans.load_from_file();
                trans.update(status);
                trans.save_to_file();
                break;
            }
            case 8:
            {
                Police_Department police(filepath1);
                police.load_from_file();
                police.update(status);
                police.save_to_file();
                break;
            }
            case 0:
            {
                FinanceDepartment fin(filepath1);
                fin.load_from_file();
                fin.update(status);
                fin.save_to_file();
            }
            }

            // Save status after changes
            ofstream status_out(filepath2);
            status_out << status.satisfaction_level << " "
                       << status.minimum_salaries << " "
                       << status.Total_Resources << " "
                       << status.population << " "
                       << status.green_levels << " "
                       << status.sustainable_living << " "
                       << status.clean_energy;
            break;
        }
        case 3:
        {
            // Climate summit implementation
            beauty();
            Climate_Summit summit;
            summit.run();
            break;
        }
        case 4:
            running = false;
            break;
        }
    }
}
void Mayor()
{
    int option;
    beauty();
    cout << "\n                       WELCOME SIR BACK TO THE OFFICE .<3" << endl;
    cout << "\nMAY YOU SERVVE THE PEOPLE OF CITY AND MAKE DESICIONS ACCORDING TO THE WELFARE OF SOCIETY" << endl;
    beauty();
    Setup();
}

int main()
{
    SetConsoleOutputCP(CP_UTF8);
    bool close_external = true;
    array<string, 2> user_data;
    Username = user_data[0];
    do
    {
        char option_external;
        option_external = menu_external();
        switch (option_external)
        {
        case 'L':
        {
            user_data = login();
            filepath1 = (user_data[0]);
            fstream my_file1;
            my_file1.open(filepath1, ios::app);
            if (!my_file1.is_open())
            {
                cout << "Failed to Open File " << endl;
            }
            my_file1.close();
            filepath2 = (user_data[0] + "_Overall_status.txt");
            fstream my_file2;
            my_file2.open(filepath2, ios::app);
            if (!my_file2.is_open())
            {
                cout << "Failed to Open File " << endl;
            }
            if (my_file2.tellg() == 0) {
                Overall_Status stat;
                stat.save_to_file(filepath2);
            } 
            
            my_file2.close();

            close_external = false;
            break;
        }
        case 'O':
        {
            sign_up();
            break;
        }
        case 'E':
        {
            return 0;
        }
        }
    } while (close_external == true);
    Overall_Status stat;
    Mayor();

    return 0;
}
