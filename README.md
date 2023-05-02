Download Link: https://assignmentchef.com/product/solved-cmsc-203-lab-10-inheritance
<br>
<h1>Objectives</h1>

<ul>

 <li>Be able to derive a class from an existing class</li>

 <li>Be able to define a class hierarchy in which methods are overridden and fields are hidden</li>

 <li>Be able to use derived-class objects  Implement a copy constructor</li>

</ul>

<h1>Introduction</h1>

In this lab, you will be creating new classes that are derived from a class called BankAccount. A checking account <strong><em>is a </em></strong>bank account and a savings account <strong><em>is a </em></strong>bank account as well. This sets up a relationship called inheritance, where BankAccount is the superclass and CheckingAccount and SavingsAccount are subclasses. This relationship allows CheckingAccount to inherit attributes from BankAccount (like owner, balance, and accountNumber, but it can have new attributes that are specific to a checking account, like a fee for clearing a check. It also allows CheckingAccount to inherit methods from BankAccount, like deposit, that are universal for all bank accounts. You will write a withdraw method in CheckingAccount that overrides the withdraw method in BankAccount, in order to do something slightly different than the original withdraw method. You will use an instance variable called accountNumber in SavingsAccount to hide the accountNumber variable inherited from BankAccount.




The UML diagram for the inheritance relationship is as follows:







<h1>Task #1 Extending BankAccount</h1>

<ol>

 <li>Copy the files AccountDriver.java (code listing 10.1) and BankAccount.java (code listing</li>

</ol>

10.2) from Blackboard. BankAccount.java is complete and will not need to be modified.

<ol start="2">

 <li>Create a new class called <strong>CheckingAccount </strong>that <strong>extends BankAccount</strong>. It should contain a static constant <strong>FEE </strong>that represents the cost of clearing one check. Set it equal to 15 cents.</li>

 <li>Write a constructor that takes a name and an initial amount as parameters. It should call the constructor for the superclass. It should initialize accountNumber to be the current value in accountNumber concatenated with –10 (All checking accounts at this bank are identified by the extension –10). There can be only one checking account for each account number. Remember since accountNumber is a private member in BankAccount, it must be changed through a mutator method.</li>

 <li>Write a new instance method, <strong>withdraw</strong>, that overrides the withdraw method in the superclass. This method should take the amount to withdraw, add to it the fee for check clearing, and call the withdraw method from the superclass. Remember that to override the method, it must have the same method heading. Notice that the withdraw method from the superclass returns true or false depending if it was able to complete the withdrawal or not. The method that overrides it must also return the same true or false that was returned from the call to the withdraw method from the superclass.</li>

 <li>Compile and debug this class.</li>

</ol>

<strong> </strong>

<h1>Task #2 Creating a Second Subclass</h1>

<ol>

 <li>Create a new class called <strong>SavingsAccount </strong>that <strong>extends BankAccount. </strong>

  <ol start="2">

   <li>It should contain an instance variable called <strong>rate </strong>that represents the annual interest rate. Set it equal to 2.5%.</li>

   <li>It should also have an instance variable called <strong>savingsNumber, </strong>initialized to 0. In this bank, you have one account number, but can have several savings accounts with that same number. Each individual savings account is identified by the number following a dash. For example, 100001-0 is the first savings account you open, 100001-1 would be another savings account that is still part of your same account. This is so that you can keep some funds separate from the others, like a Christmas club account.</li>

   <li>An instance variable called <strong>accountNumber </strong>that will hide the accountNumber from the superclass, should also be in this class.</li>

  </ol></li>

 <li>Write a constructor that takes a name and an initial balance as parameters and calls the constructor for the superclass. It should initialize accountNumber to be the current value in the superclass accountNumber (the hidden instance variable) concatenated with a</li>

</ol>

hyphen and then the savingsNumber.

<ol start="3">

 <li>Write a method called <strong>postInterest </strong>that has no parameters and returns no value. This method will calculate one month’s worth of interest on the balance and deposit it into the account.</li>

 <li>Write a method that overrides the <strong>getAccountNumber </strong>method in the superclass.</li>

 <li>Write a copy constructor that creates another savings account for the same person. It should take the original savings account and an initial balance as parameters. It should call the copy constructor of the superclass, assign the savingsNumber to be one more than the savingsNumber of the original savings account. It should assign the accountNumber</li>

</ol>

to be the accountNumber of the superclass concatenated with the hypen and the savingsNumber of the new account.

<ol start="6">

 <li>Compile and debug this class.</li>

 <li>Use the AccountDriver class to test out your classes. If you named and created your classes and methods correctly, it should not have any difficulties. If you have errors, do not edit the AccountDriver class. You must make your classes work with this program.</li>

 <li>Running the program should give the following output:</li>

</ol>




Account Number 100001-10 belonging to Benjamin Franklin

Initial balance = $1000.00

After deposit of $500.00, balance = $1500.00

After withdrawal of $1000.00, balance = $499.85

Account Number 100002-0 belonging to William Shakespeare

Initial balance = $400.00

After deposit of $500.00, balance = $900.00

Insuffient funds to withdraw $1000.00, balance = $900.00

After monthly interest has been posted, balance = $901.88

Account Number 100002-1 belonging to William Shakespeare

Initial balance = $5.00

After deposit of $500.00, balance = $505.00

Insuffient funds to withdraw $1000.00, balance = $505.00

Account Number 100003-10 belonging to Isaac Newton

<strong>           </strong>

<h1>Code Listing 10.1 (AccountDriver.java)</h1>

<strong>import</strong> java.text.*;               // to use Decimal Format

//Demonstrates the BankAccount and derived classes <strong>public</strong> <strong>class</strong> AccountDriver

{

<strong>public</strong> <strong>static</strong> <strong>void</strong> main(String[] args)

{

<strong>double</strong> put_in = 500;        <strong>double</strong> take_out = 1000;




DecimalFormat myFormat;

String money;

String money_in;           String money_out;

<strong>boolean</strong> completed;




// to get 2 decimals every time

myFormat = <strong>new</strong> DecimalFormat(“#.00”);




//to test the Checking Account class   CheckingAccount myCheckingAccount =

<strong>new</strong> CheckingAccount (“Benjamin Franklin”, 1000);

System.<strong><em>out</em></strong>.println (“Account Number ”

+ myCheckingAccount.getAccountNumber() +    ” belonging to ” + myCheckingAccount.getOwner());   money  = myFormat.format(myCheckingAccount.getBalance());   System.<strong><em>out</em></strong>.println (“Initial balance = $” + money);

myCheckingAccount.deposit (put_in);   money_in = myFormat.format(put_in);   money  = myFormat.format(myCheckingAccount.getBalance());

System.<strong><em>out</em></strong>.println (“After deposit of $” + money_in

+ “,  balance = $” + money);

completed = myCheckingAccount.withdraw(take_out);         money_out = myFormat.format(take_out);

money  = myFormat.format(myCheckingAccount.getBalance());

<strong>if</strong> (completed)

{

System.<strong><em>out</em></strong>.println (“After withdrawal of $” + money_out

+ “,  balance = $” + money);

}

<strong>else</strong>

{

System.<strong><em>out</em></strong>.println (“Insuffient funds to withdraw $”

+ money_out + “,  balance = $” + money);

}

System.<strong><em>out</em></strong>.println();




//to test the savings account class   SavingsAccount yourAccount =

<strong>new</strong> SavingsAccount (“William Shakespeare”, 400);

System.<strong><em>out</em></strong>.println (“Account Number ”

+ yourAccount.getAccountNumber() +     ” belonging to ” + yourAccount.getOwner());   money  = myFormat.format(yourAccount.getBalance());         System.<strong><em>out</em></strong>.println (“Initial balance = $” + money);

yourAccount.deposit (put_in);   money_in = myFormat.format(put_in);   money  = myFormat.format(yourAccount.getBalance());   System.<strong><em>out</em></strong>.println (“After deposit of $” + money_in

+ “,  balance = $” + money);

completed = yourAccount.withdraw(take_out);   money_out = myFormat.format(take_out);   money  = myFormat.format(yourAccount.getBalance());

<strong>if</strong> (completed)

{

System.<strong><em>out</em></strong>.println (“After withdrawal of $” + money_out

+ “,  balance = $” + money);

}

<strong>else</strong>

{

System.<strong><em>out</em></strong>.println (“Insuffient funds to withdraw $”

+ money_out + “,  balance = $” + money);

}

yourAccount.postInterest();

money  = myFormat.format(yourAccount.getBalance());   System.<strong><em>out</em></strong>.println (“After monthly interest has been posted,”

+ “balance = $”     + money);

System.<strong><em>out</em></strong>.println();







// to test the copy constructor of the savings account class

SavingsAccount secondAccount =

<strong>new</strong> SavingsAccount (yourAccount,5);

System.<strong><em>out</em></strong>.println (“Account Number ”

+ secondAccount.getAccountNumber()+     ” belonging to ” + secondAccount.getOwner());   money  = myFormat.format(secondAccount.getBalance());   System.<strong><em>out</em></strong>.println (“Initial balance = $” + money);

secondAccount.deposit (put_in);   money_in = myFormat.format(put_in);   money  = myFormat.format(secondAccount.getBalance());

System.<strong><em>out</em></strong>.println (“After deposit of $” + money_in

+ “, balance = $” + money);

secondAccount.withdraw(take_out);   money_out = myFormat.format(take_out);   money  = myFormat.format(secondAccount.getBalance());

<strong>if</strong> (completed)

{

System.<strong><em>out</em></strong>.println (“After withdrawal of $” + money_out

+ “,  balance = $” + money);

}

<strong>else</strong>

{

System.<strong><em>out</em></strong>.println (“Insuffient funds to withdraw $”

+ money_out + “,  balance = $” + money);

}

System.<strong><em>out</em></strong>.println();




//to test to make sure new accounts are numbered correctly          CheckingAccount yourCheckingAccount =

<strong>new</strong> CheckingAccount (“Issac Newton”, 5000);   System.<strong><em>out</em></strong>.println (“Account Number ”

+ yourCheckingAccount.getAccountNumber()

+ ” belonging to ”

+ yourCheckingAccount.getOwner());




}

}

<h1>Code Listing 10.2 (BankAccount.java)</h1>

/**Defines any type of bank account*/ <strong>public</strong> <strong>abstract</strong> <strong>class</strong> BankAccount

{

/**class variable so that each account has a unique number*/      <strong>protected</strong> <strong>static</strong> <strong>int</strong> <em>numberOfAccounts</em> = 100001;




/**current balance in the account*/    <strong>private</strong> <strong>double</strong> balance;     /** name on the account*/  <strong>private</strong> String owner;

/** number bank uses to identify account*/    <strong>private</strong> String accountNumber;




/**default constructor*/  <strong>public</strong> BankAccount()

{

balance = 0;

accountNumber = <em>numberOfAccounts</em> + “”;

<em>numberOfAccounts</em>++;

}




/**standard constructor

<strong>@param</strong> name the owner of the account   <strong>@param</strong> amount the beginning balance*/       <strong>public</strong> BankAccount(String name, <strong>double</strong> amount)

{

owner = name;

balance = amount;

accountNumber = <em>numberOfAccounts</em> + “”;

<em>numberOfAccounts</em>++;

}




/**copy constructor creates another account for the same owner

<strong>@param</strong> oldAccount the account with information to copy     <strong>@param</strong> the beginning balance of the new account*/    <strong>public</strong> BankAccount(BankAccount oldAccount, <strong>double</strong> amount)

{

owner = oldAccount.owner;          balance = amount;

accountNumber = oldAccount.accountNumber;

}




/**allows you to add money to the account     <strong>@param</strong> amount the amount to deposit in the account*/     <strong>public</strong> <strong>void</strong> deposit(<strong>double</strong> amount)

{

balance = balance + amount;

}




/**allows you to remove money from the account if   enough money is available,returns true if the transaction was        completed, returns false if the there was not enough money.     <strong>@param</strong> amount  the amount to withdraw from the account    <strong>@return</strong> true if there was sufficient funds to complete   the transaction, false otherwise*/     <strong>public</strong> <strong>boolean</strong> withdraw(<strong>double</strong> amount)

{

<strong>boolean</strong> completed = <strong>true</strong>;




<strong>if</strong> (amount &lt;= balance)

{

balance = balance – amount;

}

<strong>else</strong>

{

completed = <strong>false</strong>;

}

<strong>return</strong> completed;

}




/**<u>accessor</u> method to balance    <strong>@return</strong> the balance of the account*/

<strong>public</strong> <strong>double</strong> getBalance()

{

<strong>return</strong> balance;

}




/**<u>accessor</u> method to owner      <strong>@return</strong> the owner of the account*/

<strong>public</strong> String getOwner()

{

<strong>return</strong> owner;

}




/**<u>accessor</u> method to account number   <strong>@return</strong> the account number*/

<strong>public</strong> String getAccountNumber()

{

<strong>return</strong> accountNumber;

}




/**mutator method to change the balance       <strong>@param</strong> newBalance the new balance for the account*/

<strong>public</strong> <strong>void</strong> setBalance(<strong>double</strong> newBalance)

{

balance = newBalance;

}




/**mutator method to change the account number       <strong>@param</strong> newAccountNumber the new account number*/

<strong>public</strong> <strong>void</strong> setAccountNumber(String newAccountNumber)

{

accountNumber = newAccountNumber;

}

}