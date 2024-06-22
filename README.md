<<<<<<< HEAD
<!--
    README.md in branch D12-Datamodel
 -->

# Aufgabe D12: _Datamodel_

The assignment completes the datamodel with classes _Article.java_, _Order.java_
and _OrderItem.java_ classes. _Customer.java_ already exists from the previous
assignment. In addition, two _enum_ are used in the data model:
_Currency.java_ amd _TAX.java_.

The data model is (UML Class Diagram, see also StarUML-file:
[Datamodel.mdj](src/datamodel/Datamodel.mdj)
):

<img src="src/datamodel/Datamodel.png" alt="drawing" width="800"/>

Content:

- [Setup](#1-setup) - Fetching Branches and Sourcing the Project

  - branch: [C12-Customer](https://github.com/sgra64/se1.bestellsystem/tree/C12-Customer),
  - branch: [D12-Datamodel](https://github.com/sgra64/se1.bestellsystem/tree/D12-Datamodel).

- [D1: Completing the Datamodel](#d1-completing-the-datamodel)

  - Datamodel Generation and Completion
  - Building and Running the Application
  - Running JUnit Tests
  - Code Coverage Reports
  - Javadoc for Complete Datamodel

- [D2: Completing Features](#d2-completing-features)

  - New Articles, Customers and Orders (steps 1-3)
  - _find()_ - method (step 4)
  - _printOrder()_ - method (steps 5)
  - order value and tax calculations (steps 6-9)

- [Release Preparation](#release-preparation)
  - Packaging the Application
  - Running the packaged Application

&nbsp;

## 1. Setup

Merge files from the distribution branch
[D12-Datamodel](https://github.com/sgra64/se1.bestellsystem/tree/D12-Datamodel)
into project `se1.bestellsystem`.

Setup assumes the project is under `git` control. Initialize `git`
if this is not yet the case (skip step: `git init` otherwise).

```sh
cd se1.bestellsystem            # change into project directory

[ -d .git ] || git init         # initialize git, if project is not yet under git control

# add link named 'se1-origin' pointing to the remote distribution repository
git remote add se1-origin https://github.com/sgra64/se1.bestellsystem.git

# fetch branch D12-Datamodel from the remote repository
git fetch se1-origin D12-Datamodel

# merge content of fetched branch into current branch
git merge --allow-unrelated-histories --strategy-option theirs FETCH_HEAD
```

Files that came with the merge of the branch:

```sh
find src tests
```

```
src
src/application
src/application/Application.java
src/application/Application_D1.java
src/application/package-info.java
src/application/Runtime.java
src/datamodel
src/datamodel/Datamodel.mdj
src/datamodel/Datamodel.png
src/datamodel/package-info.java
src/module-info.java
tests/
tests/application
tests/application/Application_0_always_pass_Tests.java
tests/datamodel
tests/datamodel/Article_100_Constructor_Tests.java
tests/datamodel/Article_200_SetId_Tests.java
tests/datamodel/Article_300_Description_Tests.java
tests/datamodel/Article_400_UnitPrice_Tests.java
tests/datamodel/Article_500_Currency_Tests.java
tests/datamodel/Article_600_TAX_Tests.java
tests/datamodel/Order_100_Constructor_Tests.java
tests/datamodel/Order_200_SetId_Tests.java
tests/datamodel/Order_300_CreationDate_Tests.java
tests/datamodel/Order_400_OrderItems_Tests.java
```

Customer-tests from branch
[C12-Customer](https://github.com/sgra64/se1.bestellsystem/tree/C12-Customer)
might be missing. Obtain them from the branch:

```sh
# fetch branch C12-Customer from the remote repository and create local branch
# git fetch <remote> <rbranch>:<lbranch>
git fetch se1-origin C12-Customer:C12-Customer

# set new local branch C12-Customer to track remote branch C12-Customer
git branch --set-upstream-to=se1-origin/C12-Customer C12-Customer

# show branches
git branch -avv
```

<img src="https://github.com/sgra64/se1.bestellsystem/blob/markup/D12-Datamodel/D1_setup_branches.png?raw=true" alt="drawing" width="800"/>

&nbsp;

Content of branch `C12-Customer` can now be merged into branch `D12-Datamodel`
to complete files missing from that branch:

```sh
# merge fetched branch into current branch without touching existing files
git merge --allow-unrelated-histories --strategy-option ours C12-Customer
```

As result, tests for _Articles_, _Orders_ (from branch `D12-Datamodel`)
and tests for _Customers_ (merged from branch `C12-Customer`) should show:

```sh
find tests
```

```
tests
tests/application
tests/application/Application_0_always_pass_Tests.java
tests/datamodel
tests/datamodel/Article_100_Constructor_Tests.java
tests/datamodel/Article_200_SetId_Tests.java
tests/datamodel/Article_300_Description_Tests.java
tests/datamodel/Article_400_UnitPrice_Tests.java
tests/datamodel/Article_500_Currency_Tests.java
tests/datamodel/Article_600_TAX_Tests.java
tests/datamodel/Customer_100_Constructor_Tests.java
tests/datamodel/Customer_200_SetId_Tests.java
tests/datamodel/Customer_300_SetName_Tests.java
tests/datamodel/Customer_400_Contacts_Tests.java
tests/datamodel/Customer_500_SetNameExtended_Tests.java
tests/datamodel/Order_100_Constructor_Tests.java
tests/datamodel/Order_200_SetId_Tests.java
tests/datamodel/Order_300_CreationDate_Tests.java
tests/datamodel/Order_400_OrderItems_Tests.java
```

The project can now be sourced to set the project environment:

```sh
source .env/setenv.sh           # source project
```

&nbsp;

## D1: Completing the Datamodel

- D1.a - [Datamodel Generation and Completion](#d1a-datamodel-generation-and-completion)

- D1.b - [Building and Running the Application](#d1b-building-and-running-the-application)

- D1.c - [Running JUnit Tests](#d1c-running-junit-tests)

- D1.d - [Code Coverage Report](#d1d-code-coverage-report)

- D1.e - [Javadoc for Complete Datamodel](#d1e-javadoc-for-complete-datamodel)

&nbsp;

### D1.a Datamodel Generation and Completion

File
[src/datamodel/Datamodel.mdj](src/datamodel/Datamodel.mdj)
contains UML model of the `datamodel` classes.

You should have a completed class `Customer.java` from the previous
assignment. Keep it.

Open with _StarUML_ and extract classes from the UML-Model:

- Tools -> Java -> Generate Code -> select _"datamodel"_ -> OK

- select folder to save datamodel classes

- make sure, datamodel classes arrive in `src/datamodel` and `Customer.java` remains unchanged.

Classes in `src/datamodel` should now be present:

```sh
find src/datamodel
```

```
src/datamodel
src/datamodel/Article.java
src/datamodel/Currency.java
src/datamodel/Customer.java
src/datamodel/Datamodel.mdj         <-- UML model (StarUML) of datamodel
src/datamodel/Datamodel.png         <-- UML class diagram of datamodel classes
src/datamodel/Order.java
src/datamodel/OrderItem.java
src/datamodel/package-info.java
src/datamodel/TAX.java
src/module-info.java
```

You may remove the `.mdj` and `.png` files.

Adjust `src/datamodel` classes to compile.

```sh
mk compile
```

```
javac $(find src -name '*.java') -d bin/classes; \
copy resources bin/resources
done.
```

Complete methods in classes according to javadocs:

- `Article.java`,

- `Order.java` and

- `OrderItem.java`.

&nbsp;

### D1.b Building and Running the Application

After completion of classes, run the application:

```sh
mk compile
```

The application
[Application_D1.java](src/application/Application_D1.java)

shows the folloring output:

```
java application.Application
Hello, Application_D1
(5) Customer objects built.
(6) Article objects built.
(4) Order objects built.
---
(+0) Customer objects added.
(+0) Article objects added.
(+0) Order objects added.
---
Kunden:
+----------+----------------------------+--------------------------------------+
| Kund.-ID | Name                       | Kontakt                              |
+----------+----------------------------+--------------------------------------+
|   892474 | Meyer, Eric                | eric98@yahoo.com, (+1 contacts)      |
|   643270 | Bayer, Anne                | anne24@yahoo.de, (+2 contacts)       |
|   286516 | Schulz-Mueller, Tim        | tim2346@gmx.de                       |
|   412396 | Blumenfeld, Nadine-Ulla    | +49 152-92454                        |
|   456454 | Abdelalim, Khaled Saad Moha| +49 1524-12948210                    |
+----------+----------------------------+--------------------------------------+

Artikel:
+----------+----------------------------+---------------+----------------------+
|Artikel-ID| Beschreibung               |      Preis CUR|  Mehrwertsteuersatz  |
+----------+----------------------------+---------------+----------------------+
|SKU-458362| Tasse                      |       2.99 EUR|  19.0% GER_VAT       |
|SKU-693856| Becher                     |       1.49 EUR|  19.0% GER_VAT       |
|SKU-518957| Kanne                      |      19.99 EUR|  19.0% GER_VAT       |
|SKU-638035| Teller                     |       6.49 EUR|  19.0% GER_VAT       |
|SKU-278530| Buch "Java"                |      49.90 EUR|   7.0% GER_VAT_REDU  |
|SKU-425378| Buch "OOP"                 |      79.95 EUR|   7.0% GER_VAT_REDU  |
+----------+----------------------------+---------------+----------------------+

=======
## Branch Integration: *feat.730-json-data*

Branch *feat.730-json-data* enables a new feature to load data-objects (*Customer*, *Article*
and *Orders*) from *JSON files* replacing object creation in
[Application_F1.java](https://github.com/sgra64/se1.bestellsystem/blob/F12-Refactoring/src/application/Application_F1.java)
(before version).

The updated file (after integration of branch *feat.730-json-data*) will no longer
contain object creations:
[Application_F1.java](src/application/Application_F1.java)
(after version).

Instead, data will be obtained from JSON files in the new
[data](data) directory.

JSON file [data/customers.json](data/customers.json) contains *Customer* data:

```json
[
  {"id": 892474, "name": "Eric Meyer", "contacts": ["eric98@yahoo.com", "(030) 3945-642298"] },
  {"id": 643270, "name": "Bayer, Anne", "contacts": ["anne24@yahoo.de", "(030) 3481-23352", "fax: (030)23451356"] },
  {"id": 286516, "name": "Tim Schulz-Mueller", "contacts": ["tim2346@gmx.de"] },
  {"id": 412396, "name": "Nadine-Ulla Blumenfeld", "contacts": ["+49 152-92454"] },
  {"id": 456454, "name": "Khaled Saad Mohamed Abdelalim", "contacts": ["+49 1524-12948210"] },
  {"id": 651286, "name": "Lena Neumann", "contacts": ["lena228@gmail.com"] }
]
```

JSON file [data/articles.json](data/articles.json) contains *Article* data:

```json
[
  {"id": "SKU-458362", "description": "Tasse", "price": 299 },
  {"id": "SKU-693856", "description": "Becher", "price": 149 },
  {"id": "SKU-518957", "description": "Kanne", "price": 1999 },
  {"id": "SKU-638035", "description": "Teller", "price": 649 },
  {"id": "SKU-278530", "description": "Buch \"Java\"", "price": 4990, "tax": "reduced" },
  {"id": "SKU-425378", "description": "Buch \"OOP\"", "price": 7995, "tax": "reduced" },

  {"id": "SKU-300926", "description": "Pfanne", "price": 4999 },
  {"id": "SKU-663942", "description": "Fahrradhelm", "price": 16900 },
  {"id": "SKU-583978", "description": "Fahrradkarte", "price": 695, "tax": "reduced" }
]
```

JSON file [data/orders.json](data/orders.json) contains *Orders* data:

```json
[
  {"id": 8592356245, "customer_id": 892474, "items": [
    {"article_id": "SKU-638035", "units": 4 },
    {"article_id": "SKU-693856", "units": 8 },
    {"article_id": "SKU-425378", "units": 1 },
    {"article_id": "SKU-458362", "units": 4 }
  ]},

  {"id": 3563561357, "customer_id": 643270, "items": [
    {"article_id": "SKU-638035", "units": 2 },
    {"article_id": "SKU-458362", "units": 2 }
  ]},
  /* ... */
]
```

The branch contains a *code-drop* of new and modified files that enable the feature:

```
A       data/articles.json                          <-- new file (A: added)
A       data/articles_price_update.json             <-- new
A       data/customers.json                         <-- new
A       data/orders.json                            <-- new
M       resources/application.properties            <-- modified file (M: modified)
M       src/application/Application_F1.java         <-- modified
M       src/module-info.java                        <-- modified
A       src/system/impl/DataFactories.java          <-- new
M       src/system/impl/DataStoreImpl.java          <-- modified
M       src/system/impl/IoC_Impl.java               <-- modified
A       src/system/impl/JSONDataFactories.java      <-- new
A       src/system/impl/JSONRepositoryImpl.java     <-- new
```

Base of the *code-drop* is the state of the development after completing
[F12-Refactoring](https://github.com/sgra64/se1.bestellsystem/tree/F12-Refactoring)


&nbsp;

## Steps

Refer to `F12-Refactoring`
[setup](https://github.com/sgra64/se1.bestellsystem/tree/F12-Refactoring#setup)
for completing some of the steps below (e.g. for adding remotes, fetching
branches or setting up local tracking branches).

1. Make sure, code from completed assignment `F12-Refactoring` compiles
    and JUnit tests pass.

1. Create a new integration branch: `int.feat.730-json-data`*` at the last
    commit of the completed (working) `F12-Refactoring`.
    The integration branch will contain this code.

1. Fetch branch `feat.730-json-data` from a new downstream repository where
    another team develops its features: `https://github.com/sgra64/se1-dev.git`.

1. Create a local tracking branch `feat.730-json-data` for the fetched remote
    branch.

    ```sh
    git branch -u se1-dev/feat.730-json-data feat.730-json-data
    ```

1. Merge the feature from the tracking branch into the integration branch
    (containing the previous state of `F12-Refactoring`):

    ```sh
    # switch to integration branch
    git switch int.feat.730-json-data

    # merge branch feat.730-json-data into integration branch
    git merge --allow-unrelated-histories feat.730-json-data
    ```

    - The Merge will cause *merge conflicts*.

    - Open an affected file in *VSCode* and navigate to the conflict
        (*VSCode* highlights conflicts).
        
    - Resolve the conflict (usually by accepting *Incoming Changes*)

    - The merge remains *open* while all conflicts are being resolved.

    - The Merge is *finalized* and *closed* by either:

        - aborting the merge and removing all changes: `merge --abort` or by

        - committing the merge: `git add .`
            and `git commit -m "merge commit feat.730-json-data"`

        Commit the merge only when the program works and all JUnit Tests pass!

1. After integration has completed on the integration branch,
    merge it back to your main development branch (where the integration
    branch was created).

    This merge will be a `fast-forward` merge since no other changes have
    occured on the main branch. No conflicts will occur.

    The main development branch now has the feature integrated and
    development can continue.

1. Draw branches and commits for the integration.

1. Push commits with the integration to your remote main development branch.


&nbsp;

## Validation

Switch to your main development branch, build and run the program:

```sh
mk clean compile compile-tests run-tests
```
```
[       121 tests successful      ]     <-- 121 tests passed
[         0 tests failed          ]
```

Run the program:

```sh
mk run
```
```
>>>>>>> feat.730-json-data
Bestellungen:
+----------+--------------------------------------------+----------------------+
|Bestell-ID| Bestellungen             MwSt*        Preis|     MwSt       Gesamt|
+----------+--------------------------------------------+----------------------+
<<<<<<< HEAD
|id        | name                     0.00*     0.00 EUR|     0.00     0.00 EUR|
+----------+--------------------------------------------+----------------------+
|id        | name                     0.00*     0.00 EUR|     0.00     0.00 EUR|
+----------+--------------------------------------------+----------------------+
|id        | name                     0.00*     0.00 EUR|     0.00     0.00 EUR|
+----------+--------------------------------------------+----------------------+
|id        | name                     0.00*     0.00 EUR|     0.00     0.00 EUR|
+----------+--------------------------------------------+----------------------+
                                                 Gesamt:|     0.00     0.00 EUR|
                                                        +======================+
done.
```

&nbsp;

### D1.c Running JUnit Tests

JUnit-tests for class `Customer.java` should pass from the previous assignment.

```sh
java -jar branches/libs/libs/junit-platform-console-standalone-1.9.2.jar \
    $(eval echo $JUNIT_OPTIONS) \
    -c application.Application_0_always_pass_Tests \
    -c datamodel.Customer_100_Constructor_Tests \
    -c datamodel.Customer_200_SetId_Tests \
    -c datamodel.Customer_300_SetName_Tests \
    -c datamodel.Customer_400_Contacts_Tests \
    -c datamodel.Customer_500_SetNameExtended_Tests
```

Output:

```
├─ JUnit Jupiter ✔
│  └─ Application_0_always_pass_Tests ✔
│     ├─ test_001_always_pass() ✔
│     └─ test_002_always_pass() ✔
|  ...
|
├─ JUnit Vintage ✔
└─ JUnit Platform Suite ✔

Test run finished after 142 ms
[        55 tests successful      ]   <-- 55 tests successful
[         0 tests failed          ]   <--  0 tests failed
done.
```

Add tests for classes `Article.java` and `Order.java` one after another
to verify they are passing with your implementation of classes. Fix failures.

```
  - datamodel.Article_100_Constructor_Tests
  - datamodel.Article_200_SetId_Tests
  - datamodel.Article_300_Description_Tests
  - datamodel.Article_400_UnitPrice_Tests
  - datamodel.Article_500_Currency_Tests
  - datamodel.Article_600_TAX_Tests
  - datamodel.Order_100_Constructor_Tests
  - datamodel.Order_200_SetId_Tests
  - datamodel.Order_300_CreationDate_Tests
  - datamodel.Order_400_OrderItems_Tests
```

The full test-suite of _Customer_ tests runs

```sh
mk run-tests
```

Output:

```
├─ JUnit Jupiter ✔
│  └─ Application_0_always_pass_Tests ✔
│     ├─ test_001_always_pass() ✔
│     └─ test_002_always_pass() ✔
|  ...
|
├─ JUnit Vintage ✔
└─ JUnit Platform Suite ✔

Test run finished after 142 ms
[       102 tests successful      ]   <-- 102 tests successful
[         0 tests failed          ]   <--   0 tests failed
done.
```

Remove tests that are failing.

Run JUnit-Tests also in your IDE.

&nbsp;

### D1.d Code Coverage Report

<!--
https://stackoverflow.com/questions/17973067/how-to-use-jacoco-exec-report
https://stackoverflow.com/questions/40810496/jacoco-report-in-command-line

Jacoco agent and CLI:
- https://www.jacoco.org/jacoco/trunk/doc/agent.html
- https://www.jacoco.org/jacoco/trunk/doc/cli.html
-->

[**Code Coverage**](https://en.wikipedia.org/wiki/Code_coverage)
is a **metric of code quality** defined by the ratio of instructions executed
during JUnit tests and the total number of instructions in the code base.

When JUnit tests run, tested code (_"units-under-test"_) is exercised.
Depending on breath and detail tested in JUnit tests, more code is exercised.

_Code Coverage_ of, e.g. 72% means that during execution of JUnit tests, 72% of
instructions in tested code were executed at least once (_covered_) - 28% were
not (_not covered_).

Covering code does not mean it is correct - it simply means, it was executed
during JUnit tests while uncovered code was not.

In order to obtain coverage, specialized
[Code Coverage Tools](https://en.wikipedia.org/wiki/Java_code_coverage_tools)
are used that exist for all programming languages such as
[_Jacoco_](https://www.jacoco.org) for _Java_,
[_Istanbul_](https://istanbul.js.org) for _JavaScript_ or
[_Coverage.py_](https://coverage.readthedocs.io) for _Python_).

Obtaining code coverage consists of two steps (for _Jacoco_):

1. _Recording_ the execution of JUnit tests by the
   [Jacoco-Agent](https://www.jacoco.org/jacoco/trunk/doc/agent.html).
   The result of the recording is a file: `jacoco.exec` in a new directory
   in the project: `coverage`.

1. Generation of a _Coverage Report_ for relevant classes
   (coverage of test-classes is not relevant, only for tested classes).
   Reports are generated by a command using the
   [Jacoco Command Line Interface](https://www.jacoco.org/jacoco/trunk/doc/cli.html)
   (CLI).

   The report is generated as _HTML_ (it can also be generated in other formats
   such as _.csv_ or _.xml_ for further processing).

_Jacoco_ .jar files are present in the `libs` directory:

- `jacocoagent.jar` -- agent for recording the execution of instructions during
  JUnit tests.

- `jacococli.jar` -- for report generation.

Step 1:

(update [.env/setenv.sh](https://github.com/sgra64/se1.bestellsystem/blob/main/.env/setenv.sh)
in order to get the code coverage commands)

```sh
source .env/setenv.sh           # source the project
show --all                      # show all available commands
```

Output includes code-coverage commands:

```
run-tests:
  java -jar ../libs/libs/junit-platform-console-standalone-1.9.2.jar \
    $(eval echo $JUNIT_OPTIONS) --scan-class-path

coverage:
  java $(eval echo $JACOCO_AGENT) \
    -jar ../libs/libs/junit-platform-console-standalone-1.9.2.jar \
    $(eval echo $JUNIT_OPTIONS) --scan-class-path; \
    echo coverage events recorded in: coverage/jacoco.exec

coverage-report:
  coverage_report; [ -f coverage/index.html ] && \
    echo coverage report created in: coverage/index.html
```

Run JUnit tests, either all with `--scan-class-path` or selectively those
tests that are passing:

```sh
# run all tests (using: --scan-class-path)
mk run-tests

# run tests selectively (only include tests that are passing)
java -jar ../libs/libs/junit-platform-console-standalone-1.9.2.jar \
    $(eval echo $JUNIT_OPTIONS) \
    -c application.Application_0_always_pass_Tests \
    -c datamodel.Customer_100_Constructor_Tests \
    -c datamodel.Customer_200_SetId_Tests \
    -c datamodel.Customer_300_SetName_Tests \
    -c datamodel.Customer_400_Contacts_Tests \
    -c datamodel.Customer_500_SetNameExtended_Tests
```

Output:

```
Test run finished after 142 ms
[       102 tests successful      ]   <-- 102 tests successful (or fewer for fewer tests)
[         0 tests failed          ]   <--   0 tests failed
done.
```

Run the first stage of recording code coverage events:

```sh
# run all tests (using: --scan-class-path)
mk coverage

# run tests with JACOCO_AGENT selectively (only include tests that are passing)
java $(eval echo $JACOCO_AGENT) \
    -jar ../libs/libs/junit-platform-console-standalone-1.9.2.jar \
    $(eval echo $JUNIT_OPTIONS) \
    -c application.Application_0_always_pass_Tests \
    -c datamodel.Customer_100_Constructor_Tests \
    -c datamodel.Customer_200_SetId_Tests \
    -c datamodel.Customer_300_SetName_Tests \
    -c datamodel.Customer_400_Contacts_Tests \
    -c datamodel.Customer_500_SetNameExtended_Tests
```

JUnit tests execute again, but now with the ``recording.
The result is created in a new file`jacoco.exec`in a new directory`coverage`
in the project directory:

```sh
ls -la coverage
```

```
total 40
drwxr-xr-x 1 svgr2 Kein     0 May 25 17:13 .
drwxr-xr-x 1 svgr2 Kein     0 May 25 17:13 ..
-rw-r--r-- 1 svgr2 Kein 34172 May 25 17:13 jacoco.exec
```

Step 2:

A _code coverage report_ is created from the recording of JUnit test execution.

Classes to analyze are specified by a variable:

```sh
# copy into terminal to define the variable
analyze_classes=(
    --classfiles ./bin/classes/datamodel/Article.class
    --classfiles ./bin/classes/datamodel/Currency.class
    --classfiles ./bin/classes/datamodel/Customer.class
    --classfiles ./bin/classes/datamodel/Datamodel.mdj
    --classfiles ./bin/classes/datamodel/Datamodel.png
    --classfiles ./bin/classes/datamodel/Order.class
    --classfiles ./bin/classes/datamodel/OrderItem.class
    --classfiles ./bin/classes/datamodel/TAX.class
)
```

Based on this definition and the recording, the _code coverage report_ can be created.

```sh
mk coverage-report
```

Output:

```
[INFO] Loading execution data file .../se1.bestellsystem/coverage/jacoco.exec.
[INFO] Analyzing 6 classes.
coverage report created in: coverage/index.html
done.
```

Open the report in a browser `coverage/index.html`.

For package `datamodel`, a _code coverage_ of 95% was achieved by executing
all JUnit tests.

<img src="https://github.com/sgra64/se1.bestellsystem/blob/markup/D12-Datamodel/D1_coverage_1.png?raw=true" alt="drawing" width="800"/>

&nbsp;

Opening the `datamodel` reveals more detail about coverages of classes from this package:

<img src="https://github.com/sgra64/se1.bestellsystem/blob/markup/D12-Datamodel/D1_coverage_2.png?raw=true" alt="drawing" width="800"/>

&nbsp;

Inside the `Customer` class coverages of methods are shown:

<img src="https://github.com/sgra64/se1.bestellsystem/blob/markup/D12-Datamodel/D1_coverage_3.png?raw=true" alt="drawing" width="800"/>

&nbsp;

Finally, coverage of the `addContact()` method in class `Customer` can be inspected.

- Green lines show instructions that were exercised at least once during JUnit tests.

- Red lines show instructions that were not.

- Yellow lines show partial executions where one part of the line was exercised and
  the other was not.

<img src="https://github.com/sgra64/se1.bestellsystem/blob/markup/D12-Datamodel/D1_coverage_Customer.png?raw=true" alt="drawing" width="800"/>

&nbsp;

[Full coverage reports](https://sgra64.github.io/se1.bestellsystem/D12-Datamodel/coverage)
exist for all for classes:

- _Customer.java_ - ([coverage report](https://sgra64.github.io/se1.bestellsystem/D12-Datamodel/coverage/datamodel/Customer.java.html#L1)),

- _Article.java_ - ([coverage report](https://sgra64.github.io/se1.bestellsystem/D12-Datamodel/coverage/datamodel/Article.java.html#L1)),

- _Order.java_ - ([coverage report](https://sgra64.github.io/se1.bestellsystem/D12-Datamodel/coverage/datamodel/Order.java.html#L1)),

- _OrderItem.java_ - ([coverage report](https://sgra64.github.io/se1.bestellsystem/D12-Datamodel/coverage/datamodel/OrderItem.java.html#L1)),

- _Currency.java_ - ([coverage report](https://sgra64.github.io/se1.bestellsystem/D12-Datamodel/coverage/datamodel/Currency.java.html#L1)),

- _TAX.java_ - ([coverage report](https://sgra64.github.io/se1.bestellsystem/D12-Datamodel/coverage/datamodel/TAX.java.html#L1)).

&nbsp;

Other formats can be generated for coverage reports such as `.csv` or `.xml`.

```sh
coverage_report csv
coverage_report xml
```

```
[INFO] Analyzing 6 classes.
```

Verify reports have been generated:

```sh
ls -la coverage/coverage*
```

```
-rw-r--r-- 1 svgr2 Kein   572 May 25 19:53 coverage/coverage.csv
-rw-r--r-- 1 svgr2 Kein 24767 May 25 19:55 coverage/coverage.xml
```

&nbsp;

### D1.e Javadoc for Complete Datamodel

Generation of Javadoc for the complete `datamodel` package:

```sh
mk javadoc
```

Result is in sub-directory `docs` with
[index.html](https://sgra64.github.io/se1.bestellsystem/D12-Datamodel/javadoc).

&nbsp;

Package [datamodel](https://sgra64.github.io/se1.bestellsystem/D12-Datamodel/javadoc/se1.bestellsystem/datamodel/package-summary.html)
contains Javadoc for classes:

- _Customer.java_ - ([javadoc](https://sgra64.github.io/se1.bestellsystem/D12-Datamodel/javadoc/se1.bestellsystem/datamodel/Customer.html)),

- _Article.java_ - ([javadoc](https://sgra64.github.io/se1.bestellsystem/D12-Datamodel/javadoc/se1.bestellsystem/datamodel/Article.html)),

- _Order.java_ - ([javadoc](https://sgra64.github.io/se1.bestellsystem/D12-Datamodel/javadoc/se1.bestellsystem/datamodel/Order.html)),

- _OrderItem.java_ - ([javadoc](https://sgra64.github.io/se1.bestellsystem/D12-Datamodel/javadoc/se1.bestellsystem/datamodel/OrderItem.html)),

- _Currency.java_ - ([javadoc](https://sgra64.github.io/se1.bestellsystem/D12-Datamodel/javadoc/se1.bestellsystem/datamodel/Currency.html)),

- _TAX.java_ - ([javadoc](https://sgra64.github.io/se1.bestellsystem/D12-Datamodel/javadoc/se1.bestellsystem/datamodel/TAX.html)).

&nbsp;

## D2: Completing Features

Assignment D2 will complete features (methods) in
[Application_D1.java](src/application/Application_D1.java)
to print correct orders.

The assignment is structured in four stages:

- D2.a - [New Articles, Customers and Orders](#d2a-new-articles-customers-and-orders)

- D2.b - [_find()_ method](#d2b-find-method)

- D2.c - [_printOrder()_ method](#d2c-printorder-method)

- D2.d - [Order Value and Tax Calculations](#d2d-order-value-and-tax-calculations)

&nbsp;

Find markings `@TODO:` in
[Application_D1.java](src/application/Application_D1.java).

```sh
grep @TODO src/application/Application_D1.java
```

Output:

```
    * @TODO: (1.) create new Customer "Lena" with:
    * @TODO: (2.) create new articles with:
    * @TODO: (3.) create three new orders:
    * @TODO: (4.) implement the find()-method to find objects in collections:
    * @TODO: (5.) implement method to print order in table-format:
    * @TODO: (6.) implement the method to calculate the value of an order
    * @TODO: (7.) implement the method to calculate the value of an orderItem.
    * @TODO: (8.) implement the method to calculate the VAT of an order
    * @TODO: (9.) implement to calculate included VAT in a gross value
```

Read code and understand how it works, then complete the requested task.

### D2.a New Articles, Customers and Orders

@TODO: (1. - 3.)

Navigate to label @TODO (1.) and complete the challenge:

```java
/**
 * @TODO: (1.) create new Customer "Lena" with:
 *  - id: 651286, name: "Lena Neumann", contact: "lena228@gmail.com"
 * //
 * and add to List<Customer> customers;
 *
 * @TODO: (2.) create new articles with:
 *  - id: "SKU-300926", description: "Pfanne", unit-price: 49.99 EUR
 *  - id: "SKU-663942", description: "Fahrradhelm", unit-price: 169.00 EUR
 *  - id: "SKU-583978", description: "Fahrradkarte", unit-price: 6.95 EUR (reduced 7% tax rate)
 * //
 * and add to List<Article> articles;
 *
 *
 * @TODO: (3.) create three new orders:
 *
 * // Lena's order
 * +----------+--------------------------------------------+----------------------+
 * |6173043537| Lena's Bestellung:                         |                      |
 * |          |  - 1 Buch "Java"         3.26*    49.90 EUR|                      |
 * |          |  - 1 Fahrradkarte        0.45*     6.95 EUR|     3.71    56.85 EUR|
 * +----------+--------------------------------------------+----------------------+
 *
 * // Eric's 3rd order
 * +----------+--------------------------------------------+----------------------+
 * |7372561535| Eric's Bestellung:                         |                      |
 * |          |  - 1 Fahrradhelm        26.98    169.00 EUR|                      |
 * |          |  - 1 Fahrradkarte        0.45*     6.95 EUR|    27.43   175.95 EUR|
 * +----------+--------------------------------------------+----------------------+
 *
 * // Eric's 3rd order
 * +----------+--------------------------------------------+----------------------+
 * |4450305661| Eric's Bestellung:                         |                      |
 * |          |  - 3 Tasse, 3x 2.99      1.43      8.97 EUR|                      |
 * |          |  - 3 Becher, 3x 1.49     0.71      4.47 EUR|                      |
 * |          |  - 1 Kanne               3.19     19.99 EUR|     5.33    33.43 EUR|
 * +----------+--------------------------------------------+----------------------+
 *
 */
```

Output of the program should show the added customers and articles (orders will be completed
next):

```
java application.Application
Hello, Application_D1
(5) Customer objects built.
(6) Article objects built.
(4) Order objects built.
---
(+1) Customer objects added.
(+3) Article objects added.
(+3) Order objects added.
---
Kunden:
+----------+----------------------------+--------------------------------------+
| Kund.-ID | Name                       | Kontakt                              |
+----------+----------------------------+--------------------------------------+
|   892474 | Meyer, Eric                | eric98@yahoo.com, (+1 contacts)      |
|   643270 | Bayer, Anne                | anne24@yahoo.de, (+2 contacts)       |
|   286516 | Schulz-Mueller, Tim        | tim2346@gmx.de                       |
|   412396 | Blumenfeld, Nadine-Ulla    | +49 152-92454                        |
|   456454 | Abdelalim, Khaled Saad Moha| +49 1524-12948210                    |
|   651286 | Neumann, Lena              | lena228@gmail.com                    |
+----------+----------------------------+--------------------------------------+

Artikel:
+----------+----------------------------+---------------+----------------------+
|Artikel-ID| Beschreibung               |      Preis CUR|  Mehrwertsteuersatz  |
+----------+----------------------------+---------------+----------------------+
|SKU-458362| Tasse                      |       2.99 EUR|  19.0% GER_VAT       |
|SKU-693856| Becher                     |       1.49 EUR|  19.0% GER_VAT       |
|SKU-518957| Kanne                      |      19.99 EUR|  19.0% GER_VAT       |
|SKU-638035| Teller                     |       6.49 EUR|  19.0% GER_VAT       |
|SKU-278530| Buch "Java"                |      49.90 EUR|   7.0% GER_VAT_REDU  |
|SKU-425378| Buch "OOP"                 |      79.95 EUR|   7.0% GER_VAT_REDU  |
|SKU-300926| Pfanne                     |      49.99 EUR|  19.0% GER_VAT       |
|SKU-663942| Fahrradhelm                |     169.00 EUR|  19.0% GER_VAT       |
|SKU-583978| Fahrradkarte               |       6.95 EUR|   7.0% GER_VAT_REDU  |
+----------+----------------------------+---------------+----------------------+
```

### D2.b _find()_ method

TODO: (4.)

Navigate to label @TODO (4.) and implement the _find()_ method:

```java
/**
 * Find first matching object from the collection. Return empty Optional
 * if no object was found.
 *
 * @param <T> generic type of objects in collection.
 * @param collection collection of objects of type T.
 * @param matcher function that returns matching result for an object.
 * @return Optional with first matching object or empty Optional.
 */
public <T> Optional<T> find(List<T> collection, Function<T, Boolean> matcher) {

    /**
     * @TODO: (4.) implement the find()-method to find objects in collections:
     * List<Customer> customers, List<Article> articles, List<Order> orders
     */

    return Optional.empty();
}
```

### D2.c _printOrder()_ method

@TODO: (5.)

Navigate to label @TODO (5.) and implement the _printOrder()_ method such that it
prints one order in table format:

```java
/**
 * Print one order in table format into a StringBuilder, used by printOrders().
 *
 * @param order order to print into table.
 * @param tf table formatter used by printOrders().
 * @return table formatter used by printOrders().
 */
public TableFormatter printOrder(Order order, TableFormatter tf) {
    if(order==null || tf==null)
        throw new IllegalArgumentException("order or table formatter tf is null.");

    /**
     * @TODO: (5.) implement method to print order in table-format:
     *
     * +----------+--------------------------------------------+----------------------+
     * |8592356245| Eric's Bestellung:                         |                      |
     * |          |  - 4 Teller, 4x 6.49     4.14     25.96 EUR|                      |
     * |          |  - 8 Becher, 8x 1.49     1.90     11.92 EUR|                      |
     * |          |  - 1 Buch "OOP"          5.23*    79.95 EUR|                      |
     * |          |  - 4 Tasse, 4x 2.99      1.91     11.96 EUR|    13.18   129.79 EUR|
     * +----------+--------------------------------------------+----------------------+
     *
     * Figure out which data is need from the order at which place in the table
     * and extract that data from the order object.
     *
     * Fill in each row using the tf.row() method (see example below).
     */

    // "*" indicates reduced VAT rate
    tf.row("id", "name", fmtPrice(0L), "*", fmtPrice(0L, 1), fmtPrice(0L), fmtPrice(0L, 1));
    return tf;
}
```

### D2.d Order Value and Tax Calculations

@TODO: (6. - 9.)

Navigate to labels @TODO (6. - 9.) and implement methods for calculations:
_printOrder()_.

Implement the method to calculate the value of an order:

```java
/**
 * Calculate value of an order, which is comprised of the value of each
 * ordered item. The value of each item is calculated with
 * calculateOrderItemValue(item).
 *
 * @param order to calculate value for.
 * @return value of order.
 */
public long calculateOrderValue(final Order order) {
    if(order==null)
        throw new IllegalArgumentException("order is null.");

    /**
     * @TODO: (6.) implement the method to calculate the value of an order
     * using a Stream<OrderItem> over order items.
     */
    return 0L;
}
```

&nbsp;

Implement the method to calculate the value of an orderItem:

```java
/**
 * Calculate value of an order item, which is calculated by:
 * article.unitPrice * number of units ordered.
 *
 * @param item to calculate value for.
 * @return value of item.
 */
public long calculateOrderItemValue(final OrderItem item) {
    if(item==null)
        throw new IllegalArgumentException("item is null.");

    /**
     * @TODO: (7.) implement the method to calculate the value of an orderItem.
     */

    return 0L;
}
```

&nbsp;

Implement the method to calculate the VAT of an order:

```java
/**
 * Calculate VAT of an order, which is comprised of the VAT of each
 * ordered item. The VAT of each item is calculated with
 * calculateOrderItemVAT(item).
 *
 * @param order to calculate VAT tax for.
 * @return VAT calculated for order.
 */
public long calculateOrderVAT(final Order order) {
    if(order==null)
        throw new IllegalArgumentException("order is null.");

    /**
     * @TODO: (8.) implement the method to calculate the VAT of an order
     * using a Stream<OrderItem> over order items.
     */

    return 0L;
}
```

&nbsp;

Implement the calculation of included VAT in a gross value:

```java
/**
 * Calculate included VAT (Value-Added Tax) from a gross price/value based on
 * a tax rate (VAT is called <i>"Mehrwertsteuer" (MwSt.)</i> in Germany).
 *
 * @param grossValue value that includes the tax.
 * @param tax applicable tax rate in percent.
 * @return tax included in gross value.
 */
public long calculateVAT(final long grossValue, final TAX tax) {

    /**
     * @TODO: (9.) implement to calculate included VAT in a gross value
     * considering different tax rates.
     */

    return 0L;
}
```

&nbsp;

## Release Preparation

### a.) Packaging the Application

The packaged application will be `bin/application-1.0.0-SNAPSHOT.jar`.

```sh
mk package                  # run packaging
ls -la bin                  # show result in bin directory
```

Output:

```
total 16
drwxr-xr-x 1      0 May  5 23:18 ./
drwxr-xr-x 1      0 May  5 23:17 ../
-rw-r--r-- 1 173615 May  5 23:18 application-1.0.0-SNAPSHOT.jar
drwxr-xr-x 1      0 May  5 23:17 classes/
drwxr-xr-x 1      0 May  5 23:17 resources/
drwxr-xr-x 1      0 May  5 23:17 test-classes/
```

### b.) Running the packaged Application

Run the packaged jar-file with:

```sh
mk run-jar
java -jar bin/application-1.0.0-SNAPSHOT.jar
```

Final output of correct order table:

```
java application.Application
Hello, Application_D1
(5) Customer objects built.
(6) Article objects built.
(4) Order objects built.
---
(+1) Customer objects added.
(+3) Article objects added.
(+3) Order objects added.
---
Kunden:
+----------+----------------------------+--------------------------------------+
| Kund.-ID | Name                       | Kontakt                              |
+----------+----------------------------+--------------------------------------+
|   892474 | Meyer, Eric                | eric98@yahoo.com, (+1 contacts)      |
|   643270 | Bayer, Anne                | anne24@yahoo.de, (+2 contacts)       |
|   286516 | Schulz-Mueller, Tim        | tim2346@gmx.de                       |
|   412396 | Blumenfeld, Nadine-Ulla    | +49 152-92454                        |
|   456454 | Abdelalim, Khaled Saad Moha| +49 1524-12948210                    |
|   651286 | Neumann, Lena              | lena228@gmail.com                    |
+----------+----------------------------+--------------------------------------+

Artikel:
+----------+----------------------------+---------------+----------------------+
|Artikel-ID| Beschreibung               |      Preis CUR|  Mehrwertsteuersatz  |
+----------+----------------------------+---------------+----------------------+
|SKU-458362| Tasse                      |       2.99 EUR|  19.0% GER_VAT       |
|SKU-693856| Becher                     |       1.49 EUR|  19.0% GER_VAT       |
|SKU-518957| Kanne                      |      19.99 EUR|  19.0% GER_VAT       |
|SKU-638035| Teller                     |       6.49 EUR|  19.0% GER_VAT       |
|SKU-278530| Buch "Java"                |      49.90 EUR|   7.0% GER_VAT_REDU  |
|SKU-425378| Buch "OOP"                 |      79.95 EUR|   7.0% GER_VAT_REDU  |
|SKU-300926| Pfanne                     |      49.99 EUR|  19.0% GER_VAT       |
|SKU-663942| Fahrradhelm                |     169.00 EUR|  19.0% GER_VAT       |
|SKU-583978| Fahrradkarte               |       6.95 EUR|   7.0% GER_VAT_REDU  |
+----------+----------------------------+---------------+----------------------+

Bestellungen:
+----------+--------------------------------------------+----------------------+
|Bestell-ID| Bestellungen             MwSt*        Preis|     MwSt       Gesamt|
+----------+--------------------------------------------+----------------------+
|8592356245| Eric's Bestellung:                         |                      |
|          |  - 4 Teller, 4x 6.49     4.14     25.96 EUR|                      |
|          |  - 8 Becher, 8x 1.49     1.90     11.92 EUR|                      |
|          |  - 1 Buch "OOP"          5.23*    79.95 EUR|                      |
|          |  - 4 Tasse, 4x 2.99      1.91     11.96 EUR|    13.18   129.79 EUR|
+----------+--------------------------------------------+----------------------+
|3563561357| Anne's Bestellung:                         |                      |
|          |  - 2 Teller, 2x 6.49     2.07     12.98 EUR|                      |
|          |  - 2 Tasse, 2x 2.99      0.95      5.98 EUR|     3.02    18.96 EUR|
+----------+--------------------------------------------+----------------------+
|5234968294| Eric's Bestellung:                         |                      |
|          |  - 1 Kanne               3.19     19.99 EUR|     3.19    19.99 EUR|
+----------+--------------------------------------------+----------------------+
=======
>>>>>>> feat.730-json-data
|6135735635| Nadine-Ulla's Bestel                       |                      |
|          |  - 12 Teller, 12x 6.    12.43     77.88 EUR|                      |
|          |  - 1 Buch "Java"         3.26*    49.90 EUR|                      |
|          |  - 1 Buch "OOP"          5.23*    79.95 EUR|    20.92   207.73 EUR|
+----------+--------------------------------------------+----------------------+
<<<<<<< HEAD
|6173043537| Lena's Bestellung:                         |                      |
|          |  - 1 Buch "Java"         3.26*    49.90 EUR|                      |
|          |  - 1 Fahrradkarte        0.45*     6.95 EUR|     3.71    56.85 EUR|
+----------+--------------------------------------------+----------------------+
|7372561535| Eric's Bestellung:                         |                      |
|          |  - 1 Fahrradhelm        26.98    169.00 EUR|                      |
|          |  - 1 Fahrradkarte        0.45*     6.95 EUR|    27.43   175.95 EUR|
+----------+--------------------------------------------+----------------------+
|4450305661| Eric's Bestellung:                         |                      |
|          |  - 3 Tasse, 3x 2.99      1.43      8.97 EUR|                      |
|          |  - 3 Becher, 3x 1.49     0.71      4.47 EUR|                      |
|          |  - 1 Kanne               3.19     19.99 EUR|     5.33    33.43 EUR|
+----------+--------------------------------------------+----------------------+
                                                 Gesamt:|    76.78   642.70 EUR|
                                                        +======================+
done.
```

The packaged `.jar`-file: `application-1.0.0-SNAPSHOT.jar` can now be distributed.
=======

...

+----------+--------------------------------------------+----------------------+
                                                 Gesamt:|    76.78   642.70 EUR|
                                                        +======================+
```


&nbsp;

### Update Pricing

Update pricing by loading new JSON file
[data/articles_price_update.json](data/articles_price_update.json)
into the program.

1. Edit configuration file
    [resources/application.properties](resources/application.properties).

1. Since no code needed to be changed for the price update, the
    change is effective after restart. No re-compilation is needed.

    Re-run the application:

    ```sh
    mk run
    ```

Output with the price update:

```
Artikel:
+----------+----------------------------+---------------+----------------------+
|Artikel-ID| Beschreibung               |      Preis CUR|  Mehrwertsteuersatz  |
+----------+----------------------------+---------------+----------------------+
|SKU-693856| Becher                     |       2.49 EUR|  19.0% GER_VAT       |  <-- was   1.49
|SKU-638035| Teller                     |       8.49 EUR|  19.0% GER_VAT       |  <-- was   6.49
|SKU-425378| Buch "OOP"                 |      99.95 EUR|   7.0% GER_VAT_REDU  |  <-- was  79.95
|SKU-300926| Pfanne                     |      69.99 EUR|  19.0% GER_VAT       |  <-- was  49.99
|SKU-458362| Tasse                      |       4.99 EUR|  19.0% GER_VAT       |  <-- was   2.99
|SKU-278530| Buch "Java"                |      69.90 EUR|   7.0% GER_VAT_REDU  |  <-- was  49.90
|SKU-518957| Kanne                      |      29.99 EUR|  19.0% GER_VAT       |  <-- was  19.99
|SKU-663942| Fahrradhelm                |     199.00 EUR|  19.0% GER_VAT       |  <-- was 169.00
|SKU-583978| Fahrradkarte               |       8.95 EUR|   7.0% GER_VAT_REDU  |  <-- was   6.95
+----------+----------------------------+---------------+----------------------+

Bestellungen:
+----------+--------------------------------------------+----------------------+
|Bestell-ID| Bestellungen             MwSt*        Preis|     MwSt       Gesamt|
+----------+--------------------------------------------+----------------------+
|6135735635| Nadine-Ulla's Bestel                       |                      |
|          |  - 12 Teller, 12x 8.    16.27    101.88 EUR|                      |
|          |  - 1 Buch "Java"         4.57*    69.90 EUR|                      |
|          |  - 1 Buch "OOP"          6.54*    99.95 EUR|    27.38   271.73 EUR|
+----------+--------------------------------------------+----------------------+
|6173043537| Lena's Bestellung:                         |                      |
|          |  - 1 Buch "Java"         4.57*    69.90 EUR|                      |
|          |  - 1 Fahrradkarte        0.59*     8.95 EUR|     5.16    78.85 EUR|
+----------+--------------------------------------------+----------------------+
|8592356245| Eric's Bestellung:                         |                      |
|          |  - 4 Teller, 4x 8.49     5.42     33.96 EUR|                      |
|          |  - 8 Becher, 8x 2.49     3.18     19.92 EUR|                      |
|          |  - 1 Buch "OOP"          6.54*    99.95 EUR|                      |
|          |  - 4 Tasse, 4x 4.99      3.19     19.96 EUR|    18.33   173.79 EUR|
+----------+--------------------------------------------+----------------------+
|5234968294| Eric's Bestellung:                         |                      |
|          |  - 1 Kanne               4.79     29.99 EUR|     4.79    29.99 EUR|
+----------+--------------------------------------------+----------------------+
|4450305661| Eric's Bestellung:                         |                      |
|          |  - 3 Tasse, 3x 4.99      2.39     14.97 EUR|                      |
|          |  - 3 Becher, 3x 2.49     1.19      7.47 EUR|                      |
|          |  - 1 Kanne               4.79     29.99 EUR|     8.37    52.43 EUR|
+----------+--------------------------------------------+----------------------+
|7372561535| Eric's Bestellung:                         |                      |
|          |  - 1 Fahrradhelm        31.77    199.00 EUR|                      |
|          |  - 1 Fahrradkarte        0.59*     8.95 EUR|    32.36   207.95 EUR|
+----------+--------------------------------------------+----------------------+
|3563561357| Anne's Bestellung:                         |                      |
|          |  - 2 Teller, 2x 8.49     2.71     16.98 EUR|                      |
|          |  - 2 Tasse, 2x 4.99      1.59      9.98 EUR|     4.30    26.96 EUR|
+----------+--------------------------------------------+----------------------+
                                                 Gesamt:|   100.69   841.70 EUR|  <-- updated
                                                        +======================+
```


&nbsp;

### Answer Questions

1. What does `git remote add upstream git@...` do?

    - What is *"upstream"* in this expression?

1. What does `git fetch` do?

1. What is a *remote branch*?

1. What is a *tracking branch*?

1. What is a *merge conflict*?

    - How is a *merge conflict* marked in files?

    - How is a *merge conflict* resolved?

    - What does *"Accept Incoming"* compared to *"Accept Current"* mean?

    - Can *all* merge conflicts be resolved by selecting these options?

1. What does it mean that a *"merge is open"*?

1. How is an *open merge* closed (there are two alternatives)?

1. What is the result of a regular *merge*?

1. What is a *fast-forward (ff)* merge?

1. What happens with the merged branch after the merge?

1. Can a merged branch be removed?

1. What does `git gc` do?

    - Why should it be performed?

    - Which *"objects"* are removed?


<!-- 
```sh
mkdir f12json
cd f12json
git init
touch .gitignore
git add .
git commit -m "initial .gitignore"

git remote add se1-dev https://github.com/sgra64/se1-dev.git

# switch to main development branch, here: "main"
git switch main
git pull se1-dev f12-base --squash --allow-unrelated-histories --strategy-option theirs
git commit -m "pull/merge from se1-dev/f12-base"

source .env/setenv.sh
mk clean compile compile-tests run-tests
mk run


# fetch remote branch
git fetch se1-dev feat.730-json-data:feat.730-json-data

# create local tracking branch
git branch -u se1-dev/feat.730-json-data feat.730-json-data

# create/switch to new branch for the integration
git checkout -b int.feat.730-json-data

# merge the feature into t
git merge --allow-unrelated-histories feat.730-json-data

Auto-merging README.md
CONFLICT (add/add): Merge conflict in README.md
Auto-merging resources/application.properties
CONFLICT (add/add): Merge conflict in resources/application.properties
Auto-merging src/application/Application_F1.java
CONFLICT (add/add): Merge conflict in src/application/Application_F1.java
Auto-merging src/module-info.java
CONFLICT (add/add): Merge conflict in src/module-info.java
Auto-merging src/system/impl/DataStoreImpl.java
CONFLICT (add/add): Merge conflict in src/system/impl/DataStoreImpl.java
Auto-merging src/system/impl/IoC_Impl.java
CONFLICT (add/add): Merge conflict in src/system/impl/IoC_Impl.java
Automatic merge failed; fix conflicts and then commit the result.

git diff --check

mk clean compile compile-tests run-tests
mk run

git add .
git commit -m "merge commit feat.730-json-data"

# switch to main development branch, here: "main"
git switch main

# fast-forward merge
git merge int.feat.730-json-data

# delete branches
git branch -d int.feat.730-json-data
git branch -d feat.730-json-data
git branch -d -r se1-dev/feat.730-json-data

git count-objects
350 objects, 411 kilobytes

git gc
``` -->
>>>>>>> feat.730-json-data
