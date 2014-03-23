---
layout: post
title:  "UntangledJS"
date:   2014-03-23 22:21:00
---
Not a long time ago, for me the Java Script is for the uninitiated or for people who are not supposed to be programmers. Spoiled offspring of well groomed Java. Well, that opinion has changed forever and it didn't take a long time.

I belong to the Grady Booch army or the so called Java guy, the virtues of Object Orientation are forever crammed into my mind.  Whenever I hear about JavaScript all I could remember was the little hackish code I wrote to do some silly validations. And I never went back to it, never wanted to. And then there was AJAX, everyone's heartthrob, thought it was witchcraft and ignored it. Bliss.

But then something happened, few days after, all I was doing was scripting, using JavaScript, which you once considered is not even a "Programming Language". **Shi(F)t** happens.

>Java is to JavaScript what Car is to Carpet.  - Chris Heilmann

Sweet.

Except for the syntax, JavaScript has nothing to do with Java. The assumed silliness of JavaScript comes from considering it otherwise. Until you ask "what the heck is happening?", things look so stupid. So tangled.

Variable Scoping is one of those.

{% highlight JavaScript %}

function myFunction(){
    if(true){
        var myVar = 100;
    }
    alert(myVar); /* alerts '100' */
}
{% endhighlight %}

There is no block level scope in JavaScript, there is only a function scope. Hence the advise to declare all your variables once at the start of the function. The above piece of code is interpreted as -

{% highlight JavaScript %}
function myFunction(){
    var myVar; /* myVar is undefined at this point. */
    if(true){
         myVar = 100;
    }
    alert(myVar);
}
{% endhighlight %}

This kind of 'hoisting' is applicable for function declarations as well.

Speaking of functions, Yes, there are no classes. And I would use the cliche - 'Function is a first class citizen in Java Script'. What is meant by that is you can pass a function to another function as you would pass any other variable.

{% highlight JavaScript %}
function yourFunction() {
   alert("hello");
}
function myFunction(fn) {
   fn();
}
myFunction(yourFunction);

{% endhighlight %}​

Isn't it poweful?

But what about objects? Can I 'encapsulate' things and use? Yes you can.
First, there are object literals.
{% highlight JavaScript %}
var obj = {
	one: 1,
	two: 2,
	three: 3
}

var obj1 = {
    one : 1
    func1 : function()
    {
     alert(this.one); // Yes, 'this' refers to THIS object.
    }
}
{% endhighlight %}

And "Wait for it" you can create objects out of a function.

{% highlight JavaScript %}
var myFunction = function(n) {
		this.num = n + 1;
		this.printIn = function() {
			console.log(this.num);
		};
	}

var myObject = new myFunction(100);
myObject.printIn();
{% endhighlight %}

Function itself acts as a constructor in this case.

You can just access any of the properties like this -
{% highlight JavaScript %}
obj1.one
myObject.num
{% endhighlight %}

Or even like this -
{% highlight JavaScript %}
var myOne = "one";
obj1[myOne]  // cute :)
{% endhighlight %}

But wait a minute, there are no privates? is everything public?

But nothing is impossible with Java Script. You can have your privates too.
Enter **closure**.

{% highlight JavaScript %}
var myFunction = function() {
		var mySecretNum = 50;
		this.print = function() {
			console.log(mySecretNum);
		};
	};

var myObject = new myFunction(100);
myObject.print();
{% endhighlight %}

The 'print' function above forms a 'closure' for 'mySecretNum', and it stays private.
This feature is powerful especially with 'Ajax'. But that topic is for some other time.

And Oh, yeah, JavaScript is NOT strictly typed. You declare a variable and you can assigning anything to it. And if your declaration is not inside any function and if you forget to use 'var'  in front of the variable name, that becomes a global variable. OOPS!

It is just amazing the kind of things you can do with what you thought was a little smelly scripting language.

But with great power comes greater responsibility, and if you are not responsible, you will soon end up with unmanageable spaghetti code like this.

{% highlight JavaScript %}
var globalFunction = function() {
        var myFunction = function(fn) {
                console.log("mine!");
                var yourFunction = function() {
                        if(fn()) console.log("yours!!!");
                    }

                yourFunction();

            }
        var someOtherFunction = function() {
                myFunction(function() {
                    return true
                });
            }
        someOtherFunction();
    }

globalFunction();​
{% endhighlight %}

And that is a recipe for disaster. Something that makes one so averse to read, understand or use.

Untangle it.

There are tools to organize your code, much like you organize your Java code. Yes, modular code with all the goodness of OO is possible with JavaScript.

JavaScript ecosystem is flourishing.

First there was AJAX, then GMail happened, JQuery came along, Node was born. There were Firefox and Chrome.

Last few years have seen a spurt of Java Script libraries and frameworks. The days of finding work arounds for browser incompatibilities are gone, browser performance is not a problem any more. You can create cross platform mobile applications with just HTML and JavaScript, you can create desktop applications with Windows 8, heck! you can even do server side scripting. And AJAX is the thingy. HTML5 has arrived!

Ain't it worth giving a try?

Go, Do it.

*(Note: This was a write-up I penned for a news letter of the organization I work for. Unfortunately the news letter never came out)*