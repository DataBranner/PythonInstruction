The basic principle of inheritance is that a subclass is considered to be a particular variety of its more general superclass. Figuring out how to use this principle to model things in the real (or the imaginary) world is important self-training in learning to do object-oriented programming.

Examples:

 * Class Tree and class Fruit. Tree can have various subclasses, such as OrangeTree, LemonTree, or what have you. Fruit can have various subclasses as appropriate. A tree has fruit, and "knows" how many fruit it has and what kind of fruit it has. The tree may have methods modeling its growth and ageing and flowering and bearing of fruit after certain conditions are met; the fruit may have methods modeling their ripening or rotting when the tree grows and ages.
 
 * Class Oven and class Cookie. Different kinds of cookies can subclass Cookie; there can even be different sub-subclasses of Cookie, depending on your imagination or neurosis. An oven may have different kinds of cookies baked in it; the oven knows its temperature and capacity; a cookie knows what its condition is on being baked at a certain temperature for a certain length of time. But neither the oven nor the cookie controls putting a cookie into an oven or taking it out at a certain time — who controls that? Well, you might have a Baker class, which controls the communication between Oven and Cookie, preventing the Oven and the Cookie from having to know anything about each other's domains — the Baker ensures that "separation of concerns" is rigorously observed.

Using non-Python examples, here's some discussion of classical applications of class inheritance at http://stackoverflow.com/questions/575217/whats-a-good-example-for-class-inheritance.

---

An important variety of class programming is called Model-View-Controller (MVC) structure. In order to ensure separation of concerns, the View class controls all communication with the human user, but none of the actual program logic; at the same time, the Model class (or classes) contain all the program logic, but never directly interact with the human user to get input or print output. The Controller class, like the Baker in the Oven-and-Cookie project, handles all interaction between Model and View. MVC structure is important in complex programs that interact with a human user.

There are some special rules I haven't mentioned — for one thing, the Model should override the `__str__` method. Note that the `__str__` method doesn't actually print anything! It merely returns a string of some kind, showing what the Model wants itself to look like when printed. It isn't the job of the Model to print anything — it's the job of the View. But when an instance of the class Model is printed, Python then turns to the overridden `__str__` method to decide what to print. It *is* the job of the Model to know what to print when View (or some other class) decides to print an instance of the Model — and knowing what to print when asked is accomplished with __str__`. Below is a very simple example (I'm using Ipython):

```python
In [1]: import random

In [2]: class M():  # Define class M, with one attribute and one method.
    def __init__(self):
        self.value = random.random()
    def __str__(self):
        return "My value is {}.".format(self.value)
   ....:     

In [3]: m = M()     # Instantiate class M and assign m as the instance name.

In [4]: m.value     # Directly report the "value" attribute of instance m.
Out[4]: 0.1496701267279016

In [5]: print(m)    # Use print to report what instance m says it looks like.
My value is 0.1496701267279016.
```

Note that line 5, using print, actually forced `m.__str__` to be called behind the scenes.

If you imagine that a project is like a company, then the Model is the parts of the company where the business decisions are being made, while the View is the front office that speaks to the public. The public never gets to talk to or hear from the Model. And the View never gets to make any decisions, except for relatively shallow decisions like what language are we speaking? or what time is the press conference being held?

The Controller is like a secretary or manager who controls all conversation between Model and View. In a sense, the Controller is the most powerful part of the project, since it controls everything else. I like to think of it as a kind of lawyer, handling two people who are in the midst of getting divorced. The two people getting divorced never speak to each other directly any more — all communication goes through the Controller.

So the Controller will instantiate both Model and View, and make sure their respective methods are called at the appropriate times. Looking at some examples will make this clear.

---

Python has two special methods that all objects possess: isinstance() and issubclass().

 * `isinstance(object_x, ClassY)` returns `True` if `object_x` is an instance of `ClassY` or of some subclass of `ClassY`. 

 * `issubclass(ClassX, ClassY)` returns `True` if `ClassX` is a subclass of `ClassY` (or the same class as `ClassY`).

---

Python differs from some object-oriented languages in permitting **multiple inheritance**. You will only very rarely ever have to use that, but I suppose it's the sort of thing you might find yourself tossed into in an interview.

[end]