# Typescript NextJS Redux simple App

### Prerequisites

`Node 9+`

### Installing

```
$ npm install -g eslint jest now
$ npm install
```
### In order to configure pre-commit that will execute prettier-eslint & unit-test before commit
```
$ npm install --save-dev husky prettier-eslint
```

### Starting the application

In order to start, just execute the following command line:
```
$ npm run dev
```

And then, open a browser with the following link:
```
http://localhost:3000
```
### Running unit tests
```
$ npm run test
```
### Running unit tests in watch mode
```
$ npm run test:watch
```

### Some design, principles and best practices

* Re-Ducks: Following this proposal structure improve modularity and encapsulation (only expose `index.tsx` from each dock folder, for instance: `state/ducks/catalog/index.ts`). Also allow us to scale better and improve testability of actions, action creators, reducers, operators and selectors in a really flexible way.
* In order to be easy to search your resources, the file name conventions of the project is the following:
    - [module_name].[type-file].ts
     Eg: 
    - `article.actions.ts`
    - `article.d.ts`
    - `article.operations.ts`
    - `article.reducers.ts`
    - `article.selectors.ts`
    - etc

* Typescript: Implementing check typing in a dynamic interpreted language like JS, help us and also to Ides, to catch typos and errors while your are coding. That is a really important when you app will be large.
* Selectors (`selectors`): Implementing selectors improve complex operations and also to lifting our state in a more granular way (help us to keep following SRP principle). Also we open a windows of improvements to implement `reselect` or other mechanism of memoization.
* Selectors naming convention:`Selector name: get<Noun>`
* Following top down best practice redeability declaration (most important and public collaborates first, like a news paper).
* BEM: using block element modifier and with some variation of SMACSS like (`is-visible` instead of `block--visible`) is a really clean way to style components. Also it's a really a performance way to style component instead use neested selectors. (you don't care any more about not pass to 3 nested level)
* Server: the end-point should be prefixed with: `/api/v1`. That help us to versioning our API, and also to be a common pre-fix url to apply easy filters, middlewares, etc.
* REST calls in a middleware, instead of action creators: That allow us to decrease the coupling between our action creators and the side-effect libraries(`redux-thunk`, `redux-saga`, `redux-observable`, etc). Also make test simpler and our modules more isolates. Also give us teh possibility to implement in parallel with other libraries like `redux-observable` with Epics idea.
* Action Types naming convention: All async action, should be post fixed with:
1. `REQUESTING_COMPLETED`
1. `REQUESTING_FAILED`
And also should have a attribute `async:true` in their body, and has the following data structure: 
```
type: types.REQUEST_SEARCH,
    meta: {
        async: true,
        path: `/search?text="${text}"`,
        method: 'GET',
    },
```
Following that convention, help us to avoid boilerplate code using `api-service.ts` middleware.

* Action Types names convention is:
1. ACTION: Effect is most commonly a noun that means the result of an action —> <NOUN>_<VERB> —> `CATALOG_ADDED` | `CATALOG_REMOVED`
1. ASYNC ACTION CREATOR: Affect is most commonly a verb —> <VERB><NOUN> —> `REQUESTING_CATALOG` | `REQUESTING_CATALOG_COMPLETED` | `REQUESTING_CATALOG_FAILED`

### Frameworks & libraries
* NextJS used to provider server rendering for performance, SEO and Code splitting reasons.
* React-testing-Library: A really useful library to help us to test React component in a clean, predictable and readable way.
* Redux: The reactive programming allow us to build more predictable, scalable & Solid web application.
* Immutablejs: For performance reason, allowing us to perform shallow equality and avoid unheeded rendering. (only for container component and reducer layer. In order to avoid problems when handling data, try to minimize the interoperability, and only keep your container component with immutable info. Lets dumb components with native objects.
* Lodash: For cross browsing support, performance and reliable way to handler data. (only for dump component and action creators).
* Prettier/husky/lint-staged/Eslint, Help us to avoid commit and push some code that don't follow with the default standards of the project and also prevent to push some code that don't pass the UT. (It's already configure airbnb, and eslint:recommended practices)
* Following in each part of the app SRP (Single responsibility principle). One reason to change. Each module/class/function has their own level of the abstraction.

### Testing tips

* Test should follow the SRP principle too (single responsibility principle). Do one thing, test one thing.
* Test files, should be ended with `*.test.tx` and should be placed in the same folder from their SUT (Subject under test).
* Keep in mind the implicit structure of test must be AAA (Arrange, Act, Assert).
* Each test must be isolated, means that one test not be dependent to another in order to get given result, therefore it should not matter the order of execution of them.
* Avoid global variables. Instead, declare them in setup method.
* Follow the DRY principle (Don’t Repeat Yourself). If we identify that we have repeated code throughout our tests use beforeEach function to put the code in one place.
* Putting comments in the header of the test is an anti-pattern, avoid them.
* Don't test action isolate, when testing reducer I like to test action as well in order to avoid unwanted testing. (I know that sounds like an integrating test instead of unit test, but it make sense for me.)

### Technical pending implementation

* Improve in a way that much closer to be a full PWA application.
* Implement Normalize, to have a flatten state. That help you to make more performance the shallow equality performed and also to deal with a easy structure store.
* Implement some CI such as Circle or Travis.
* E2E Testing with Cypress. It's really powerful implement it, in order to save time in the regressions testing.
* Improve Logging report in Backend side and also in front-end side to be sure that your app are working properly, otherwise send a email when throws some error.
* implement reselect to improve performance in out selectors.
* Increase UT code coverage from FE and BE.


## Particulars React component design:

* I choose to be build `Card` component in a uncontroller way, because I didn't want to populate the global state, with custom states of the inner context. I prefer in this particular case, let the global state clean of custom behaviors from that particular component. That allow us, to be focus in buisiness logic, and high level state of your app. And also avoid potencial performance problem. [Please take a look this comment for more detail](https://twitter.com/acdlite/status/1045362245507506176). Also Kent Dodds, also mentioned  that. In some use cases, you state should be near as much as possible from their origin. A general rule, it's try to build controller component, as much as possible. But, the component that has a really complex behavior, didn't make sense to populate your global state, with internal state of the component.
* Aslo `Card` component could be large, and I didn't split in sub component as well. That was for the reason, to prevent that my application surface, don't keep growing unneeded. Just, if you need to re-use some port of the component, split that. But, don't split from the start. This Rule, is some trend the las year that I saw that is doing several React expert. 

### Deployed link:
[Link APP](https://application-blog-2.herokuapp.com)
