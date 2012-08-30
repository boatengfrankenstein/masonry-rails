# Masonry for Rails asset pipeline

[masonry](http://masonry.desandro.com/docs/intro.html) at [github](https://github.com/desandro/masonry)

Using fork from [masonry](https://github.com/kristianmandrup/masonry)

See more Masonry info at [masonry README](https://github.com/desandro/masonry/README.mdown)

This gem includes:

* jquery masonry
* jquery imagesLoaded
* jquery infinitescroll
* jquery event drag

For random content generation

* box maker
* loremimages

## Usage

In Gemfile

`gem 'masonry-rails'`

### CSS 

You can include stylesheets extracted from the masonry examples directly:

Manifest `application.css` file:

```css
*= require 'masonry/basic'
*= require 'masonry/centered'
*= require 'masonry/fluid'
*= require 'masonry/gutters'
*= require 'masonry/infinitescroll'
*= require 'masonry/right-to-left'
*= require 'masonry/transitions'
```

Use these stylesheets as a base in order to play around with different effects... :)

### Javascript

```javascript
// require masonry/jquery.masonry
```

Optional

```javascript
// require masonry/jquery.event-drag
// require masonry/jquery.imagesloaded.min
// require masonry/jquery.infinitescroll.min
// require masonry/modernizr-transitions
```

Content generation helpers:

```javascript
// require masonry/box-maker
// require masonry/jquery.loremimages.min
``

See examples on [masonry](http://masonry.desandro.com/docs/intro.html) or [github](https://github.com/desandro/masonry)

### Setup

We will use the _infinite scroll_ example for a full walkthrough of how to setup and use Masonry. We add the classes `transitions-enabled`and `infinite-scroll` to the container in order to enable these two effects simultaneously. Look further down in this guide to see configurations of other effects that canbe combined ;)

*Main container*

```html
<div id="container" class="transitions-enabled infinite-scroll clearfix">

  <div class="box col3">

  <div class="box col1">
    <p>Donec nec justo eget felis facilisis fermentum. Aliquam porttitor mauris sit amet orci. </p>
  </div>

  <div class="box col2">
    <p>
      <a href="http://www.flickr.com/photos/nemoorange/3319714470/" title="Whitlow's on Wilson by nemoorange, on Flickr"><img src="http://farm4.static.flickr.com/3008/3319714470_c05a5cb5a8_m.jpg" alt="Whitlow's on Wilson" /></a>
    </p>
  </div>
  ...
</div>
```

```css
#container {
  background: #FFF;
  padding: 5px;
  margin-bottom: 20px;
  border-radius: 5px;
  clear: both;
  -webkit-border-radius: 5px;
     -moz-border-radius: 5px;
          border-radius: 5px;
}

.clearfix:before, .clearfix:after { content: ""; display: table; }
.clearfix:after { clear: both; }
.clearfix { zoom: 1; }
```

Configuring the different brick sizes:

```css
.col1 { width: 80px; }
.col2 { width: 180px; }
.col3 { width: 280px; }
.col4 { width: 380px; }
.col5 { width: 480px; }

.col1 img { max-width: 80px; }
.col2 img { max-width: 180px; }
.col3 img { max-width: 280px; }
.col4 img { max-width: 380px; }
.col5 img { max-width: 480px; }
```

## Gutters

The `gutterWidth` option adds additional spacing between columns, but not on the outer sides of the container.

Example:

```javascript
$(function(){
  
  $('#container').masonry({
    itemSelector: '.box',
    columnWidth: 100,
    gutterWidth: 40
  });
  
});
```

Add class `has-gutters` to container for this effect.

## Right to left

Enable right-to-layout by setting the `isRTL` option to true.

See `masonry/right-to-left.css`

```javascript
$(function(){
  
  $('#container').masonry({
    itemSelector: '.box',
    columnWidth: 100,
    isAnimated: !Modernizr.csstransitions,
    isRTL: true
  });
  
});
```

Add class `rtl` to container for this effect ;)

## Centered

This layout is centered by setting `isFitWidth: true` and adding necessary CSS position styles `margin: 0 auto;`.

See `masonry/centered.css`

```css
.centered { margin: 0 auto; }
```

```html
<div id="container" class="transitions-enabled centered clearfix masonry">
  ...
</div>
```

```javascript
$(function(){  
  $('#container').masonry({
    itemSelector: '.box',
    columnWidth: 200,
    isAnimated: !Modernizr.csstransitions,
    isFitWidth: true
  });
  
});
```

## Fluid

For fluid or responsive layouts, where the width of the column is a percentage of the container's width, you can pass in a function for `columnWidth`.

```javascript
$('#container').masonry({
  itemSelector: '.box',
  // set columnWidth a fraction of the container width
  columnWidth: function( containerWidth ) {
    return containerWidth / 5;
  }
});
```

Use `masonry/fluid.css` for a head start!

## Animated transitions

Transitions used in examples 

Note: use `masonry/transitions.css` for a head start!

Noice the class names: `.transitions-enabled`, `masonry` and `.masonry-brick`.

```css
.transitions-enabled.masonry,
.transitions-enabled.masonry .masonry-brick {
  -webkit-transition-duration: 0.7s;
     -moz-transition-duration: 0.7s;
      -ms-transition-duration: 0.7s;
       -o-transition-duration: 0.7s;
          transition-duration: 0.7s;
}

.transitions-enabled.masonry {
  -webkit-transition-property: height, width;
     -moz-transition-property: height, width;
      -ms-transition-property: height, width;
       -o-transition-property: height, width;
          transition-property: height, width;
}

.transitions-enabled.masonry  .masonry-brick {
  -webkit-transition-property: left, right, top;
     -moz-transition-property: left, right, top;
      -ms-transition-property: left, right, top;
       -o-transition-property: left, right, top;
          transition-property: left, right, top;
}


/* disable transitions on container */
.transitions-enabled.infinite-scroll.masonry {
  -webkit-transition-property: none;
     -moz-transition-property: none;
      -ms-transition-property: none;
       -o-transition-property: none;
          transition-property: none;
}
```

Note: You can use compass and sass to auto-generate these [transitions](http://compass-style.org/reference/compass/css3/transition/) for all browser prefixes ;)

*CSS transitions*

Alternatively, you can rely on CSS3 transitions to animate layout rearrangements. Enabling transitions is recommended, as they provide for better browser performance over jQuery animation.

In your CSS, add transition styles below. The Masonry plugin will add a class of masonry to the container after the first arrangement so transitions can be applied afterward. Item elements will have a class of masonry-brick added.

*Animate via Modernizr*

To get the best of both worlds, you can use *Modernizr* to detect browser support for CSS transitions. Add the transitions styles above, then enable animated based on Modernizr’s detected support for transitions. This will allow browsers that support *CSS transitions* to use them, and browsers without support to use *jQuery animation*.

```javascript
$('#container').masonry({
  // options...
  isAnimated: !Modernizr.csstransitions
});
```

Use the [modernizr-rails](https://github.com/kristianmandrup/modernizr-rails) gem to include *Modernizr* ;)

Or simply include `masonry/modernizr-transitions` in your javascript manifest.

## Infinite scroll

Use with [infinite-scroll](https://github.com/paulirish/infinite-scroll) which is included for convenience. All credits & license rights (MIT) to Paul Irish.

```javascript
// require masonry/jquery.infinitescroll.min
```

See [infinite-scroll-jquery-plugin](http://www.infinite-scroll.com/infinite-scroll-jquery-plugin/) for configuration info.

Also see [demo](http://masonry.desandro.com/demos/infinite-scroll.html)
and [source](view-source:http://masonry.desandro.com/demos/infinite-scroll.html)


*Navigation* for infinite scroll

Put a `<nav>` under your main container. This will trigger loading the next page!

```html
<nav id="page-nav">
  <a href="../pages/2.html"></a>
</nav>
```

The link should load in a page containing elements that match `.block`

```html
<div class="box col3">
  <p>Donec nec justo eget felis facilisis fermentum. Aliquam porttitor mauris sit amet orci. Aenean dignissim pellentesque felis.</p>
  <p>Vestibulum volutpat, lacus a ultrices sagittis,</p>
  <ul>
    <li>Lacus a ultrices sagittis</li>
    <li>Democratis</li>
    <li>Plummus</li>
  </ul>
</div>
```

These will be appended at the bottom of the `#container`. If you are using search with paging, be sure to update the page counter after each load somehow.

```javascript
$(function(){
  
  var $container = $('#container');
  
  $container.imagesLoaded(function(){
    $container.masonry({
      itemSelector: '.box',
      columnWidth: 100
    });
  });
  
  $container.infinitescroll({
    navSelector  : '#page-nav',    // selector for the paged navigation 
    nextSelector : '#page-nav a',  // selector for the NEXT link (to page 2)
    itemSelector : '.box',     // selector for all items you'll retrieve
    loading: {
        finishedMsg: 'No more pages to load.',
        img: 'http://i.imgur.com/6RMhx.gif'
      }
    },
    // trigger Masonry as a callback
    function( newElements ) {
      // hide new items while they are loading
      var $newElems = $( newElements ).css({ opacity: 0 });
      // ensure that images load before adding to masonry layout
      $newElems.imagesLoaded(function(){
        // show elems now they're ready
        $newElems.animate({ opacity: 1 });
        $container.masonry( 'appended', $newElems, true ); 
      });
    }
  );
});
```

The loader should be "on top". Here the loader iscon is configured in the `loading` object as `http://i.imgur.com/6RMhx.gif`. This loader is included as an image asset at `assets/images/masonry/loader.gif`. So instead simply use: 

`img: '/assets/masonry/loader.gif'` 

Or whichever animated loader icon you want to use ;)

```css
/* Infinite Scroll loader */
#infscr-loading { 
  text-align: center;
  z-index: 100;
  position: fixed;
  left: 45%;
  bottom: 40px;
  width: 200px;
  padding: 10px;
  background: #000; 
  opacity: 0.8;
  color: #FFF;
  -webkit-border-radius: 10px;
     -moz-border-radius: 10px;
          border-radius: 10px;
}
```

### Kaminary paging

You can combine masonry infinite scroll with Kaminari using suggestions here:

[Create-Infinite-Scrolling-with-jQuery](https://github.com/amatsuda/kaminari/wiki/How-To:-Create-Infinite-Scrolling-with-jQuery)

[Sausage](https://github.com/christophercliff/sausage), used in this example is also included with this gem ;)

Stylesheets: `sausage/sausage.css`and `sausage/sausage.reset.css`

Javascript: `masonry/jquery.sausagemin.min.js`

For more see [sausage info](http://christophercliff.github.com/sausage)

Note: You need to configure Jquery UI to use sausage.

See: [railscast-endless-page](http://railscasts.com/episodes/114-endless-page-revised) for how to use endless pages with Rails using *will_paginate* gem.

### jQuery pageless

[jquery pageless](https://github.com/jney/jquery.pageless) could also be used...

The jquery pageless plugin is now provided as `masonry/jquery.pageless.min.js`. The [repo]((https://github.com/jney/jquery.pageless) demonstrates how to use pageless with Rails 3.

## Use with images

See [image demo](http://masonry.desandro.com/demos/images.html) which uses *imagesLoaded* plugin (included - see below)

## Images Loaded plugin

See [repo](http://desandro.github.com/imagesloaded/)

A jQuery plugin that triggers a callback after all the selected/child images have been loaded. Because you can't do `.load()` on cached images.

```javascript
// require masonry/jquery.imagesloaded.min
```

Also included is the [loremimages plugin](http://darsa.in/loremImages/), useful for testing purposes ;)

+ [**View contributors**](https://github.com/desandro/imagesloaded/contributors)

## Contributing to masonry-rails
 
* Check out the latest master to make sure the feature hasn't been implemented or the bug hasn't been fixed yet.
* Check out the issue tracker to make sure someone already hasn't requested it and/or contributed it.
* Fork the project.
* Start a feature/bugfix branch.
* Commit and push until you are happy with your contribution.
* Make sure to add tests for it. This is important so I don't break it in a future version unintentionally.
* Please try not to mess with the Rakefile, version, or history. If you want to have your own version, or is otherwise necessary, that is fine, but please isolate to its own commit so I can cherry-pick around it.

## Copyright

Copyright (c) 2012 Kristian Mandrup. See LICENSE.txt for
further details.

