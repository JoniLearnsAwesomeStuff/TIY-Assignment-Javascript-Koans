# About Arrays
* should know about shifting arrays
  * I grasp these concepts but I have to think, reflect, and sometimes look them up.

# About Functions
*

# About Mutability
* should expect object properties to be public and mutable
  * No struggles with this one really...

* should understand that constructed properties are public and mutable
  * This is going to take some time to really learn. I don't struggle with the
    concept so much as remembering the difference between constructed and prototype functions (regarding Mutability and more...);
    ```
    function () {
      function Person(firstname, lastname)
      {
        this.firstname = firstname;
        this.lastname = lastname;
      }
      var aPerson = new Person ("John", "Smith");
      aPerson.firstname = "Alan";

      expect(aPerson.firstname).toBe("Alan");
    });
    ```

* should expect prototype properties to be public and mutable
  * See comments about constructed properties. Copying code in here to help me study this more.
    ```
    function Person(firstname, lastname)
    {
      this.firstname = firstname;
      this.lastname = lastname;
    }
    Person.prototype.getFullName = function () {
      return this.firstname + " " + this.lastname;
    };

    var aPerson = new Person ("John", "Smith");
    expect(aPerson.getFullName()).toBe("John Smith");

    aPerson.getFullName = function () {
      return this.lastname + ", " + this.firstname;
    };

    expect(aPerson.getFullName()).toBe("Smith, John");
    ```

* should know that variables inside a constructor and constructor args are private
  *
    ```
    function Person(firstname, lastname)
    {
      var fullName = firstname + " " + lastname;

      this.getFirstName = function () { return firstname; };
      this.getLastName = function () { return lastname; };
      this.getFullName = function () { return fullName; };
    }
    var aPerson = new Person ("John", "Smith");

    aPerson.firstname = "Penny";
    aPerson.lastname = "Andrews";
    aPerson.fullName = "Penny Andrews";

    expect(aPerson.getFirstName()).toBe("John");
    expect(aPerson.getLastName()).toBe("Smith");
    expect(aPerson.getFullName()).toBe("John Smith");

    aPerson.getFullName = function () {
      return aPerson.lastname + ", " + aPerson.firstname;
    };

    expect(aPerson.getFullName()).toBe("Andrews, Penny");
    ```
    * Used console.logs to prove this to myself:
    ```
    console.log('aPerson.firstname: ', aPerson.firstname);
    console.log('aPerson.lastname: ', aPerson.lastname);
    console.log('aPerson.fullName: ', aPerson.fullName);

    console.log('aPerson.getFirstName(): ', aPerson.getFirstName());
    console.log('aPerson.getLastName(): ', aPerson.getLastName());
    console.log('aPerson.getFullName(): ', aPerson.getFullName());
    ```


# About Higher Order Functions
* Oh boy! I struggled with this. Had to create a playground
  project, pull in underscore.js and play with these.
  * At this point I can say I understand chaining (no issues there).
  * Once I got past the strangeness of using an underscore,
    the functions made more sense...
  * except for reduce: I thought I got it here but really struggled with
    it later in the last module "Applying What We've Learnt".

# About Objects
* should know properties that are functions act like methods
  * Understand the concept pretty well (I think). However, struggled with
    this piece of code:
    ```
    Array(noOfBrains + 1).join(" " + this.mastermind)
    ```
    This should translate to "Brain Brain Brain Brain Brain",
    but I still don't get why? MDN isn't helping.
    Never mind. Found this explanation Stackoverflow:
    [StackOverflow](http://stackoverflow.com/questions/30522129/javascript-koans-about-objects-how-does-this-function-work-in-3)
    * Array() acts like new Array() and creates an array with the
      number of uninitialized elements passed in the parens.

  * Oh yay! A delete method! I was wondering how we could remove
    properties from objects.

  # About Inheritance
  * Great topic -- must pay attention to detail or it can be missed.

  # Applying What We've Learnt(sp?)
  * given I'm allergic to nuts and hate mushrooms, it should find a pizza I can eat (functional)
    * "/* solve using filter() & all() / any() */"
    * ^^ Never could get the any or all methods to work for me
      So I used two filters:
      ```
      var productsICanEat = [];

      /* solve using filter() & all() / any() */
      var noHazNuts = _(products).filter(function(x) {
          return x.containsNuts === false
        });

      var productsICanEat = _(noHazNuts).filter(function(y) {
          return "mushrooms" in y.ingredients;
      });
      ```
      * Later I searched for solutions online. Found this on StackOverflow
        but it returns a list of ingredients -- not a list of pizzas (which
        would be a zero-sized list):
        ```
        var productsICanEat = [];

        var noMushrooms = _(products).chain()
         .filter(function(x){
           return x.containsNuts;
         })
         .reject(function(x){
           return _(x.ingredients).any(function(y){
                 return y === "mushrooms";
         })})
        ```
