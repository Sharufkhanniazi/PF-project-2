# PF project 2
 
Sharuf Zaryab Khan  231633.
Course: Programming Fundamentals
Instructor: Dr. Ashfaq Hussain Farooqi
Class: BSCS-IB
Project 2: Clothes Management System.

Code:

#include <iostream>
#include <fstream>
#include <string>
using namespace std;

const int MAX_RECORDS = 100; // Maximum number of records

// Function prototypes
void addclothes(int(*records)[4], int& recordCount);
void viewrecord(int(*records)[4], int recordCount);
void searchrecord(int(*records)[4], int recordCount);
void updaterecord(int(*records)[4], int recordCount);
void deleterecord(int(*records)[4], int& recordCount);
void exitrecord();

int main() {
    int records[MAX_RECORDS][4]; // 2D array to store records [ID, Quantity, Price, Name]
    int recordCount = 0; // Current count of records

    int choice;
    cout << "Cloth Management System\n";
    do {
        cout << "1. Add Clothes\n"
            << "2. Search Record\n"
            << "3. View Records\n"
            << "4. Update/edit Record\n"
            << "5. Delete Record\n"
            << "6. Exit\n"
            << "Enter your choice: ";
        cin >> choice;

        switch (choice) {
        case 1:
            addclothes(records, recordCount);
            break;
        case 2:
            searchrecord(records, recordCount);
            break;
        case 3:
            viewrecord(records, recordCount);
            break;
        case 4:
            updaterecord(records, recordCount);
            break;
        case 5:
            deleterecord(records, recordCount);
            break;
        case 6:
            exitrecord();
            break;
        default:
            cout << "Incorrect choice \n";
        }
    } while (choice != 6);

    return 0;
}

void addclothes(int(*records)[4], int& recordCount) {
    if (recordCount < MAX_RECORDS) {
        int clothid, quantity, price;
        string clothname;
        cout << "Enter Cloth Id: ";
        cin >> clothid;
        cout << "Enter price: ";
        cin >> price;
        cout << "Enter quantity: ";
        cin >> quantity;
        cout << "Enter cloth name: ";
        cin.ignore(); // Ignore the newline character in the buffer
        getline(cin, clothname);

        records[recordCount][0] = clothid;
        records[recordCount][1] = quantity;
        records[recordCount][2] = price;
        records[recordCount][3] = clothname.length(); // Storing length of name
        for (int i = 0; i < clothname.length(); ++i) {
            records[recordCount][4 + i] = clothname[i]; // Storing characters of name
        }
        recordCount++;
        cout << "Record added successfully.\n";
    }
    else {
        cout << "Maximum records reached, cannot add more.\n";
    }
}

void searchrecord(int(*records)[4], int recordCount) {
    int clothid;
    cout << "Enter id to search its record: ";
    cin >> clothid;
    bool found = false;
    for (int i = 0; i < recordCount; ++i) {
        if (records[i][0] == clothid) {
            found = true;
            cout << "Cloth ID: " << records[i][0] << endl;
            cout << "Quantity: " << records[i][1] << endl;
            cout << "Price: " << records[i][2] << endl;
            cout << "Cloth Name: ";
            for (int j = 0; j < records[i][3]; ++j) {
                cout << char(records[i][4 + j]); // Converting ASCII code to character
            }
            cout << endl;
            break;
        }
    }
    if (!found) {
        cout << clothid << " does not exist in the record.\n";
    }
}

void viewrecord(int(*records)[4], int recordCount) {
    cout << "Cloth ID\tQuantity\tPrice\tCloth Name\n";
    for (int i = 0; i < recordCount; ++i) {
        cout << records[i][0] << "\t\t" << records[i][1] << "\t\t" << records[i][2] << "\t\t";
        for (int j = 0; j < records[i][3]; ++j) {
            cout << char(records[i][4 + j]); // Converting ASCII code to character
        }
        cout << endl;
    }
}

void updaterecord(int(*records)[4], int recordCount) {
    int clothid;
    cout << "Enter id to update its record: ";
    cin >> clothid;
    bool found = false;
    for (int i = 0; i < recordCount; ++i) {
        if (records[i][0] == clothid) {
            found = true;
            cout << "Enter updated details for the record:\n";
            cout << "New Quantity: ";
            cin >> records[i][1];
            cout << "New Price: ";
            cin >> records[i][2];
            cout << "New Cloth Name: ";
            cin.ignore();
            string clothname;
            getline(cin, clothname);
            records[i][3] = clothname.length();
            for (int j = 0; j < clothname.length(); ++j) {
                records[i][4 + j] = clothname[j];
            }
            cout << "Record updated successfully.\n";
            break;
        }
    }
    if (!found) {
        cout << clothid << " does not exist in the record.\n";
    }
}

void deleterecord(int(*records)[4], int& recordCount) {
    int clothid;
    cout << "Enter id to delete its record: ";
    cin >> clothid;
    bool found = false;
    for (int i = 0; i < recordCount; ++i) {
        if (records[i][0] == clothid) {
            found = true;
            for (int j = i; j < recordCount - 1; ++j) {
                for (int k = 0; k < 4 + records[j][3]; ++k) {
                    records[j][k] = records[j + 1][k];
                }
            }
            recordCount--;
            cout << "Record with ID " << clothid << " deleted successfully.\n";
            break;
        }
    }
    if (!found) {
        cout << clothid << " does not exist in the record.\n";
    }
}

void exitrecord() {
    cout << "Exiting from the system...";
    exit(0);
}