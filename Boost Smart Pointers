#include <iostream>
#include <string>
#include <vector>
#include <boost/shared_ptr.hpp>
#include <boost/weak_ptr.hpp>

// Define a Book class
class Book {
public:
    Book(const std::string& title, const std::string& author)
        : title_(title), author_(author) {}

    void PrintInfo() const {
        std::cout << "Title: " << title_ << ", Author: " << author_ << std::endl;
    }

private:
    std::string title_;
    std::string author_;
};

// Define a LibraryPatron class
class LibraryPatron {
public:
    LibraryPatron(const std::string& name) : name_(name) {}

    void PrintInfo() const {
        std::cout << "Patron Name: " << name_ << std::endl;
    }

private:
    std::string name_;
};

int main() {
    // Using boost::shared_ptr for managing books in the library
    std::vector<boost::shared_ptr<Book>> libraryBooks;

    // Add some books to the library
    libraryBooks.push_back(boost::make_shared<Book>("The Great Gatsby", "F. Scott Fitzgerald"));
    libraryBooks.push_back(boost::make_shared<Book>("To Kill a Mockingbird", "Harper Lee"));
    libraryBooks.push_back(boost::make_shared<Book>("1984", "George Orwell"));

    // Print information about each book in the library
    std::cout << "Books in the library:" << std::endl;
    for (const auto& book : libraryBooks) {
        book->PrintInfo();
    }

    // Using boost::weak_ptr for managing patrons borrowing books
    boost::weak_ptr<LibraryPatron> patron1;
    {
        // Create a library patron
        boost::shared_ptr<LibraryPatron> newPatron = boost::make_shared<LibraryPatron>("John");

        // Save a weak reference to the patron
        patron1 = newPatron;

        // Print information about the patron
        newPatron->PrintInfo();
    }

    // Check if the patron still exists
    if (auto lockedPatron = patron1.lock()) {
        std::cout << "Patron still exists: ";
        lockedPatron->PrintInfo();
    } else {
        std::cout << "Patron has been destroyed." << std::endl;
    }

    return 0;
}

/*

Explanation:

In this code, we define a Book class representing books in the library and a LibraryPatron class representing patrons who borrow books.
We use boost::shared_ptr to manage the dynamically allocated Book objects in the libraryBooks vector. This ensures that the memory for each book is automatically deallocated when there are no more references to it.
We use boost::weak_ptr to create a weak reference to a LibraryPatron object. This allows us to check if the LibraryPatron object still exists without affecting its lifetime.
The code demonstrates creating books in the library, printing information about each book, creating a library patron, printing information about the patron, and checking if the patron still exists using the weak pointer.
This example showcases how Boost Smart Pointers can be utilized in a library management system to ensure safe and efficient memory management.

*/
