# unity-reactive-var
small lib only for reactive variables

Uses UniRx implementation, but more compact.


# What is this:

A wrapper around any type that has several events 
* OnChanged - the most used, any time you set the variable, this is raised, as a result you hook everything in game directly to variables with any additional tracking or redundant delegates.
* OnPreEvaluate - also raised when changed, but before the value is set, and allows you to modify that value, for example clamp it
* evaluate - internal, used in child classes to internally evaluate the value to raise some concrete class specific event, for example r_bool has OnTrue, that is raised after the set value is evaluated in evaluate();

# Features:

* Events
* Serializeable by unity
* Works in inspector, reacts to user input (meaning if you change value on runtime it raises events)

# Usage

```cs

r_float Health = new r_float(100f);

Health.OnPreEvaluate += (x) => Mathf.Clamp(x, 0f, maxHealth);
Health.OnChanged += x => uiHealthText.text = x.ToString();
Health.Value -= 50;

float currentHealth = Health; //implicit

```

# Annoying part

Due to unity way of handling generics we cant use rVar<T> for inspector and serialization.
This means we use crutches, look at https://github.com/pointcache/unity-reactive-var/tree/master/Assets/rVar/CustomizeMe

generic non serializeable (by unity) are called rVar<R>
for unity use vars like

```cs

r_bool IsRunning;
r_int Moneys = new r_int(100);
r_float Health = new r_float();
r_Color...

```

Check https://github.com/pointcache/unity-reactive-var/blob/master/Assets/rVar/core/rVar.cs for all built in classes and add yours to the files in CustomizeMe folder.

These are used in commercial projects and are battletested.
