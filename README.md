                                      # BookshopManagementSystem
Develop a C++ Bookshop Management System using inheritance and polymorphism. The system allows adding textbooks and novels, searching by title or ISBN, and displaying books. Textbooks have a subject and novels have a genre. The program provides a menu-based interface with options to add, search, display, and exit.

The system should allow the user to perform various operations such as adding textbooks and novels to the bookshop, searching for books by title or ISBN, and displaying all the books in the bookshop.

The system should utilize inheritance and polymorphism concepts to model different types of books. There are two types of books: textbooks and novels. Both types of books share common attributes such as title, author, ISBN, price, and quantity. However, textbooks also have an additional attribute called subject, while novels have a genre.

The program should provide a menu-based interface where the user can select different options. The menu should include the following options:

FEATURES:

=>Add Textbook: This option allows the user to add a new textbook to the bookshop. The user should be prompted to enter the title, author, ISBN, price, quantity, and subject of the textbook.

=>Add Novel: This option allows the user to add a new novel to the bookshop. The user should be prompted to enter the title, author, ISBN, price, quantity, and genre of the novel.

=>Search Book : This option enables the user to search for a book in the bookshop by its title or ISBN or gerne or subject. The program should display all the books whose title or subject matches the search term entered by the user.

=>Display Books: This option displays all the books currently available in the bookshop, along with their respective details such as title, author, ISBN, price, and quantity.

=>Exit: This option terminates the program.


                                             CODE

```

#include <iostream>
#include <string>

using namespace std;
// declare a base class book
class Book {
protected:
    string title;
    string author;
    string ISBN;
    double price;
    int quantity;

public:
    Book(const string& title, const string& author, const string& ISBN, double price, int quantity)
        : title(title), author(author), ISBN(ISBN), price(price), quantity(quantity) {}

    virtual void displayInfo() {
        cout << "Title: " << title << endl;
        cout << "Author: " << author << endl;
        cout << "ISBN: " << ISBN << endl;
        cout << "Price: " << price << endl;
        cout << "Quantity: " << quantity << endl;
    }

    virtual bool search(const string& searchTitle) {
        return title == searchTitle;
    }

    virtual ~Book() {}
};
// declare a derived class textbook 
class Textbook : public Book {
private:
    string subject;

public:
    Textbook(const string& title, const string& author, const string& ISBN, double price, int quantity, const string& subject)
        : Book(title, author, ISBN, price, quantity), subject(subject) {}
    //override the displayinfo function in textbook class
    void displayInfo() override {
        cout << "--- Textbook ---" << endl;
        Book::displayInfo();
        cout << "Subject: " << subject << endl;
    }
    //override the search function in textbook class
    bool search(const string& searchTitle) override {
        return title == searchTitle || subject == searchTitle;
    }
};

class Novel : public Book {
private:
    string genre;

public:
    Novel(const string& title, const string& author, const string& ISBN, double price, int quantity, const string& genre)
        : Book(title, author, ISBN, price, quantity), genre(genre) {}
    //override the displayinfo function in novel class
    void displayInfo() override {
        cout << "--- Novel ---" << endl;
        Book::displayInfo();
        cout << "Genre: " << genre << endl;
    }
    //override the search function in textbook class
    bool search(const string& searchTitle) override {
        return title == searchTitle || genre == searchTitle || ISBN==searchTitle;
    }
};
//create a addbook function which helps in adding a new book

void addBook(Book* book) {
    book->displayInfo();
    cout << "Book added successfully!\n";
    delete book;
}

//create a searchbook function which helps in finding a book 
//in this function we can find the book by using tittle ,isbn, gerene and subject
void searchBook(Book** books, int size, const string& searchTitle) {
    bool found = false;
    for (int i = 0; i < size; ++i) {
        if (books[i]->search(searchTitle)) {
            found = true;
            books[i]->displayInfo();
        }
    }
    if (!found) {
        cout << "Book not found!\n";
    }
}
//displaybooks function helps to print the collection of books
void displayBooks(Book** books, int size) {
    for (int i = 0; i < size; ++i) {
        books[i]->displayInfo();
        cout << endl;
    }
}

int main() {
    const int MAX_BOOKS = 100;
    Book* books[MAX_BOOKS];
    int bookCount = 0;
// use do-while loop to make many choices and choice 5 to exit the loop
    int choice;
    do {
        cout << "========== Bookshop Management System ==========\n";
        cout << "1. Add Textbook\n";
        cout << "2. Add Novel\n";
        cout << "3. Search Book\n";
        cout << "4. Display Books\n";
        cout << "5. Exit\n";
        cout << "Enter your choice: ";
        cin >> choice;

        switch (choice) {
            case 1: {
                string title, author, ISBN, subject;
                double price;
                int quantity;
                cout << "Enter book title: ";
                cin.ignore();
                getline(cin, title);
                cout << "Enter author name: ";
                getline(cin, author);
                cout << "Enter ISBN: ";
                getline(cin, ISBN);
                cout << "Enter price: ";
                cin >> price;
                cout << "Enter quantity: ";
                cin >> quantity;
                cout << "Enter subject: ";
                cin.ignore();
                getline(cin, subject);
                Book* textbook = new Textbook(title, author, ISBN, price, quantity, subject);
                addBook(textbook);
                break;
            }
            case 2: {
                string title, author, ISBN, genre;
                double price;
                int quantity;
                cout << "Enter book title: ";
                cin.ignore();
                getline(cin, title);
                cout << "Enter author name: ";
                getline(cin, author);
                cout << "Enter ISBN: ";
                getline(cin, ISBN);
                cout << "Enter price: ";
                cin >> price;
                cout << "Enter quantity: ";
                cin >> quantity;
                cout << "Enter genre: ";
                cin.ignore();
                getline(cin, genre);
                Book* novel = new Novel(title, author, ISBN, price, quantity, genre);
                addBook(novel);
                break;
            }
            case 3: {
                string searchTitle;
                cout << "Enter the title or keyword to search: ";
                cin.ignore();
                getline(cin, searchTitle);
                searchBook(books, bookCount, searchTitle);
                break;
            }
            case 4: {
                displayBooks(books, bookCount);
                break;
            }
            // choice 5to exit the loop 
            case 5: {
                cout << "Exiting... Thank you!\n";
                break;
            }
            default: {
                cout << "Invalid choice. Please try again.\n";
                break;
            }
        }

        cout << endl;

    } while (choice != 5);

    for (int i = 0; i < bookCount; ++i) {
        delete books[i];
    }

    return 0;
}
```


