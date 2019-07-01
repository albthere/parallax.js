Parallax.js
===========

Simple parallax scrolling implemented as a jQuery plugin.  

## Installation

### NPM

```bash
npm i --save jquery-parallax.js
```

### Yarn

```bash
yarn add jquery-parallax.js
```

### Setup

Include `parallax.min.js` in your document after including jQuery (compatible with jQuery >= 1.7).

```html
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.2.1/jquery.min.js"></script>
<script src="/path/to/parallax.min.js"></script>
```

Use these CDN links, provided by jsDelivr.com
```html
<script src="https://ajax.googleapis.com/ajax/libs/jquery/1.11.0/jquery.min.js"></script>
<script src="https://cdn.jsdelivr.net/parallax.js/1.4.2/parallax.min.js"></script>
```

### Via JavaScript

To call the parallax plugin manually, simply select your target element with jQuery and do the following:

```javascript
$('.parallax-window').parallax({imageSrc: '/path/to/image.jpg'});
```

### Notes

What parallax.js will do is create a fixed-position element for each parallax image at the start of the document's body (or another configurable container). This mirror element will sit behind the other elements and match the position and dimensions of its target object.

Due to the nature of this implementation, you must ensure that these parallax objects and any layers below them are transparent so that you can see the parallax effect underneath.  Also, if there is no other content in this element, you will need to ensure that it has some fixed dimensions otherwise you won't see anything.

```css
.parallax-window {
	min-height: 400px;
	background: transparent;
}
```

Also, keep in mind that once initialized, the parallax plugin presumes a fixed page layout unless it encounters a `scroll` or `resize` event.  If you have a dynamic page in which another javascript method may alter the DOM, you must manually refresh the parallax effect with the following commands:

```javascript
jQuery(window).trigger('resize').trigger('scroll');
```

### Using inner HTML for complex content

You can use the following syntax to enable complex content for the parallax:

```html
<div class="parallax-window">
  <div class="parallax-slider">
    <span style="position:absolute; top: 400px; left: 400px;">Some Text</span>
	<p>Some other Content</p>
  </div>
</div>
```
Please note, that the div with class "parallax-slider" is essential here.

You then need to initialize it through JS and provide the naturalWidth and naturalHeight options in order to be rendered correctly.

```
$('.parallax-window').parallax({
    naturalWidth: 600,
    naturalHeight: 400
  });
```

This also makes it possible to use responsive images in the slider:

```html
<div class="parallax-window">
  <div class="parallax-slider">
    <img src="/path/to/image.jpg" srcset="/path/to/image-400px.jpg 400w, /path/to/image-800px.jpg 800w, /path/to/image-1200px.jpg 1200w" sizes="100vw">
  </div>
</div>
```

## Options

Options can be passed in via data attributes of JavaScript.  For data attributes, append the option name to `data-`, as in `data-image-src=""`.

Note that when specifying these options as html data-attributes, you should convert "camelCased" variable names into "dash-separated" lower-case names (e.g. `zIndex` would be `data-z-index=""`).

<table class="table table-bordered table-striped">
	<thead>
		<tr>
			<th style="width: 100px;">Name</th>
			<th style="width: 100px;">type</th>
			<th style="width: 50px;">default</th>
			<th>description</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>imageSrc</td>
			<td>path</td>
			<td>null</td>
			<td>You must provide a path to the image you wish to apply to the parallax effect.</td>
		</tr>
		<tr>
			<td>naturalWidth</td>
			<td>number</td>
			<td>auto</td>
			<td rowspan="2">You can provide the natural width and natural height of an image to speed up loading and reduce error when determining the correct aspect ratio of the image.</td>
		</tr>
		<tr>
			<td>naturalHeight</td>
			<td>number</td>
			<td>auto</td>
		</tr>
		<tr>
			<td>position</td>
			<td>xPos yPos</td>
			<td>center center</td>
			<td rowspan="3">This is analogous to the background-position css property. Specify coordinates as top, bottom, right, left, center, or pixel values (e.g. -10px 0px). The parallax image will be positioned as close to these values as possible while still covering the target element.</td>
		</tr>
		<tr>
			<td>positionX</td>
			<td>xPos</td>
			<td>center</td>
		</tr>
		<tr>
			<td>positionY</td>
			<td>yPos</td>
			<td>center</td>
		</tr>
		<tr>
			<td>speed</td>
			<td>float</td>
			<td>0.2</td>
			<td>The speed at which the parallax effect runs. 0.0 means the image will appear fixed in place, and 1.0 the image will flow at the same speed as the page content.</td>
		</tr>
		<tr>
			<td>zIndex</td>
			<td>number</td>
			<td>-100</td>
			<td>The z-index value of the fixed-position elements.  By default these will be behind everything else on the page.</td>
		</tr>
		<tr>
			<td>bleed</td>
			<td>number</td>
			<td>0</td>
			<td>You can optionally set the parallax mirror element to extend a few pixels above and below the mirrored element.  This can hide slow or stuttering scroll events in certain browsers.</td>
		</tr>
		<tr>
			<td>iosFix</td>
			<td>boolean</td>
			<td>true</td>
			<td>iOS devices are incompatable with this plugin. If true, this option will set the parallax image as a static, centered background image whenever it detects an iOS user agent. Disable this if you wish to implement your own graceful degradation.</td>
		</tr>
		<tr>
			<td>androidFix</td>
			<td>boolean</td>
			<td>true</td>
			<td>If true, this option will set the parallax image as a static, centered background image whenever it detects an Android user agent. Disable this if you wish to enable the parallax scrolling effect on Android devices.</td>
		</tr>
		<tr>
			<td>overScrollFix</td>
			<td>boolean</td>
			<td>false</td>
			<td>(Experimental) If true, will freeze the parallax effect when "over scrolling" in browsers like Safari to prevent unexpected gaps caused by negative scroll positions.</td>
		</tr>
		<tr>
			<td>mirrorContainer</td>
			<td>jQuery Selector</td>
			<td>body</td>
			<td>The parallax mirror will be prepended into this container.</td>
		</tr>
	</tbody>
</table>

w/The MIT License (MIT)

