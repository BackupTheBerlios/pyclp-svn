Calling Python from Eclipse
###########################

It is possible to implement a predicate in python.

A simple example::

   from pyclp import *
   def external_predicate(arguments):
       #arguments store all arguments passed with call_python_function
       #Note unify usage
       return unify(arguments[0],arguments[1])
 

    init()   #Init ECLiPSe engine   
    #Register function with 'my_name' atom
    add_python_function('my_name',external_predicate)
    my_var=Var()
    # call_python_function,'my_name',[1,My_var])
    Compound('call_python_function',Atom('my_name'),[1,my_var]).post_goal()
    resume()
    if my_var.value() != 1:
        print("Failed resume ")

If an exception is raised during the python function execution ``abort`` event will be raised by
eclipse with the following message.
If this event will be handled by the user in eclipse program, eclipse engine will send a message to python (FLUSHIO) and then THROW value.
See the below example.

 

