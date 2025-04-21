# Smart-City

#include <iostream>
#include <fstream>
#include <string>
#include <cmath>
#include <iomanip>
#include <ctime>
using namespace std;
string filepath1 = "initial";
void beauty()
{
    cout << "\n\n*************************************************************************************************************************************************\n\n";
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
    

    if (option_exter > 3 || option_exter < 1)
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
class Setup
{
};
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
        cout << "YOUR ACCOUNT NO. IS : " << account_no << endl;

        passw.open("passwords_username.txt", ios::out | ios::app);
        passw << username << endl;
        passw << password << endl;
        passw.close();
    }
    cout << "THANKS FOR OPENNING AN ACCOUNT <3" << endl;
    beauty();
}
class Health_Departement
{
};
class Educational_Departement
{
};
class Finance_Departement
{
};
class Transport_Departement
{
};
class Construction_Departement
{
};
class Maintainence_Departement
{
};
class Environmental_Departement
{
};
class Police_Departement
{
};
class Resource_Managment
{
};
void Mayor()
{
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
