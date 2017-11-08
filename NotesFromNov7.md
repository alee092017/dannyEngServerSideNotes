# classes

so far, the new `class` stuff doesn't seem to hard for me, so i'll do my best to explain how it works.

if you remember, we did `constructors` and `.prototype` way back in unit 2 with John Master. this stuff is all about visualizing your code blocks as objects, and arranging the logic to reflect that.

this `class` stuff is no different. after building a class, you can crank out copies of the object you want, and those objects will be fully functional.

let say we want to make a `banana` class.

the framework for all this `class` stuff goes like this:

```
class [insert name here] {

  ...

}
```

The `...` is where you put all your code.

### constructor

a class contains a lot of little parts inside of it that determine its behaviors.

one of those parts is a constructor.

i know we did the whole 'you can do without a constructor' exercise with drake, but from what i've done so far having a constructor is necessary.

a constructor, like in the past, is the part of the class that builds the class. it's a method, a function within an object, that creates a banana for your code to use. it's also where we define the properties of the class: what color is the banana? how big is it? how much does it cost? etc.

and like many methods, it'll accept inputs.

```
class Banana {

  constructor (cost, color, size){
  
    ...
  
  }

}
```

so there's the framework for the constructor. notice that, within the `()`, we've got parameters of the banana. That way, when we want to construct a banana, we have full control over its properties. of course, you might not want some properties under your control; in that case, dont put that property in the `()`.

for the rest of the constructor, we've got to assign the parameters we input into actual keys for the object we're making.

object keys are the things that follow the `.` in an object. so `Banana.cost`, `Banana.color`, and `Banana.size` are all keys. we also see them like this

```
banana = {

  cost: 50,
  color: "yellow",
  size: "medium"

}
```

sometimes.

so for the contents of the constructor, we'll have to arrange the things like this:

```
constructor (cost, color, size){

  this.cost = cost;
  this.color = color;
  this.size = size;
  
 }
```

in the case of constructors, we need to use `this.` to refer to the new object we'll be creating each time. so the input named `cost` will be put into the new banana's `.cost` property, etc.

in the case there's some default value that you don't change, like `banana.type`, you can put `this.type = "fruit"` into the constructor.

### methods

as i mentioned before, methods are functions within an object.

using our banana example, we can eat a banana, peel a banana, and... toss a banana i guess. each one of these actions we can perform on a banana will be a method. and we'll need to put them into the class.

so in general, the result will look something like this:

```
class Banana {

  constructor (cost, color, size){
    this.cost = cost;
    this.color = color;
    this.size = size;
  }
  
  eat(){
    ...
  }
  
  peel(){
    ...
  }
  
  toss(){
    ...
  }

}
```

i know the methods are empty. i just want to point out that, like when we refer to an object's key, we can call these methods using `banana.eat()` or `banana.toss()`. please note that these methods will only work on the specific object we're talking about. we won't be eating every single banana in existence, i mean.

so for actual method writing, i can't give a lot of information. i mean, methods can do all sorts of things so long as you can churn out the right code for it. they follow the normal conventions for generating functions and all, and we've been writing those since forever.

```
eat(){
  this.status = "eaten";
}
```

also remember to use `this.` when referring to a specific banana.

happy coding. i'll update this if there's any requests.
