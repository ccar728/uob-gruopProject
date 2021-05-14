# Framework Chosen

The back-end part of this project is implemented using mongoDB and koa, and the front-end part is implemented using React. This project uses Node.js version 14.15.2, the package management tools are: yarn version 1.22.10, npm version 6.14.9.

# Front-end

The front-end is developed using TypeScript and React.

1. **Benefits of the React framework**

   React is generally used as the V layer in MVC, it does not rely on any other libraries and therefore can be used in development, integrated with any other library including Jquery, Backbone etc. It can be run on the browser side or rendered on the server side via nodejs. It can be run on the browser side or rendered on the server side via nodejs. React is very unique in its thinking and outstanding in its performance, allowing for front-end code to be written with less repetitive code and clear logic.

   React supports a special jsx syntax, by using this syntax it is possible to write code in a mix of js and html directly in react code, so that the logic of the code is very clear, but of course it also means that the jsx code needs to be compiled into normal javascript code in order to run in the browser, a process that can be done in a number of different ways depending on the actual project. React supports jsx syntax through the babel browser, a tool that translates jsx code into js code, so we need to use `requires.js` to load the module asynchronously within the project.

   The React framework uses the Virtual DOM technology, which is a Document Object Model, a tree-based API document that can simply be understood as the elements rendered out of a page. Changing the state of the real DOM takes a lot of system resources, so based on this concept, developers invented the Virtual DOM algorithm. virtual DOM is a JavaScript object that maps the real DOM, so if the state of any element needs to be changed, it is first changed on the Virtual DOM, rather than directly on the When a change is made, a new Virtual DOM object is created and the differences between the old and new Virtual DOM are calculated. The fundamental reason why the Virtual DOM algorithm saves system resources is that it is much more expensive to change the state of the real DOM than to change a JavaScript object. When a new item is added to this JavaScript object, a function calculates the difference between the old and new Virtual DOM and reacts to the real DOM. For React, all child components are re-rendered whenever the state of the application is changed, a process that can be controlled through the shouldComponentUpdate lifecycle method.

   React also encourages componentized applications. This essentially suggests that developers split their application into modules with clear functionality, each of which can be interlinked in a suitable way. Think of a component as a small piece of the user interface. For example, in an ebay page, the shopping cart is a component, the constantly refreshing list of displayed items is itself a component, and each item being displayed is still a component in itself.

   Moreover, React has a number of build tools that programmer can use to quickly set up their development environment. react can be used with Create-React-App/dva/umi and in this app we have chosen Create-React-App as the build tool for the project.

2. **Benefits of TypeScript over JavaSrcipt**

   In the following we will refer to TypeScript as TS and JavaScript as JS. TS is a superset of JS. TS is compatible with all the syntax of JS and complements the type part of JS which is missing, i.e. TS is a strongly typed language and is more readable and easier to maintain than JS. However, for most browsers, the TS needs to be translated into JS in order to be recognised by the browser, so when building a project, it is often necessary to install some first- or third-party toolkits, as well as the TSdeclaration files, which are used to convert the TS into the JS.

3. **Project file structure for the front end**

   The front-end project directory is called `front-end` and is divided into several directories: `build`,  `config`,  `node_modules`,  `public`,  `script`, `src` and a few remaining configuration files.

   * `build` contains the complete webpack-packaged page project, which is the full version of the project demo for publishing.

   * `config ` is the directory created by the cra automation tool for configuring webpack.
   * `node_modules` is the dependency file for the entire project, including the source code for the react framework itself, as well as the code for the cra-like tool.
   * `public` is a collection of public resources for the entire project, including the original html files and web icons for the project.
   * `src` is the source code directory for the entire project.
     * `src/components` contains several components that can be used in several places within the app; 
     * `src/icons` contains the diagrams needed for the project, stored in svg format; 
     * `src/model` is the component used for login and registration, using a promise to send asynchronous requests; 
     * `src/page` is the function value component for each page; 
     * `src/stores` holds the custom hooks used in this project, which can be reused throughout the project once wrapped; 
     * `src/types` holds our custom ts types; 
     * `src/utils` contains some tool components;
     * `src/App.tsx` is the entry file for the entire app; 
     * `src/helper.scss` is used to load global font styles;
     * `src/index.scss` is the global default style file;
     * The remaining four ts files are environment configuration files and test files generated by external toolkits such as cra, react-router, etc.

4. **Specific technical and implementation details used in the project front-end part.**

   * **Create-React-App**

     Developers can quickly create a React App using create-react-app by entering the following command: 

     ```
     yarn global add create-react-app@3.4.1
     create-react-app MoneyCat –template typescript
     cd MoneyCat
     yarn start
     ```

     Create-React-App is an official scaffolding tool for building React single page applications from the React team. It integrates with Webpack itself and is configured with a series of built-in loaders and default npm scripts, making it easy to quickly develop React apps with zero configuration. As webpack is too cumbersome to configure, it's a great option to use an official React scaffolding tool for configuring projects directly.

   * **CSS reset**

     HTML tags have a default style in browsers, which varies from browser to browser. For example, ul is indented by default, but in IE it is indented by margin, whereas in Firefox it is indented by padding. The default browser style can cause multi-browser compatibility problems and affect development efficiency. The solution to this is to remove all browser defaults from the outset, or more precisely to 'override' the browser's default CSS properties by redefining the tab styles.

     Here we hesitated for a while in choosing between using css-normalize and css-reset. At the beginning of the index.css file, add `@import-normalize` to complete the css normalize. The purpose of this statement is to ensure that the page is similar in terms of default style across browsers, but this is not the effect we want, as our own style will still override the default style later on.

   * **Configuring SCSS**

     SCSS is an advanced CSS syntax, also known as sass, which is an extended enhancement to css, adding rules, variables, blending, selectors, inheritance and other features. It can be understood as writing in js and then compiling to css. For example, it is possible to define repeatedly used css property values as variables in sass and then refer to them by variable name without having to write that property value repeatedly.

     We want the app to support sass syntax, so we need to install external dependencies to implement sass syntax support.

     Installing node-sass to make the app support the scss syntax. However, we encountered a number of problems during the installation of scss. Since node-sass is not very compatible and the download is not compiled locally, we searched the web for alternatives to node-sass and found a package called dart-sass, using the following command to install dart-sass:

     ```
     yarn add -dev node-sass@npm:dart-sass@1.25.0
     ```

     The reason why we have to pretend to download node-sass in the command to install dart-sass is because React doesn't support dart-sass, and installing dart-sass directly will give us an error, which means that I want yarn to install node-sass locally, but actually have npm replace this node-sass with dart-sass. This is possible because npm v6.9 has been updated with a new feature called package alias.

   * **Mobx**

     Mobx makes state management easy and scalable by transparently applying functional reactive programming. React and Mobx are a powerful duo, with React providing a mechanism to convert application state into a tree of renderable components and render them. MobX provides a mechanism to store and update application state for use by React.

   * **Configuring styled-component**

     This is a kind of CSS-in-JS solution. It is implemented using the JS template string.
     Enter the following command to install the dependencies for styled-components and the styled-components support for TS.

     ```
     yarn add styled-components
     yarn add –dev @types/styled-components
     ```

     The styled-component feature allows developers to write their CSS code in TS files, allowing for better component development, with each TS file managing its own CSS code, making it easy to modify and maintain. The dependency package actually translates the CSS code inside the TS code into an HTML `<style>` tag and automatically adds the class of the tag, which is a computed hash, and solves the problem of naming the class, as the styled-components package automatically matches the The style tag is automatically bound to a real html element on the page and the page is rendered together. And if a component needs to be reused more than once, we can directly use the styled component by `import` it in the same project, and all the code for the component exists in a single ts file, making it very easy to modify.

   * **Route implement** 

     A route represents the insertion of a url into the corresponding handler. After the user has entered the url to be accessed, the route will parse the path in the url, then find the corresponding pre-defined function according to the mapping in the mapping table and return the result to the user, thus completing an operation. Front-end routing differs from traditional routing in that it does not require a server to parse it, but is implemented through a hash function or history API. When developing, the route is used to set the access path and map the path to the corresponding component. When the user accesses the corresponding path, the route switches between different components according to the mapping relationship, the whole process is implemented in the same page and does not involve jumping between pages, which is a single page application.

     Front-end routing is faster when refreshing. As the back-end routing will re-send a request to the server when requesting a new path, and then re-render the page according to the corresponding result from the server, this process will be affected by network latency, while the front-end routing omits the whole request process and only completes part of the switching between components, so the page refresh speed will be relatively fast and the user experience is relatively good. Front-end routing is also highly reusable, as many modules in the code, such as layout and wrapper, can be used together, reducing the time wasted by repeated openings. If you don't use front-end routing, and just go through ajax to switch pages locally, the state of the page can't be recorded because the url doesn't change, but after using routing this problem can be solved.

   * **Adding bottom navigation with React-Router**

     React-router is a routing library maintained by the official react team, and is pretty much the only fully fledged routing library available in react. It enables component switching and state changes by managing URL. Enter the following command to install react-router-dom, and react-router's declaration file for TS:

     ```
     yarn add react-router-dom
     yarn add –dev @types/react-router-dom
     ```

     The React-router package provides a `<router>` tag that developers can use to wrap the entire code file. react-router actually treats each page as a functional component of react, using the link tag in a list of H's to navigate to the corresponding page component for access. Inside the `<router>` tag, the path is linked with the `<link>` tag, and then the `<switch>` tag is used below to indicate which path corresponds to which specific functional component, allowing you to jump to the corresponding page by typing the corresponding path in the browser's address bar. Since the `<link>` tag is used here, it is possible to jump to the corresponding page by clicking on the list element directly on the page. The corresponding CSS code can be written to achieve the effect of the bottom navigation bar.

     The app has three main pages, tags, bookkeeping and statistics, which are used for tag management, bookkeeping and data presentation respectively. As these three pages are essentially three functional components of react, when the user enters another path in the browser's address bar, the request will be blocked and the status code will be 404, so a path of `*` is added to the bottom of the `<switch>` tag, so that all addresses that do not correspond precisely to the three components are directed to a fixed page, and the user is informed on that page that The page that tells the user that the page does not exist is obviously also a simple functional component. The `<switch>` tag here actually specifies a browser rendering region, and only the components inside the `<switch>` will be rendered as real dom elements on the page.

     React-router has two common modes, history mode and hash mode. history mode is suitable for cases where there is a backend server and all paths are configured to the home page. Since this app is coded first, the hash mode is used here. The mode switch is done by writing `HashRouter as Router` in the `import from 'react-router-dom' ` in the app.tsx file. After switching to this mode, a # is inserted between the actual path of the page and the domain, indicating that the subsequent path is a hash value.

#  Back-end

1. **Data Structure**

   The first is the back-end design of the whole project. First of all, for users, we design the data of each user as a data structure, that is, user data structure. Each user object is a user. Each user has the following attributes: the same account name and password (encrypted by sha256), so app users don't have to worry about the disclosure of their own user information. Accounting cat will protect the user's privacy throughout the whole process. Sign (number of days to sign in), tags (number of groups to label).

2. **SHA-256 Algorithm**

   The five algorithms of SHA family, SHA-1, sha-224, SHA-256, sha-384, and sha-512, are planned by the National Security Agency (NSA) and released by the National Institute of standards and skills (NIST). This algorithm is the United States government standard algorithm, the latter four are sometimes called SHA-2. SHA is widely used in many security protocols, including TLS and SSL, PGP, SSH, S / MIME and IPSec. It was once regarded as the successor of MD5 (hash function widely used before). However, the security of SHA-1 is now seriously questioned by cryptographers. Some scholars have revealed the back door of NSA in SHA-1.Although there is no effective attack on SHA-2, its algorithm is basically similar to SHA-1, so some people began to develop other alternative hash algorithms. Sha256 is to generate a 256 bit hash.

3. **MongoDB**

   MongoDB is a database based on distributed file storage. Written by C + +. It aims to provide scalable high-performance data storage solutions for web applications. MongoDB is a product between relational database and non relational database, which has the most abundant functions and is most like relational database. It supports a very loose data structure, which is similar to JSON bson format, so it can store more complex data types. The most important feature of MongoDB is that the query language it supports is very powerful. Its syntax is a bit similar to the object-oriented query language. It can almost realize most of the functions similar to the single table query of relational database, and it also supports the indexing of data.MongoDB is designed to be high-performance, scalable, easy to deploy, easy to use, and convenient to store data. Its main functions are as follows.

   MongoDB feature: 

   1. It is easy to store data of object type. In MongoDB, data is grouped and stored in a set, which is similar to the table in RDBMS. An unlimited number of documents can be stored in a set. 
   2. The mode is free and the storage is modeless. The data stored in a collection in MongoDB is a modeless document, which is an important feature that distinguishes a collection from a table in RDBMS. 
   3. It supports full index, and can build index on any attribute, including internal objects. The index of MongoDB is basically the same as that of RDBMS. You can create indexes on specified attributes and internal objects to improve the query speed. In addition, MongoDB also provides the ability to create geospatial based indexes.
   4. Query is supported. MongoDB supports rich query operations, and MongoDB almost supports most queries in SQL.

   5. Powerful aggregation tools. MongoDB not only provides rich query functions, but also provides powerful aggregation tools, such as count and group, to support complex aggregation tasks using MapReduce. 
   6. Support replication and data recovery. MongoDB supports master-slave replication mechanism, which can realize data backup, fault recovery, read expansion and other functions. The replication mechanism based on replica set provides the function of automatic failure recovery to ensure that the cluster data will not be lost. 
   7. Use efficient binary data storage, including large objects such as video. Using binary format storage, you can save any type of data object. 
   8. Automatically process fragmentation to support the expansion of cloud computing hierarchy. MongoDB supports cluster automatic data segmentation. Data fragmentation can make the cluster store more data, achieve greater load, and ensure the load balance of storage. 
   9. Support Perl, PHP, Java, C #, JavaScript, ruby, C and C + + language drivers. MongoDB provides database driver packages for all the current mainstream development languages. Developers can easily program in any mainstream development language to access MongoDB database.
   10. The file storage format is bson (an extension of JSON). Bson is the abbreviation of binary format JSON. Bson supports nesting of documents and arrays.

   11. It can be accessed through the network. The MongoDB database can be accessed remotely through the network.

   ![mongoDB](/Users/ccar/Desktop/report/mongoDB.png)

4. **koa2 Framework**

   Koa2 is a web framework based on node, which is characterized by elegance, conciseness, strong expression and high degree of freedom. It's lighter than express. Koa1.0 uses the execution mode of Generator + co.js, while 2.0 uses async / await. Therefore, if you use 2.0, you need to run at node 8 or above. If the current version is too low, you can upgrade the version or install Babel cli, and use the Babel node to run. There are four modules to realize koa2

   The four modules are as follows:

   1. Encapsulate node HTTP server and create koa class constructor.
   2. Construct request, reponse and context objects.
   3. Implementation of middleware mechanism and onion peeling model.
   4. Error mechanism and error handling

