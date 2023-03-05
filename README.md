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
- We will have Jira tickets with mock ups for each Acceptance Criteria.
- We will use Gherkin as a syntax standard.

### System Requirements Definition

As we mentioned in the Assumptions section, we will start providing a set of User Stories that allows us to create the set of Acceptance Tests.

#### User Story 1:
As a User  
I want to be able to select multiple products from a list  
So I can see the total price of the selected products  

##### Acceptance Criteria 1.1
__Feature__: Add products from product list

*__Scenario 1.1.1__*: Add multiple products to Cashier
>_Given_ the user is authenticated as a valid user  
>_And_ the user can access to the product list  
>_When_ the user selects a multiple products  
>_And_ the user selects multiple quantities for the selected products  
>_Then_ Cashier Systems displays price per unit  
>_And_ Cashier Systems displays price per product type (price x quantity)  
>_And_ Cashier System displays total price for all selected products  

##### Acceptance Criteria 1.2
__Feature__: Remove Products from a list  
*__Scenario 1.2.1__*: Decrease quantity products from Cashier List (Quantity >=1)  
>_Given_ the user is authenticated as a valid user  
>_And_ the user can access to the product list  
>_And_ the user has created a list of products in Cashier System  
>_When_ the user deletes a product from the list  
>_Then_ Cashier System reduces the product quantity by 1 unit (if quantity is not zero)  
>_And_ Cashier Systems updates price per product type (price x new quantity)  
>_And_ Cashier System updates total price for all selected products that remains in list  

*__Scenario 1.2.2__*: Delete products from Cashier List (quantity is zero)  
>_Given_ the user is authenticated as a valid user  
>_And_ the user can access to the product list  
>_And_ the user has created a list of products in Cashier System  
>_When_ the user deletes a product from the list that has quantity = 1  
>_Then_ Cashier System deletes product from list  
>_And_ Cashier System updates total price for all selected products that remain in list.  


#### User Story 2:
As a User  
I want to be able to select multiple products from a list that has special rules  
So I can see the total price of the selected products with special rules applied.  

##### Acceptance Criteria 2.1
__Feature:__ Apply "Buy x get y free" Rule  
*__Scenario 2.1.1__*: Add multiple products to Cashier with "Buy x Get y Free" Rule  
>_Given_ the user is authenticated as a valid user  
>_And_ the user can access to the product list  
>_When_ the user selects a multiple products that has "Buy x Get y Free" Rule  
>_And_ the user selects multiple quantities for the selected products  
>_Then_ Cashier Systems displays price per unit  
>_Then_ Cashier Systems duplicates any products that has free products after calculation  
>_Then_ Cashier Systems displays price as zero "0" per unit for each duplicated product  
>_And_ Cashier Systems displays price per product type (price x quantity)  
>_And_ Cashier System displays total price for all selected products  


##### Acceptance Criteria 2.2
__Feature:__ Apply "Buy > N pay x price per unit" Rule  
*__Scenario 2.2.1__*: Add more than N products to Cashier with "Buy > N pay x price per unit" Rule  
>_Given_ the user is authenticated as a valid user  
>_And_ the user can access to the product list  
>_When_ the user selects a more than N products that has "Buy > N pay x price per unit" Rule  
>_Then_ Cashier Systems displays price "x" per unit (Applying Rule)  
>_And_ Cashier Systems displays price per product type (price x quantity)  
>_And_ Cashier System displays total price for all selected products  


*__Scenario 2.2.2__*: Add less than N products to Cashier with "Buy > N pay x price per unit" Rule  
>_Given_ the user is authenticated as a valid user  
>_And_ the user can access to the product list  
>_When_ the user selects a more than N products that has "Buy > N pay x price per unit" Rule  
>_Then_ Cashier Systems displays normal price per unit (Not Applying Rule)  
>_And_ Cashier Systems displays price per product type (price x quantity)  
>_And_ Cashier System displays total price for all selected products  


##### Acceptance Criteria 2.3
__Feature:__ Apply "Buy > N pay x% price per unit" Rule  
*__Scenario 2.3.1__*: Add more than N products to Cashier with "Buy > N pay x% price per unit" Rule  
>_Given_ the user is authenticated as a valid user  
>_And_ the user can access to the product list  
>_When_ the user selects a more than N products that has "Buy > N pay x% price per unit" Rule  
>_Then_ Cashier Systems displays normal price reduced in x% per unit (Applying Rule)  
>_And_ Cashier Systems displays price per product type (price x quantity)  
>_And_ Cashier System displays total price for all selected products


*__Scenario 2.3.2__*: Add less than N products to Cashier with "Buy > N pay x% price per unit" Rule  
>_Given_ the user is authenticated as a valid user  
>_And_ the user can access to the product list  
>_When_ the user selects a more than N products that has "Buy > N pay x% price per unit" Rule  
>_Then_ Cashier Systems displays normal price per unit (Not Applying Rule)  
>_And_ Cashier Systems displays price per product type (price x quantity)  
>_And_ Cashier System displays total price for all selected products  


### Test Cases
Now we will start writing test cases for each Acceptance Criteria previously defined. And also we will add tags to identify which of the following test Cases should be included on which Test cycle. The Test Cycles will be the following:
- [Regression:]() 
- [Module:]()
- [Smoke:]()

**Test ID: TC-0001**
```
User Story: 1
Acceptance Criteria: AC-1.1
Scenario: Sc-1.1.1
Tag: [Regression] [Cashier]
Summary: Add simple product to Cashier List
Pre-conditions:
    - Valid User loged
    - Product List loaded
Steps to execute:
    Step                        Data                Result
    Go to Product List                              Product List is displayed
    Select random product A     Coffee              Product is selected
    Sumbmit selection                               Cashier list is displayed
                                Coffee bag          Product is displayed in Cashier List
                                Quantity: 1
                                PpU: £11.23
                                PpP: £11.23
                                Tot: £11.23
```

**Test ID: TC-0002**
```
User Story: 1
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
Acceptance Criteria: AC-1.1
Scenario: Sc-1.1.1
Tag: [Regression] [Cashier]
Summary: Add n item for one product to Cashier List
Pre-conditions:
    - Valid User logged
    - Product List loaded
Steps to execute:
    Step                        Data                Result
    Go to Product List                              Product List is displayed
    Select random product A     Coffee              Product is selected
    Submit selection                                Cashier list is displayed
                                Coffee bag          Product is displayed in Cashier List
                                Quantity: 1
                                PpU: £11.23
                                PpP: £11.23
                                Tot: £11.23
    Select same product          Coffee            Product is selected
    Submit selection                               Cashier list is displayed
                                Coffee bag         Product is displayed in Cashier List
                                Quantity: 2
                                PpU: £11.23
                                PpP: £22.46
                                Tot: £22.46
    Select same product          Coffee            Product is selected
    Submit selection                               Cashier list is displayed
                                Coffee bag         Product is displayed in Cashier List
                                Quantity: 3
                                PpU: £11.23
                                PpP: £33.92
                                Tot: £33.92
```


