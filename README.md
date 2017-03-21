# unity-reactive-var
small lib only for reactive variables

Uses UniRx implementation, but more compact.


What is this:
A wrapper around any type that has several events 
* OnChanged - the most used, any time you set the variable, this is raised, as a result you hook everything in game directly to variables with any additional tracking or redundant delegates.
* OnPreEvaluate - also raised when changed, but before the value is set, and allows you to modify that value, for example clamp it
* evaluate - internal, used in child classes to internally evaluate the value to raise some concrete class specific event, for example r_bool has OnTrue, that is raised after the set value is evaluated in evaluate();

Features:
* Events
* Serializeable by unity
* Works in inspector, reacts to user input (meaning if you change value on runtime it raises events)
