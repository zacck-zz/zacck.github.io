---
  layout: post
  title: Daily Mocha Hacks
  tags:
  categories:
---

I use [Mocha](https://mochajs.org/) along with the [Karma](https://karma-runner.github.io/1.0/index.htmlmjac) test runner and Michael Jackson's [Expect](https://github.com/mjackson/expect) for assertions, No not the singer!

This is a little list of features that help with my daily tasks.

First checkout an example of my test-runner [set up](https://github.com/zacck/ReactTODOSample/blob/master/karma.conf.js).


Now to `Mocha`!

As your app grows is size and functionality so should your test suite or rather should I say,  **As your test suite grows in coverage so should your apps functionality**.

Eventually you find yourself with a suite containing a large number of tests.

**.only**

When running tests it's a huge time saver if I run a subset of tests instead of my whole test suite.
I have found the `.only` option very helpful for this.

Consider

```javascript
describe.only('cocktailActions', () => {

  describe('sync', () => {

    it('should generate addCocktail Action', () => {

      //mock a cocktail
      const cocktail  =  {
        name: 'Tea',
        contents: [
          {id: 23, amount: '2 spoons'},
          {id: 56, amount: '1 pinch'}
        ]
      };

      //mock the action
      const action =  {
        type: 'ADD_COCKTAIL',
        cocktail
      };

      //call the actions
      const res =  actions.addCocktail(cocktail);

      expect(res).toEqual(action);
    });
  });
});
```

Here you can see in a test suite that is numbering hundreds as is the case from my example, I would run only this subset of tests. This is both quicker in time and helps me to stay focused as I can iterate quicker!

**blank tests**

In Mocha you describe test cases using the it key word as you can see in the example above but you can simply flesh out your tests by writing empty cases, this will be skipped during the test runs.

Consider adding this to my example above

```javascript
it('should generate deleteCocktail action', () => {})


```

This will be skipped and listed when I run my tests and output would be like below

![mocha skipped](/images/skipped-test.png)


You can also use the `afterEach` and `beforeEach` functions to run some set up before some tests. Bear with me as this part may be a little dogmatic below is some set for running some async tests

```javascript
afterEach((done) => {
    firebaseRef.remove().then(() => done());
  });
```

As you can see here I clear my sample database that I use for testing after every test has run so they all run in isolation without each others data or contexts.


How do you use your testing?


Check out even more Mocha [options](https://mochajs.org/)

Queries? Suggestions? PR?

Back To Code! &#x1f61d;
