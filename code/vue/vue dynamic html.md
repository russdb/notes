[[vue]][[vue basics]][[vue dynamic html]]

s. Vue has automatic HTML escaping built in, so if you try to write {{ yourHtml }}, the HTML characters will be escaped—it’ll look like &lt;strong&gt;this</strong> in the source—and it will appear as the HTML text sent down from the API on the page.

If you want to take HTML and display it on the page, you can use the v-html directive as follows:
`<div v-html="yourHtml"></div>`