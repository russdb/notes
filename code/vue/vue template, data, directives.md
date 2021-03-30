tags: [[vue]] [[templates]] [[directives]] [[data]] [[vue basics]]

heart of Vue is a way to display data on the page. This is done using [[templates]].
HTML is embellished using special attributes—known as [[directives]]—that we use to tell Vue what we want to happen and what it should do with the data we’ve provided it.

![[vue basic template.png]]

the data object. This is how we tell Vue what data we want to display in the template  

in the template, we’re using the[[ v-if ]]directive to show only one of the three greetings, depending on what the variable is set to.

![[vue basic template better.png]]

business logic in the JavaScript and the view logic in the template is a much better approach than having the code responsible for deciding whether to show or hide the element in some JavaScript far away from the element in question. 

In addition to using directives, we can also pass data into templates by using interpo‐ lation, as follows:

![[vue basic interpolation.png]]

We can also combine the two, using both directives and interpolation to show some text only if it is defined or useful. See

![[vue interpolation and directive mixed.png]]

addition to being able to pass through strings and numbers, pass other types of data into templates. can pass an array or object into the template and look up a single property or item:

![[vue pass array basic.png]]