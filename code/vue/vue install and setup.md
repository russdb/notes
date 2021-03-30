don’t need any special tools to install Vue

most basic app:
```
<div id="app"></div>

<script src="https://unpkg.com/vue"></script> 
<script> 
new Vue({ el: '#app', created() {
  // This code will run on startup 
  } 
}); 
</script>
```

1. , there is a div with the ID app, which is where we’re going to initiate Vue onto
downloading the CDN version of Vue onto our page.
2. some JavaScript of our own, which creates a new instance of Vue with the el property set pointing at the div previously mentioned.

works great on simple pages, but with anything more complicated, you probably want to use a bundler such as [[webpack]] or [[snowpack]]
