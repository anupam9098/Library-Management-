# Library-Management-
#include <iostream>
#include <vector>
#include <string>
using namespace std;

// Book class
class Book {
public:
    int bookID;
    string title;
    string author;
    bool isIssued;

    Book(int id, string t, string a) {
        bookID = id;
        title = t;
        author = a;
        isIssued = false;
    }
};

// Library class
class Library {
private:
    vector<Book> books;

public:
    // Add a book
    void addBook(int id, string title, string author) {
        books.emplace_back(id, title, author);
        cout << "Book added successfully!\n";
    }

    // Display all books
    void displayBooks() {
        if (books.empty()) {
            cout << "No books in the library.\n";
            return;
        }
        cout << "Books in the library:\n";
        for (const auto &book : books) {
            cout << "ID: " << book.bookID << ", Title: " << book.title
                 << ", Author: " << book.author
                 << ", Status: " << (book.isIssued ? "Issued" : "Available") << endl;
        }
    }

    // Search for a book
    void searchBook(int id) {
        for (const auto &book : books) {
            if (book.bookID == id) {
                cout << "Book found: Title: " << book.title << ", Author: " << book.author
                     << ", Status: " << (book.isIssued ? "Issued" : "Available") << endl;
                return;
            }
        }
        cout << "Book not found.\n";
    }

    // Issue a book
    void issueBook(int id) {
        for (auto &book : books) {
            if (book.bookID == id) {
                if (book.isIssued) {
                    cout << "Book is already issued.\n";
                } else {
                    book.isIssued = true;
                    cout << "Book issued successfully!\n";
                }
                return;
            }
        }
        cout << "Book not found.\n";
    }

    // Return a book
    void returnBook(int id) {
        for (auto &book : books) {
            if (book.bookID == id) {
                if (book.isIssued) {
                    book.isIssued = false;
                    cout << "Book returned successfully!\n";
                } else {
                    cout << "Book was not issued.\n";
                }
                return;
            }
        }
        cout << "Book not found.\n";
    }
};

// Main function
int main() {
    Library library;
    int choice, id;
    string title, author;

    while (true) {
        cout << "\nLibrary Management System\n";
        cout << "1. Add Book\n";
        cout << "2. Display Books\n";
        cout << "3. Search Book\n";
        cout << "4. Issue Book\n";
        cout << "5. Return Book\n";
        cout << "6. Exit\n";
        cout << "Enter your choice: ";
        cin >> choice;

        switch (choice) {
        case 1:
            cout << "Enter Book ID: ";
            cin >> id;
            cin.ignore(); // Clear input buffer
            cout << "Enter Book Title: ";
            getline(cin, title);
            cout << "Enter Book Author: ";
            getline(cin, author);
            library.addBook(id, title, author);
            break;
        case 2:
            library.displayBooks();
            break;
        case 3:
            cout << "Enter Book ID to search: ";
            cin >> id;
            library.searchBook(id);
            break;
        case 4:
            cout << "Enter Book ID to issue: ";
            cin >> id;
            library.issueBook(id);
            break;
        case 5:
            cout << "Enter Book ID to return: ";
            cin >> id;
            library.returnBook(id);
            break;
        case 6:
            cout << "Exiting the program. Goodbye!\n";
            return 0;
        default:
            cout << "Invalid choice. Please try again.\n";
        }
    }
}
