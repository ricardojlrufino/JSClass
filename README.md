# JSClass
Simple and easy Inheritance with JavaScript

## Inheritance Examples 

```javascript
var Animal = Class.extend(function(){

    // Public var
    this.walking = false;

    //  Contructor
    this.init = function (_walk) {
        this.walking = _walk;
    };

    // Public function
    this.walk = function () {
        console.log("[walk]");
        this.walking = true;
    }
});
```

```javascript
var Cat = Animal.extend(function(){

    // Private var
    var furtive = false;

    this.init = function () {
        this._super(false); // call supper constructor
    };

    // Private function
    function sneakyWalk(){
        furtive = true;
    }

    this.walk = function () {
        sneakyWalk();
        return this._super(); // Call super function...
    }

    this.meow = function () {
        return ">> meow !!"
    }
});
```

> You can extend using plain objects '{}', But you can not create private functions

```javascript
var Lion = Cat.extend({

    // Override
    meow : function () {
        // Lion meow ?? I think not ..
        return "meow not + " + this.hunt();
    },

    hunt : function(){
        if(!this.walking) this.walk();
        return "hunting !! (walking ? : "+this.walking+")";
    }

});

```

## Test

```javascript
var c = new Cat();
var l = new Lion();

console.log("c.walking:", c.walking); // => false
console.log("l.walking:", l.walking); // => false

c.walk();

console.log("c.walking:", c.walking); // => true
console.log("l.walking:", l.walking); // => false

console.log("c.meow():", c.meow());
console.log("l.meow():", l.meow());
console.log("l.walking:", l.walking); // => true (l.meow > hunt > walk)

console.log("l.meow:", typeof l.meow); // => function
console.log("c.hunt:", typeof c.hunt); // => undefined

console.log("=== Cat")
console.log("instanceof Animal : ", c instanceof Animal); // => true
console.log("instanceof Cat : ", c instanceof Cat); // => true
console.log("instanceof Lion : ", c instanceof Lion);   // => false
console.log("=== Lion")
console.log("instanceof Animal : ", c instanceof Animal); // => true
console.log("instanceof Cat : ", c instanceof Cat); // => true
console.log("instanceof Lion : ", c instanceof Lion);   // => false
```

