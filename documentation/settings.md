---
layout: documentation
title: Settings
bodyClass: settings
---
##Image sizes
You can select which image sizes that the plugin should use from the settings page.  
These settings can be overwritten from your templates.

{% highlight php %}
<?php
// Using get_posts()
$posts = get_posts( array(
    'post_type' => 'portfolio',
    'rwp_settings' => array(
        'sizes' => array('large', 'full')
    )
) );

// Using WP_Query()
$query = new WP_Query( array(
    'category_name' => 'wordpress',
    'rwp_settings' => array(
        'sizes' => array('large', 'full')
    )
) );
if ( $query->have_posts() ) {
    // ...
}
?>
{% endhighlight %}

<h2 id="settings-sizes-attribute">Sizes attribute</h2>
<p>By default, <strong>img</strong> tags with <strong>sizes</strong> / <strong>srcset</strong> is the selected markup pattern. <strong>100vw</strong> is the default value of the <strong>sizes</strong> attribute, but it's possible to specify your own. </p>
{% highlight php %}
<?php
$posts = get_posts(array(
    'post_type' => 'portfolio',
    'rwp_settings' => array(
        'sizes' => array('medium', 'large'),
        'attributes' => array(
            'sizes' => '(min-width: 500px) 1024px, 300px'
        )
    )
));
?>
{% endhighlight %}
<p>This will produce the following:</p>
{% highlight html %}
<img srcset="medium.jpg 300w, large.jpg 1024w" sizes="(min-width: 500px) 1024px, 300px)" src="medium.jpg">
{% endhighlight %}
<p><strong>large.jpg</strong> will be selected when the window width is at least 500px. On smaller screens, <strong>medium.jpg</strong> will be selected.</p>

<h2 id="settings-media-queries">Media queries</h2>
<p>If you've selected the <strong>picture</strong> element in the settings, you can specify your own media queries for the different image sizes.</p>
{% highlight php %}
<?php
$posts = get_posts(array(
    'post_type' => 'portfolio',
    'rwp_settings' => array(
        'sizes' => array('thumbnail', 'medium', 'large'),
        'media_queries' => array(
            'medium' => 'min-width: 500px',
            'large' => 'min-width: 1024px'
        )
    )
));
?>
{% endhighlight %}
<p>In the example above, <strong>thumbnail</strong> is the smallest image size and should therefore have no media query specified.<br><strong>medium</strong> will be selected if the screen is 500 px or larger. The same goes for <strong>large</strong> if the screen is at least 1024 px.</p>
{% highlight html %}
<picture>
    <source srcset="large.jpg" media="(min-width: 1024px)">
    <source srcset="medium.jpg" media="(min-width: 500px)">
    <img srcset="thumbnail.jpg" alt="Image description">
</picture>
{% endhighlight %}