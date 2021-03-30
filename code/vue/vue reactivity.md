[[vue]][[vue basics]][[vue reactivity]]
Vue watches the data object for changes and updates the DOM when the data changes. To

![[vue simple reactivity.png]]

In addition to working with interpolation to output the value to the page, Vue’s reac‐ tivity functionality also works when using a property of the data object as an attribute to a directive

Reactivity is an extremely important feature and part of what makes Vue so powerful


#### How it works

Vue’s reactivity works by modifying every object added to the data object so that Vue is notified when it changes.

Every property in an object is replaced with a getter and setter so that you can use the object as a normal object, but when you change the property

![[vue simple object.png]]

you can override the property by using Object.defineProperty(): 

![[vue object.devineProperty().png]]

#### Caveats 
some limitations to how this works. Understanding

**Adding new properties to an object**
getter/setter functions are added when the instance is initialized, only existing properties are reactive

when you add a new property, it won’t be reactive if you do it directly:

![[vue reactive object.png]]

While the formData.username property will be reactive and respond to changes, the formData.name property will not. There are a few ways around this.

easiest way is to define the property on the object on initialization, but with a value of undefined

![[vue object property undefined.png]]
most useful if you’re updating multiple properties at the same time—you can use Object.assign() to create a new object and override the only object:

Vue provides a function called Vue.set() that you can use to set reactive properties:

`Vue.set(vm.formData, 'name', 'Some User');`

**Setting items on an array**

can’t directly set items on an array by using the index. 
this wont work:
![[vue reactive caveat set array by index.png]]

two ways you can do this instead. You can use .splice() to remove the old item and add a new one:
`vm.dogs.splice(2, 1, 'Bob)`; 
Or you can use Vue.set() again: 
`Vue.set(vm.dogs, 2, 'Bob');`

**Setting the length of an array In JavaScript,** 

you can set the length of an array to either pad it to that length with empty items, or to cut off the end of the array (depending on whether the set length is more or less than the old length). You can’t do that with an array in the data object, because Vue won’t be able to detect any changes to the array.
You can use splice instead: `vm.dogs.splice(newLength);` 


