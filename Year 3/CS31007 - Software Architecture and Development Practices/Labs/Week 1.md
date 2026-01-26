
| Line(s)    | Principle Broken                | Why?                                                                                                                    | How to Resolve                                                                  | Revised Code   |
| ---------- | ------------------------------- | ----------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------- | -------------- |
| 81-86      | YAGNI                           | Loyalty member not implemented yet                                                                                      | Remove this code                                                                | [[#81-86]]     |
| 50         | KISS / LoD                      | Complicated & used lots of chained functions                                                                            | Refactor to use some other, simpler approach                                    | [[#50]]        |
| 36 & 41    | Meaningful Variable Names       | variable name "b" is used multiple times in this function for different reasons, and is confusing and will cause errors | change variable names to be more meaningful                                     | [[#36 & 41]]   |
| 145        | Meaningful Variable Names       | Function name "return" is already a Java keyword, so cannot be used as a function name                                  | change to "handIn" or similar                                                   | [[#145]]       |
| 119 & 161  | Meaningful Variable Names       | "t" and "a" are hard to understand without looking at the function implementation, as well as other variables           | change to "title" and "author" etc.                                             | [[#119 & 161]] |
| 56-87      | Smaller, more focused functions | lots of various and processes that could be made into their own functions                                               | Split up each subprocess into its own function                                  | [[#56 - 87]]   |
| everywhere | DRY                             | comments are saying "what" not "why".                                                                                   | remove unnecessary comments, or change them to explain why things are happening |                |
# Revised Code
## 81-86
```java

```
## 50
```java

```
## 36 & 41
```Java
public void addBook(Book bookToAdd) {
	// add the book
	books.add(bookToAdd);
	
	// display all books in library for confirmation
	for (Book b : books) {
		System.out.println(b.title + " by " + b.author + " - Available: " + b.isAvailable);
	}
}
```
## 145
```Java
public void handIn() {
	isAvailable = true;
	borrower = null;
}
```
## 119 & 161
```java
public Book(String title, String author, int shelfNum, boolean isAvailable) {
	...
}

public EBook(String title, String author, int shelfNum, boolean isAvailable, String url) {
	...
}
```
## 56 - 87
```Java
public boolean doesBookExist(Book b){
	...
}

public boolean isBookAvailable(Book b){
	...
}

public void displayBorrowerConfirmation(Book b, Member m){
	System.out.println(b.title + " has been borrowed by " + m.name);
}

public void sendConfirmationEmail(Book b, Member m){
	notifier.sendEmail(m.email, "You borrowed: " + b.title);
}

public void doLoyaltyCheck(m){
	if (m.borrowedCount > 10) {
		m.isLoyaltyMember = true;
	}
}

public void borrowBook(String title, Member m) {
	Book b = findBook(title);
	if (!doesBookExist(b)){
		return;
	}
	
	if (!isBookAvailable(b)){
		return;
	}
	
	b.borrow(m);
	
	displayBorrowerConfirmation(b, m);
	sendConfirmationEmail(b, m);
	doLoyaltyCheck(m);
}
```