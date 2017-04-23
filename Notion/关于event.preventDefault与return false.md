今天突然有一个疑问？
项目里如果你需要阻止默认事件

一般 return false就可以了

那么event.preventDefault和 return false的区别呢？

带着疑问网上搜了一下。

form :http://stackoverflow.com/questions/1357118/event-preventdefault-vs-return-false

Q:
When I want to prevent other event handlers from executing after a certain event is fired, I can use one of two techniques. I'll use jQuery in the examples, but this applies to plain-JS as well:

1. event.preventDefault()

$('a').click(function (e) {
    // custom handling here
    e.preventDefault();
});
2. return false

$('a').click(function () {
    // custom handling here
    return false;
});
Is there any significant difference between those two methods of stopping event propagation?

For me, return false; is simpler, shorter and probably less error prone than executing a method. With the method, you have to remember about correct casing, parenthesis, etc.

Also, I have to define the first parameter in callback to be able to call the method. Perhaps, there are some reasons why I should avoid doing it like this and use preventDefault instead? What's the better way?


A:

return false from within a jQuery event handler is effectively the same as calling both e.preventDefault and e.stopPropagation on the passed jQuery.Event object.

e.preventDefault() will prevent the default event from occuring, e.stopPropagation() will prevent the event from bubbling up and return false will do both. Note that this behaviour differs from normal (non-jQuery) event handlers, in which, notably, return false does not stop the event from bubbling up.

Source: John Resig