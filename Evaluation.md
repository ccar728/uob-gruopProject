# Details of how we evaluated your design

### Front-end

The front-end is developed using TypeScript and React.

1. **Benefits of the React framework**

   React is generally used as the V layer in MVC, it does not rely on any other libraries and therefore can be used in development, integrated with any other library including Jquery, Backbone etc. It can be run on the browser side or rendered on the server side via nodejs. It can be run on the browser side or rendered on the server side via nodejs. React is very unique in its thinking and outstanding in its performance, allowing for front-end code to be written with less repetitive code and clear logic.

   React supports a special jsx syntax, by using this syntax it is possible to write code in a mix of js and html directly in react code, so that the logic of the code is very clear, but of course it also means that the jsx code needs to be compiled into normal javascript code in order to run in the browser, a process that can be done in a number of different ways depending on the actual project. React supports jsx syntax through the babel browser, a tool that translates jsx code into js code, so we need to use `requires.js` to load the module asynchronously within the project.

   The React framework uses the Virtual DOM technology, which is a Document Object Model, a tree-based API document that can simply be understood as the elements rendered out of a page. Changing the state of the real DOM takes a lot of system resources, so based on this concept, developers invented the Virtual DOM algorithm. virtual DOM is a JavaScript object that maps the real DOM, so if the state of any element needs to be changed, it is first changed on the Virtual DOM, rather than directly on the When a change is made, a new Virtual DOM object is created and the differences between the old and new Virtual DOM are calculated. The fundamental reason why the Virtual DOM algorithm saves system resources is that it is much more expensive to change the state of the real DOM than to change a JavaScript object. When a new item is added to this JavaScript object, a function calculates the difference between the old and new Virtual DOM and reacts to the real DOM. For React, all child components are re-rendered whenever the state of the application is changed, a process that can be controlled through the shouldComponentUpdate lifecycle method.

   React also encourages componentized applications. This essentially suggests that developers split their application into modules with clear functionality, each of which can be interlinked in a suitable way. Think of a component as a small piece of the user interface. For example, in an ebay page, the shopping cart is a component, the constantly refreshing list of displayed items is itself a component, and each item being displayed is still a component in itself.

   Moreover, React has a number of build tools that programmer can use to quickly set up their development environment. react can be used with Create-React-App/dva/umi and in this app we have chosen Create-React-App as the build tool for the project.

2. **Benefits of TypeScript over JavaSrcipt**

   In the following we will refer to TypeScript as TS and JavaScript as JS. TS is a superset of JS. TS is compatible with all the syntax of JS and complements the type part of JS which is missing, i.e. TS is a strongly typed language and is more readable and easier to maintain than JS. However, for most browsers, the TS needs to be translated into JS in order to be recognised by the browser, so when building a project, it is often necessary to install some first- or third-party toolkits, as well as the TSdeclaration files, which are used to convert the TS into the JS.
   
   

### Back-end

1. **Why koa**

   The first step is to assess the back end. It is crucial in the overall design process, so we took great care in the design. From the evaluation of the framework used to the choice of database, we chose the most appropriate one for our needs. For the back-end framework, we compared the two most popular frameworks koa2 and express and chose one of them: the koa2 framework, built by the original express team, is lightweight, but powerful. The koa2 framework, which is built by the same team as express, is lightweight but powerful, and uses async and await instead of callbacks. Moreover, one of koa's intermediate middle keys can choose its own position for execution.

   Koa is a Web Framework in the same sense as Express, but is more of a middleware framework in terms of functionality and architecture design, providing a shelf and requiring almost all of the functionality to be done by third party middleware. The most obvious difference between Express and Koa is the handling of the Handler, one is a normal callback function and the other uses a Generator Function as a responder. In other words, Express does all HTTP requests for the current process on the same thread, whereas Koa uses co as the underlying runtime framework and uses the Generator feature to achieve a "concurrent response".

2. **Why mongoDB**

   The second step, after the evaluation of the choice of database, we chose in the database between the relational database and non-relational database MongoDB, compared to the Mysql database, MongoDB has the following characteristics advantages: the use of key-value pairs to store data, distributed, does not support ACID characteristics, non-relational database strictly speaking, not considered a database, should be a collection of data structured storage methods.

   Advantages: no parsing through the sql layer, high read and write performance; based on key-value pairs, data is uncoupled and easily scalable.The format of the stored data, nosql uses key:val form, document form, image form and so on, whereas relational databases only support the base type. So we prefer MongoDB to a relational database like mysql.

3. **Evaluate the choice of the design of data-structure**

   In terms of designing the data structure, we have designed it so that each user has a separate structure for each user. Our back-end can generate different paths based on different responses from the front-end, and thus manipulate the database to return different structures. So when evaluating this aspect of the design I felt that our data structure was relatively independent and easy to handle.



# Unit testing / Functional testing



# User acceptance testing

Black-box testing and configuration review are the main focus, supplemented by automated testing and special performance tests, in which the project implementer participates together with the end user in coordination with the project author. Of course, as a large and comprehensive information technology project, acceptance testing must be carried out with great care. It is important that those involved take a serious and responsible attitude.

Here are our test steps:

1. We accept that the functionality implemented in the software is the same as the original design document.
2. We verify the correctness of the software, with errors as a supplement.
3. We classify the software errors found in the acceptance tests and deal with them in a hierarchical manner until they pass the acceptance test.
4. We design the use cases in the acceptance tests in a comprehensive manner, so that we can confirm whether the functionality and performance of the software meet the requirements in the least amount of time and to the greatest extent possible. And the entire process requires user participation.

We tested the various functions of the app step-by-step, or hierarchically, during acceptance. We also black-box tested every sub-function of the software. We had a very detailed test plan, including function tests, framework tests and so on.
After the tests were completed, we made changes to address the issues found in the tests, and we retested after each iteration.