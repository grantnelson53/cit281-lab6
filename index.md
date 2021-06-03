## Lab 6

In this lab, we learned all about classes 

### Source Code 

    class Book {
      constructor(title, author, pubDate, isbn) {
        this.title = title;
        this.author = author;
        this.pubDate = pubDate;
        this.isbn = isbn;
      }
    }

    class Library {
      constructor(name) {
        this._name = name;
        this._books = [];
      }
      get books() {
        // Return copy of books
        return JSON.parse(JSON.stringify(this._books));
      }
      get count() {
        return this._books.length;
      }
      addBook(book = {}) {
        const { title = "", author = "", pubDate = "", isbn = "" } = book;
        if (title.length > 0 && author.length > 0) {
          const newBook = { title, author, pubDate, isbn };
          this._books.push(newBook);
        }
      }
      listBooks() {
        for (const book of this._books) {
          const { title, author, pubDate, isbn } = book;
          console.log(`Title: ${title}, Author: ${author}, PubDate: ${pubDate}, ISBN: ${isbn}`);
        }
      }

      deleteBook(isbn) {

        let indexOfBookToRemove = null;
        for (let index = 0; index < this._books.length; index++) {
            let currentBook = this._books[index];
            if (currentBook.isbn == isbn) {
                indexOfBookToRemove = index;
                break;
            }
        }

        this._books.splice(indexOfBookToRemove, 1);

      }
    }


    const myBook = new Book("AP Calc Crash Course", "Grant L. Nelson", "04/20/1969", "111566187423");
    const atomicHabits = new Book("Atomic Habits", "James Clear", "10/16/2018", "123456789048");

    const uoLibrary = new Library("Knight Library");
    uoLibrary.addBook(myBook);
    uoLibrary.addBook(atomicHabits);
    //console.log(myBook);
    console.log(`Book count: ${uoLibrary.count}`);
    uoLibrary.listBooks();

    console.log("Deleting Book");
    uoLibrary.deleteBook("111566187423");
    uoLibrary.listBooks();
