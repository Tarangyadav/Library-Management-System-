#include <iostream>
#include <string>
using namespace std;

class Library {
private:
    string books[100];
    int copies[100];
    int issued[100];
    int count;

public:
    Library() {
        count = 0;
        for (int i = 0; i < 100; i++) {
            copies[i] = 0;
            issued[i] = 0;
        }
    }

    void addBook() {
        if (count >= 100) {
            cout << "Library full!\n";
            return;
        }

        cout << "Enter Book Name: ";
        getline(cin >> ws, books[count]);
        copies[count] = 4;
        issued[count] = 0;
        count++;
        cout << "Book added successfully!\n";
    }

    void deleteBook() {
        string name;
        cout << "Enter Book Name to Delete: ";
        getline(cin >> ws, name);
        for (int i = 0; i < count; i++) {
            if (books[i] == name) {
                books[i].clear();
                copies[i] = 0;
                issued[i] = 0;
                cout << "Book deleted!\n";
                return;
            }
        }
        cout << "Book not found!\n";
    }

    void showBooks() {
        cout << "\n--- Library Books ---\n";
        for (int i = 0; i < count; i++) {
            if (!books[i].empty())
                cout << i + 1 << ". " << books[i] << " (Copies: " 
                     << (copies[i] - issued[i]) << ")\n";
        }
    }

    void searchBook() {
        string name;
        cout << "Enter Book Name to Search: ";
        getline(cin >> ws, name);
        for (int i = 0; i < count; i++) {
            if (books[i] == name) {
                cout << "Book found at position: " << i + 1 << endl;
                return;
            }
        }
        cout << "Book not found!\n";
    }

    void issueBook() {
        string name;
        cout << "Enter Book Name to Issue: ";
        getline(cin >> ws, name);
        for (int i = 0; i < count; i++) {
            if (books[i] == name) {
                if (issued[i] < copies[i]) {
                    issued[i]++;
                    cout << "Book issued successfully!\n";
                } else {
                    cout << "No copies available!\n";
                }
                return;
            }
        }
        cout << "Book not found!\n";
    }

    void returnBook() {
        string name;
        cout << "Enter Book Name to Return: ";
        getline(cin >> ws, name);
        for (int i = 0; i < count; i++) {
            if (books[i] == name) {
                if (issued[i] > 0) {
                    issued[i]--;
                    cout << "Book returned successfully!\n";
                } else {
                    cout << "No copies were issued!\n";
                }
                return;
            }
        }
        cout << "Book not found!\n";
    }
};

int main() {
    Library lib;
    int mainChoice, choice;

    while (true) {
        cout << "\n===== LIBRARY MANAGEMENT SYSTEM =====\n";
        cout << "1. Admin\n2. Student\n0. Exit\nEnter choice: ";
        cin >> mainChoice;

        if (mainChoice == 0) break;

        if (mainChoice == 1) {
            cout << "\n--- Admin Menu ---\n";
            cout << "1. Add Book\n2. Delete Book\n3. Show Books\n0. Back\nEnter choice: ";
            cin >> choice;
            switch (choice) {
                case 1: lib.addBook(); break;
                case 2: lib.deleteBook(); break;
                case 3: lib.showBooks(); break;
                default: break;
            }
        } 
        else if (mainChoice == 2) {
            cout << "\n--- Student Menu ---\n";
            cout << "1. Search Book\n2. Issue Book\n3. Return Book\n0. Back\nEnter choice: ";
            cin >> choice;
            switch (choice) {
                case 1: lib.searchBook(); break;
                case 2: lib.issueBook(); break;
                case 3: lib.returnBook(); break;
                default: break;
            }
        } 
        else {
            cout << "Invalid choice!\n";
        }
    }

    cout << "Exiting... Thank you!\n";
    return 0;
}
