[[vue-loader]] is a loader for [[webpack]] that allows you to write all the HTML, JavaScript, and CSS for a component in a single file.

If you have an existing webpack setup or favorite webpack template, you can install it by installing vue-loader through npm, and then adding the following to your webpack loader configuration:
```
module: { 
	loaders: [{
		test: /\.vue$/, 
		loader: 'vue',
	}, 
	// ... your other loaders ... 
	]
}
```

