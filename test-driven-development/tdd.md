# Test Driven Development

Write tests before you write the code. **CODE IS DRIVEN BY TESTS**

Steps to test deiven development

1. write a unit test
2. run the test. See it fail
   - The application doesnt have the eature yet so it should fail
3. Write the feature code to pass the test
4. refactor the code to reduce duplication
5. repeat for each new feature of your app

## Why Test Driven Development

- It reduces errors and defects in the long run
- it leads to higher quality code

# Libraries and frameworks used to test react apps

## Jest

- A test runner made by facebook
- write tests in the \_ _tests_ \_ folder or with tests.js
- snapshot testing, coverage and mocking

## Enzyme

- manipulate React components and Dom behavior
- Enzyme + Jest = TDD with react
