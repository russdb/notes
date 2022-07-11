tags: [[vue]] [[basics]] [[v-if]][[v-show]]

The following Vue template
```<div v-if="true">one</div>
<div v-if="false">two</div> 
```

results in the following output: 
`<div>one</div>`
Compare that to v-show, which uses CSS to show and hide the element.

The following Vue [[a - template]]
```<div v-show="true">one</div> 
<div v-show="false">two</div> 
```

results in the following output:
```<div>one</div> 
<div style="display: none">one</div>
```

1. because the inside element hidden using v-if isn’t going to be displayed, Vue doesn’t try to generate the HTML; v-if is better for hiding stuff that hasn’t loaded yet.

![[vue v-if error.png]]

error will be thrown is that Vue has attempted to execute user.name— a property of an object that doesn’t exist. The same example using v-if works just fine, because Vue doesn’t attempt to generate the inside of the element

Using v-if has a performance cost
v-show has no such cost beyond the initial setup cost.
expecting something to change frequently, v-show might be the best choice. Also, , if the element contains any images, then download the image ahead of it being displayed, meaning