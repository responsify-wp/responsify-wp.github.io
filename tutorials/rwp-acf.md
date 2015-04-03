---
layout: page
title: RWP + ACF
bodyClass: tutorials
---
Even as the author of Responsify WP, I think that Advanced Custom Field is The best WordPress plugin on the internet. I actually use it more than I use RWP on sites that I make. 
Because of that, I know a lot of the various ways that ACF can be used on. That's why also know how to combine ACF with RWP.

It's quite simple actually. Let's imagine a page template which has a large header image that is unique to each page. You might use the built in featured image to set the header image, or you might create a custom field. 
The custom field can be called header_image and the field type is set to image. The return type can be set to either image object or image ID. 

Let's make the image responsive with RWP:

{% highlight php %}
<?php
$header_image_id = get_field('header_image');
echo Picture::create( 'element', $header_image );
?>
{% endhighlight %}

That’s it! 
Thanks for caring about responsive images.