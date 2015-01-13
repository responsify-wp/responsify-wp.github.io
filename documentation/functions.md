---
layout: documentation
title: Functions
bodyClass: functions
---
<p>If you want to generate markup for a responsive image in other places of the template, the <strong>Picture::create()</strong> function allows you to do that.</p>

<h2 id="functions-element">Element/Img</h2>
<p>Based on an attachment ID, you can generate either a <strong>picture</strong> <i>element</i> or a <i>img</i> tag with <strong>srcset</strong>/<strong>sizes</strong> attributes.</p>
{% highlight php %}
<?php echo Picture::create( 'img', $attachment_id ); ?>  
{% endhighlight %}
{% highlight php %}
<?php echo Picture::create( 'element', $attachment_id ); ?>  
{% endhighlight %}
<p>Let's say that you have the following markup for a very large header image:</p>
{% highlight php %}
<header>
    <?php the_post_thumbnail( 'full' ); ?>
</header>
{% endhighlight %}
<p>As you probably know, <strong>the_post_thumbnail()</strong> will just create a regular <strong>img</strong> tag for the full-size image in this case.<br>But you does of course not want to send a big 1440px image to a mobile device. This can easily be solved like this:</p>
{% highlight php %}
<header>
    <?php
    $thumbnail_id = get_post_thumbnail_id( $post->ID );
    echo Picture::create( 'element', $thumbnail_id );
    ?>
</header>
{% endhighlight %}
<p>You can also specify which sizes of the image that should be used:</p>
{% highlight php %}
<?php 
$thumbnail_id = get_post_thumbnail_id( $post->ID );
echo Picture::create( 'element', $thumbnail_id, array(
    'sizes' => array( 'medium', 'large', 'full' )
) ); 
?>
{% endhighlight %}
                        
<h2 id="functions-style">Style</h2>
<p>There might be times when you have a <strong>div</strong> with a very large background image. It's very easy to replace the image with a smaller one using media queries in your stylesheet, but that requires you to hard code the filename.<br>
What if it's some kind of header image that can be changed later by the administrator of the site? In that case, you cannot hard code the filename inside your stylesheet.<br>
You might have done something like this in the past:</p>
{% highlight html %}
<header id="hero" style="background-image: url(<?php echo $dynamic_header_image;?>)">
    <h1>Overlying headline</h1>
</header>
{% endhighlight %}
<p>Instead, you could do this:</p>
{% highlight php %}
<?php
echo Picture::create( 'style', $dynamic_header_image_ID, array(
    'selector' => '#hero'
) );
?>
<header id="hero">
    <h1>Overlying headline</h1>
</header>
{% endhighlight %}
<p>This will generate a <strong>style</strong> tag containing the following:</p>
{% highlight css %}
#hero {
    background-image: url("example.com/wp-content/uploads/2014/03/IMG_4540-150x150.jpg");
}
@media screen and (min-width: 150px) {
    #hero {
        background-image: url("example.com/wp-content/uploads/2014/03/IMG_4540-300x199.jpg");
    }
} 
// And so on...
{% endhighlight %}
<p>You can of course specify sizes and media queries here to.</p>
{% highlight php %}
<?php
echo Picture::create( 'style', $dynamic_header_image_ID, array(
    'selector' => '#hero',
    'sizes' => array('medium', 'large', 'full'),
    'media_queries' => array(
        'large' => 'min-width: 500px',
        'full' => 'min-width 1024px'
    )
) );
?>
{% endhighlight %}