# Kantox Technical Test
## for: Software QA Engineer Position
## _by Erick Polato_

To ensure software quality, it is essential to refer to the ISO/IEC 25010 standard, which encompasses a set of eight key quality characteristics, as illustrated in the diagram below.
![Software Quality Tree](https://iso25000.com/images/figures/en/iso25010.png)

Adhering to this standard can help to establish rigorous quality assurance practices and ensure that software meets the high standards demanded by modern computing environments.

In addition, it is important to cover different Test Levels when developing a comprehensive testing strategy. These levels include:
- [Component Tests](), which focus on isolated software components;
- [Integration Tests](), which examine the behavior between interconnected components;
- [System Tests](), which evaluate the overall correctness of the entire product system; and
- [Acceptance Tests](), which verify that specific requirements have been implemented successfully.

All of these key testing concepts should be outlined in a Master Test Plan document, which lays out the overall test strategy for the product. However, in order to tailor this Technical Test, we will make the following assumptions:

### Assumptions

- Every Non-Functional characteristic of quality has been covered for our hypothetical product. This means that we will cover only [Functional Suitability]().
- Since the Technical Tests only include a specific functionality (Cashier System), we also exclude [Integration]() and [System Tests]() from the reach of this exercise.
- For the Component Test coverage we will provide some User Stories with their specific Acceptance Criteria to emulate how the Product Managers should define the requirement.
- We will have Jira tickets with mock ups for each User Story.
- We will use Gherkin as a syntax standard.

### Cashier System Requirement Definition

As we mentioned in the Assumptions section, we will start providing a set of User Stories that allows us to create the set of Acceptance Tests.

#### User Story 1:
As a User  
I want to be able to select multiple products from a list  
So I can see the total price of the selected products in Cashier System  

##### Acceptance Criteria 1.1
__Feature__: Add products from product list  

*__Scenario 1.1.1__*: Add multiple products to Cashier System  
>_Given_ the user is authenticated as a valid user  
>_And_ the user can access to the product list  
>_When_ the user selects multiple products one at the time  
>_Then_ the quantities for the selected products increments with each selection by one (1)  
>_And_ Cashier Systems displays price per unit by product  
>_And_ Cashier Systems displays total price by product (price x quantity)  
>_And_ Cashier System displays total price for all selected products  

##### Acceptance Criteria 1.2
__Feature__: Remove Products from a list  

*__Scenario 1.2.1__*: Decrease quantity products from Cashier List (Quantity >=1)  
>_Given_ the user is authenticated as a valid user  
>_And_ the user can access to the product list  
>_And_ the user has created a list of products in Cashier System  
>_When_ the user deletes a product from the list  
>_Then_ Cashier System reduces the product quantity by 1 unit (if quantity is not zero)  
>_And_ Cashier Systems updates total price by product (price x new quantity)  
>_And_ Cashier System updates total price for all selected products that remains in list  

*__Scenario 1.2.2__*: Delete products from Cashier List (quantity is zero)  
>_Given_ the user is authenticated as a valid user  
>_And_ the user can access to the product list  
>_And_ the user has created a list of products in Cashier System  
>_When_ the user deletes a product from the list that has only one (1) item  
>_Then_ Cashier System deletes product from list  
>_And_ Cashier System updates total price for all selected products that remain in list.  


#### User Story 2:
As a User  
I want to be able to select multiple products from a list that has special rules  
So I can see the total price of the selected products with special rules applied.  

##### Acceptance Criteria 2.1
__Feature:__ Apply "Buy X get Y free" Rule  

*__Scenario 2.1.1__*: Add multiple products to Cashier with "Buy X Get Y Free" Rule  
>_Given_ the user is authenticated as a valid user  
>_And_ the user can access to the product list  
>_When_ the user selects a multiple products that has "Buy X Get Y Free" Rule  
>_And_ the user sets multiple quantities for the selected products  
>_Then_ Cashier Systems displays price per unit  
>_And_ Cashier Systems displays products with normal price per unit for each X products  
>_And_ Cashier Systems displays products with zero (0) price per unit for each Y products if applies  
>_And_ Cashier Systems displays price per product type (price x quantity)  
>_And_ Cashier System displays total price for all selected products  


##### Acceptance Criteria 2.2
__Feature:__ Apply "Buy > N pay X price per unit" Rule  

*__Scenario 2.2.1__*: Add more than N products to Cashier with "Buy > N pay X price per unit" Rule  
>_Given_ the user is authenticated as a valid user  
>_And_ the user can access to the product list  
>_When_ the user includes more than N products that has "Buy > N pay X price per unit" Rule  
>_Then_ Cashier Systems displays price X per unit (Applying Rule)  
>_And_ Cashier Systems displays price per product type (price x quantity)  
>_And_ Cashier System displays total price for all selected products  


*__Scenario 2.2.2__*: Add less than N products to Cashier with "Buy > N pay X price per unit" Rule  
>_Given_ the user is authenticated as a valid user  
>_And_ the user can access to the product list  
>_When_ the user selects a more than N products that has "Buy > N pay x price per unit" Rule  
>_Then_ Cashier Systems displays normal price per unit (Not Applying Rule)  
>_And_ Cashier Systems displays total price per product (price x quantity)  
>_And_ Cashier System displays total price for all selected products  


##### Acceptance Criteria 2.3
__Feature:__ Apply "Buy > N pay X% price per unit" Rule  

*__Scenario 2.3.1__*: Add more than N products to Cashier with "Buy > N pay X% price per unit" Rule  
>_Given_ the user is authenticated as a valid user  
>_And_ the user can access to the product list  
>_When_ the user selects a more than N products that has "Buy > N pay X% price per unit" Rule  
>_Then_ Cashier Systems displays normal price reduced in X% per unit (Applying Rule)  
>_And_ Cashier Systems displays total price per product (price x quantity)  
>_And_ Cashier System displays total price for all selected products  


*__Scenario 2.3.2__*: Add less than N products to Cashier with "Buy > N pay x% price per unit" Rule  
>_Given_ the user is authenticated as a valid user  
>_And_ the user can access to the product list  
>_When_ the user selects a more than N products that has "Buy > N pay x% price per unit" Rule  
>_Then_ Cashier Systems displays normal price per unit (Not Applying Rule)  
>_And_ Cashier Systems displays price per product type (price x quantity)  
>_And_ Cashier System displays total price for all selected products  


### Test Cases
Now we will start writing test cases for each Acceptance Criteria previously defined. Also we will add tags to identify which of the following test Cases should be included on which Test cycle. The Test Cycles will be the following:
- [Regression:]() Full Coverage for the product. Should be executed on each Product Version increase.
- [Module (Cashier) :]() Full Coverage for each particular module. Should be executed before merging any change on the module into master branch or Release Candidate Product.
- [Smoke:]() Light coverage over all products. Can be executed in parallel with Module Test Cycle to guarantee the integration coverage before merging changes into a Release Candidate Product.

**Test ID: TC-0001**
```
User Story: 1
Acceptance Criteria: AC-1.1
Feature: Add products from product list
Scenario: Sc-1.1.1
Tag: [Regression] [Cashier]
Summary: Add simple product to Cashier List
Pre-conditions:
    - Valid User logged
    - Product List loaded
Steps to execute:
    Step                        Data                Result
    Go to Product List                              Product List is displayed
    Select random product A     Coffee              Product is selected
    Submit selection                                Cashier list is displayed
                                Coffee bag          Product is displayed in Cashier
                                Quantity: 1
                                PpU: £11.23
                                PpP: £11.23
                                Tot: £11.23
```

**Test ID: TC-0002**
```
User Story: 1
Feature: Add products from product list
Acceptance Criteria: AC-1.1
Scenario: Sc-1.1.1
Tag: [Regression] [Cashier]
Summary: Add 1 item for multiple products to Cashier List
Pre-conditions:
    - Valid User logged
    - Product List loaded
Steps to execute:
    Step                        Data                Result
    Go to Product List                              Product List is displayed
    Select random product A     Coffee              Product is selected
    Submit selection                               Cashier list is displayed
                                Coffee bag          Product is displayed in Cashier List
                                Quantity: 1
                                PpU: £11.23
                                PpP: £11.23
                                Tot: £11.23
    Select random product B     Apple               Product is selected
    Submit selection                               Cashier list is displayed
                                Apple               Product is displayed in Cashier List
                                Quantity: 1
                                PpU: £0.80
                                PpP: £0.80
                                Tot: £12.03
```

**Test ID: TC-0003**
```
User Story: 1
Feature: Add products from product list
Acceptance Criteria: AC-1.1
Scenario: Sc-1.1.1
Tag: [Regression] [Cashier]
Summary: Add multiple items for one product to Cashier List
Pre-conditions:
    - Valid User logged
    - Product List loaded
Steps to execute:
    Step                        Data                Result
    Go to Product List                              Product List is displayed
    Select random product A     Coffee              Product is selected
    Submit selection                                Cashier list is displayed
                                Coffee bag          Product is displayed in Cashier List
                                Quantity: 1
                                PpU: £11.23
                                PpP: £11.23
                                Tot: £11.23
    Select same product          Coffee            Product is selected
    Submit selection                               Cashier list is displayed
                                Coffee bag         Product is displayed in Cashier List
                                Quantity: 2
                                PpU: £11.23
                                PpP: £22.46
                                Tot: £22.46
    Select same product          Coffee            Product is selected
    Submit selection                               Cashier list is displayed
                                Coffee bag         Product is displayed in Cashier List
                                Quantity: 3
                                PpU: £11.23
                                PpP: £33.92
                                Tot: £33.92
```

>In order to make this Technical Test document non-repetitive and easy to read. We will just add the summary for the rest of the test cases...

**Test ID: TC-0004**
```
User Story: 1
Feature: Add products from product list
Acceptance Criteria: AC-1.1
Scenario: Sc-1.1.1
Tag: [Regression] [Cashier] [Smoke]
Summary: Add multiple items for multiple products to Cashier List
```

**Test ID: TC-0005**
```
User Story: 1
Feature: Remove products from product list
Acceptance Criteria: AC-1.2
Scenario: Sc-1.2.1
Tag: [Regression] [Cashier] [Smoke]
Summary: Decrease 1 item from a product with quantity > 1
```

**Test ID: TC-0006**
```
User Story: 1
Feature: Remove products from product list
Acceptance Criteria: AC-1.2
Scenario: Sc-1.2.2
Tag: [Regression] [Cashier] [Smoke]
Summary: Decrease 1 item from a product with quantity = 1
```

**Test ID: TC-0007**
```
User Story: 2
Feature: Apply “Buy x get y free” Rule
Acceptance Criteria: AC-2.1
Scenario: Sc-2.1.1
Tag: [Regression] [Cashier]
Summary: Verify that adding X or less products does not trigger “Buy X get Y free”
```

**Test ID: TC-0008**
```
User Story: 2
Feature: Apply “Buy x get y free” Rule
Acceptance Criteria: AC-2.1
Scenario: Sc-2.1.1
Tag: [Regression] [Cashier] [Smoke]
Summary: Verify that adding X+1 or more products triggers “Buy X get Y free” only until Y is reached.
```

**Test ID: TC-0009**
```
User Story: 2
Feature: Apply “Buy x get y free” Rule
Acceptance Criteria: AC-2.1
Scenario: Sc-2.1.1
Tag: [Regression] [Cashier]
Summary: Verify that adding 2(X+Y) products triggers “Buy X get Y free” 2 times.
```

**Test ID: TC-0010**
```
User Story: 2
Feature: Apply “Buy x get y free” Rule
Acceptance Criteria: AC-2.1
Scenario: Sc-2.1.1
Tag: [Regression] [Cashier]
Summary: Verify that adding (X+1) products triggers “Buy X get Y free” but when deleting 1 item the rule stops to apply.
```

**Test ID: TC-0011**
```
User Story: 2
Feature: Apply “Buy > N pay x price per unit” Rule
Acceptance Criteria: AC-2.2
Scenario: Sc-2.2.2
Tag: [Regression] [Cashier]
Summary: Verify that adding N products does not trigger “Buy > N pay x price per unit”.
```

**Test ID: TC-0012**
```
User Story: 2
Feature: Apply “Buy > N pay x price per unit” Rule
Acceptance Criteria: AC-2.2
Scenario: Sc-2.2.1
Tag: [Regression] [Cashier]
Summary: Verify that adding (N+1) products trigger “Buy > N pay x price per unit”.
```

**Test ID: TC-0013**
```
User Story: 2
Feature: Apply “Buy > N pay x price per unit” Rule
Acceptance Criteria: AC-2.2
Scenario: Sc-2.2.2
Tag: [Regression] [Cashier]
Summary: Verify that adding (N+1) products trigger “Buy > N pay x price per unit” but when deleting 1 item the rule stops to apply.
```

**Test ID: TC-0014**
```
User Story: 2
Feature: Apply “Buy > N pay x% price per unit” Rule
Acceptance Criteria: AC-2.3
Scenario: Sc-2.3.2
Tag: [Regression] [Cashier]
Summary: Verify that adding N products does not trigger “Buy > N pay x% price per unit”.
```

**Test ID: TC-0015**
```
User Story: 2
Feature: Apply “Buy > N pay x% price per unit” Rule
Acceptance Criteria: AC-2.3
Scenario: Sc-2.3.1
Tag: [Regression] [Cashier]
Summary: Verify that adding (N+1) products trigger “Buy > N pay x% price per unit”.
```

**Test ID: TC-0016**
```
User Story: 2
Feature: Apply “Buy > N pay x% price per unit” Rule
Acceptance Criteria: AC-2.3
Scenario: Sc-2.3.2
Tag: [Regression] [Cashier]
Summary: Verify that adding (N+1) products trigger “Buy > N pay x% price per unit” but when deleting 1 item the rule stops to apply.
```

### Final Considerations
In this Technical Test we created our own User Stories and Acceptance Criteria and based on those we create a coverage for them. But because of the nature of the exercise there are some important details that weren't defined. In a real life scenario it is important for a qualified QA Engineer to solve these undefined details in order to guarantee the testability and quality of the product.  

We will like to add some of the propper questions that a QA Engineer must with Project Manager during the Refinement of this User Stories:

- Does the Cashier System have a maximum quantity of items to be submitted?
- Will the Cashier System work with inventory? or is it possible to add infinite quantity?
- What does the system do when the user tries to introduce an item that does not exist? (invalid id)
- How does the system behave if the user tries to delete an item that is not in the current Cashier product list?
- Is it possible to add items to the same cashies through different users? or the same user logged in different sessions? or workstations?
- How does the system behave if there is a syntax error in the "products.yml" or "rules.yml"
- What happens if the rules are negative or zero? i.e. "Buy 0 Get -3 Free"
- Is there any validations for rules or products?
- Can 2 products have the same id?
- What happens if I update the rules file or the product file and then I update my Cashier list? Will the rules and prices be updated?

The answers of all these questions must be answered in the User Story ticket by the Product Manager and Stakeholders before the ticker is ready to be developed and goes into the spring.