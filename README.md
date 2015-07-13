Ghost blog infinite scroll
==========================


Just an infinite scroll for ghost blog using jquery


Open your default.hbs and before ```</body>``` put the code:

```javascript
    <script>
    var max_pages = parseInt('{{pagination.pages}}');
    </script>
```


Now create an archive named infinitescroll.js in your assets folder.
open it and put the code:

```javascript
$().ready(function(){
  $('.pagination').hide();
    var page = 2;
    var url_blog = window.location;
    $(window).scroll(function() {
    if($(window).scrollTop() + $(window).height() == $(document).height()) {
      $.get((url_blog +'/page/'+page),
      function(content) {
        if(page <= max_pages){
        $('.posts-section').append($(content).find(".post"));
        page = page + 1;
      }
    });
   }
 });
});
```
Open the default.hbs again and import the infinitescroll.js

```html
<script type="text/javascript" src="{{asset "js/infinitescroll.js"}}"></script>
```

#NOTES
1. In order to have the new posts loaded before the footer tag, I had to add a `<div class="posts-section">` to the markup on both index and author templates for my theme. You might not need this, but then update the corresponding section in the code above to reflect the markup on your theme.

2. The plugin won't work on a standard (Casper) installation of ghost, I had to modify it for my theme. Refer to the original project if or drop me a line if you want help setting it for yours.

3. This plugin was forked from https://github.com/z0pe/ghost-blog-infinite-scroll - many thanks to the author!
