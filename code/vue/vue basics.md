[[vue template, data, directives]] framework to rival jquery, helps turn this:

```
<ul class="js-items"></ul>
  <script> $(function () {
    $.get('https://example.com/items.json').then(function (data) {
    var $itemsUl = $('.js-items');
    if (!data.items.length) {
      var $noItems = $('li'); $noItems.text('Sorry, there are no items.'); $itemsUl.append($noItems);
    } else {
      data.items.forEach(function (item) {
        var $newItem = $('li'); $newItem.text(item);
        if (item.includes('blue')) {
          $newItem.addClass('is-blue');
        } $itemsUl.append($newItem);
      });
    }
  }); });
```

into this:  

```
<ul class="js-items"> 
	<li v-if="!items.length">Sorry, there are no items.</li> 
	<li v-for="item in items" : {'is-blue': item.includes('blue') }"> 
		{{ item }}
	</li>
</ul>
 
<script>
new Vue({
  el: ".js-items",
  data: { items: [] },
  created() {
    fetch("https://example.com/items.json")
      .then(res => res.json())
      .then(data => {
        this.items = data.items;
      });
  }
});
</script> 
```
1. It makes an Ajax request using[[ fetch()]]. 
2. It parses the response from [[JSON]] into a JavaScript object. 
3. It stores the downloaded items in the items data property.
That’s

Now that the items have been downloaded and stored, we can use Vue’s templating functionality to write the elements to the Docu‐
That’s all the actual logic in the code. Now that the items have been downloaded and stored, we can use Vue’s templating functionality to write the elements to the Docu‐ ment Object Model (DOM) 
