<h1>Clean Code</h1>

<h2>Significant names</h2>

<ul>
<li>Use names that reveal your purpose</li>

```
Tell about what your code do:

It is not a good ideia:

    public List<int[]> getThen(){
        List<int[]> list1 = new ArrayList<>();
        for (int[] x : theList){
            if (x[0] == 4){
                list1.add(x);
            }
            return list1;
        }
    }

Much better:

    public List<int[]> getFlaggedCells(){
        List<int[]> flaggedCells = new ArrayList<>();
        for (int[] cell : gameBoard){
            if (cell[STATUS_VALUE == FLAGGED] == 4){
                flaggedCells.add(cell);
            }
            return flaggedCells;
        }
    }
```


<li>Avoid wrong informations</li>

```
If you have a list of accounts

It is not a good ideia:

    List<Account> accountsList;

Much better:

    List<Account> accounts;
```

<li>Make meaningful distinctions</li>

```
Use names that you can distinct your attributes, classes, methods each other: 

It is not a good ideia:

    - getActiveAccount();
    - getActiveAccounts();
    - getActiveAccountInfo();


Much better:

    - getOnSingleAccount;
    - getOnSingleAccountDetails;
    - getOnAllAccounts;

*disclaimer: I don't know if this is the more correct but for now it is my best solution for this case in this exemple
```
<li>Use pronounceable names</li>

```
Use names that you can pronounce: 

It is not a good ideia:

    class DtaRcd102 {
        private Date genymdhms;
        private Date modymdhms;
        private final String pszqint = "102";
    }

Much better:
    class Customer {
        private Date generationTimestamp;
        private Date modificationTimestamp;
        private final String recordId = "102";
    }
```

<li>Use passive search names</li>

```
Use names that you can search along the code:

It is not a good ideia:

    for (int j = 0; j < 34; j++) {
        s += (t[j] * 4 / 5);
    }

Much better:

    int realDaysPerIdealDay = 4;
    const int WORK_DAYS_PEER_WEEK = 5;
    int sum = 0 ;

    for (int j = 0; j < NUMBER_OF_TAKS; j++){
        int realTaskDays = taskEstimate[j] * realDaysPerIdealDay;
        int realTaskWeeks = (realdays / WORK_DAYS_PEER_WEEK);
        sum += realtaskWeeks;
    }

*in this exemple, the number 5 it has been named WORK_DAYS_PEER_WEEK to make it easier in the text.

```
<li>Avoid scope's encodings in your code</li>

<li>Class names</li>
<p>Classes and objets must have names with substantive such as Customer, WikiPage, Account and AdressParser</p>

<li>Method names</li>
<p>Methods must ahve names with verbs such as Post, Payment, DeletePage or save</p>

<li>Selec one word by concept</li>
<p>Avoid to use Controller, Driver and Manager together in your code because diferentiate then can be hard</p>

</ul>


<h2>Functions</h2>


<ul>
<li>Try make small functions. If it have conditions block such as if, else and while, then must have only one line. And, the most important: functions must make only one thing</li>

<li></li>
</ul>

<h3>References</h3>
<p><a href="https://www.amazon.com.br/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882">Clean Code: A Handbook of Agile Software Craftsmanship</a> by Robert C. Martin</p>