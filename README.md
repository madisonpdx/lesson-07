What Is AJAX
------------

AJAX stand for Asynchronous JavaScript and XML. What exactly all that means isn't that important. What is important is
to understand that AJAX is a very commonly used technique when developing web applications. Almost all the websites that
you visit probably use some form of AJAX to get and show information. The idea is that instead of constantly having to
refresh a web page to see new information or to send some information to a website, developers can write JavaScript
code to perform the same actions. For example when setting a new status on Facebook, the whole page doesn't reload.
Instead your new status is just added to the correct place within the page you are currently on. What you aren't seeing
is that JavaScript code is sending your status to a Facebook web server, the status is saved, the web server sends a
message back to the JavaScript code in your browser to confirm that the status is saved, only then after that whole
exchange has taken place is your new status added to the page.

The Challenge
-------------

Modify the schedule.html page so that it will show information about today's schedule.

- Write a JavaScript function that is run when the page is loaded.
- In your function, request today's schedule data from the web service with the address
http://madisonpdx.com/schedule_details.html.
- Take the data that is returned from the web service and display it on the page.

Comments
--------

Comments are a way to make notes about what your code is doing. They are ignored by the web browser and are not run
like your other code. Comments are helpful to explain your code to other people, or even as a reminder to yourself
when you come back to look at your code at a later time. You can write a comment that is only on one line by starting
with two forward slashes like:

```
// this is a single line comment.
```

You can also write comments that cover multiple lines by starting with a forward slash then an asterisk and ending
with an asterisk then a forward slash like:

```
/*
This is a multiple line
comment. I don't have to stay on
one line.
*/
```

Alert Message
-------------

One simple but helpful technique for debugging your code is to popup a message that either confirms that
you have reached a certain point in your code, or display information from within your code, like the contents
of a variable.

```
alert('put some message here');
```

Functions
---------

Functions allow you to bundle together lines of code and then run those lines of code whenever you choose.
The way to write a function is:

```
function myFunctionName() {
    alert('This message is shown when I run my function!!');
}
```

Later, to run the code contained in your function:

```
myFunctionName();
```

Modifying The HTML Page
-----------------------

To change an HTML tag through your code, you must first get a reference to that tag. A reference allows your code
to 'see' a specific HTML tag on the page. For example, if I asked you to look at the HTML and find a DIV tag with
the ID of 'schedule_details' you could look through the page and find that tag. After you find the tag, you could
make changes to it, such as adding text inside the tag. You must follow a similar process in code before you
can make changes to an HTML tag.

```
// get a reference to the tag with id schedule_details.
document.getElementById('schedule_details')
```

Once you have referenced an HTML tag you can do various things with it. For now, we can change what's inside the
tag by setting the innerHTML property of the tag.

```
// get a reference to the tag with id schedule_details and change what's inside that tag.
document.getElementById('schedule_details').innerHTML = 'This message is inside the DIV tag.';
```

XMLHttpRequest
--------------

This is a tool available in JavaScript to get data from web servers.

```
// create an instance of XMLHttpRequest and store it in a variable.
var xmlhttp = new XMLHttpRequest();
```

Next we must specify some code that will be run after we request data from the web server and the web server has
sent data back. To specify what code is run we create an anonymous function. An anonymous function is like a regular
function, except that it doesn't have a name. We are directly telling our XMLHttpRequest that it should run
this function when the web server responds. Since we won't ever have to run our function ourselves, then we
don't need to give it a name.

```
xmlhttp.onreadystatechange = function() {
    if (xmlhttp.readyState == 4 && xmlhttp.status == 200) {
        // if we are here then it means everything is working. popup a message with the data from the web server.
        alert(xmlhttp.responseText);
    }
}
```

Now that everything is configured, we need to tell our XMLHttpRequest to contact the web server and get the data. The
address of our web service is http://madisonpdx.com/schedule_details.html.

```
// open a connection to the web server and send our request for data.
xmlhttp.open('GET', 'web service address goes here', true);
xmlhttp.send();
```

Finally, instead of showing a popup with the data from the server, let's put that data onto the page. To figure that out
look back at the section titled Modifying The HTML Page.

Bonus Points
------------

By default the schedule web service returns the schedule for the current day. But you can pass a parameter to it
and specify a different date and it will return the schedule for that day. This would allow us for example to provide
a list of dates that the user could choose from and then we could show them the schedule for that day. Don't worry
about that for now though, just try to get the web service to return a different date. The parameter is named 'date'.

```
// get today's date and store it in a variable.
var myDate = new Date();

// use this line instead of the original web service address.
'http://madisonpdx.com/schedule_details.html?date=' + myDate.getFullYear() + '-' + myDate.getMonth() + '-' + myDate.getDate()
```

This still returns the same result, but now you are telling the web service what date to use instead of letting it
decide. You can supply a year, month, and day when creating a date. For example:

```
// myDate will be November 1, 2013. Note that JavaScript months start at 0, so the month number
// for January is 0 and for December is 11.
var myDate = new Date(2013, 10, 1);
```

The web service can only handle dates in this school year. You will get an error if you try to request other dates.


