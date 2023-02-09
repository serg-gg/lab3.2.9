# lab3.2.9
class decorator
It is necessary to declare a decorator class named Handler, which could be applied to functions as follows:

@Handler(methods=('GET', 'POST')) # by default methods = ('GET',)
def contact(request):
return "Sergey Balakirev"
Here, the methods argument of the Handler decorator contains a list of allowed requests to be processed. The decorated function itself is called by analogy with the previous feat:

res = contact({"method": "POST", "url": "contact.html "})
As a result, the contact function should return a string in the format:

"<method>: <data from function>"

In our example, it will be:

"POST: Sergey Balakirev"

If there is no method key in the request dictionary, then a GET request is assumed by default. If the method key takes a value that is not in the methods list of the Handler decorator, for example, "PUT", then the decorated contact function should return the value None.

To simulate GET and POST requests, two auxiliary methods with signatures must be declared in the Handler class:

def get(self, func, request, *args, **kwargs) - to simulate the processing of a GET request
def post(self, func, request, *args, **kwargs) - to simulate POST request processing

Depending on the type of request, the corresponding method should be called (its selection in the class can be implemented by the __getattribute__() method). At the output, these methods should form strings in the specified format.

P.S. It is enough to declare only a class in the program. You don't need to display anything on the screen.

A little help
To implement a decorator with class-level parameters in the initializer __init__(self, methods), we prescribe a parameter for the decorator, and declare the magic method __call__() as a full-fledged decorator at the function level, for example:

class Handler:
def __init__(self, methods):
# here are the necessary lines

def __call__(self, func):
def wrapper(request, *args, **kwargs):
# here are the necessary lines
return wrapper
