# Styling your website to be responsive

## Viewport

The viewport is the part of the webpage that's currently visible to the user. Viewports vary between different devices,
as the screen size between devices also varies. For example, the viewport of a desktop monitor will be significantly larger than the viewport of
a mobile device.

The viewport can be controlled by setting a `<meta>` tag in each web page you'd like to make responsive. The following is an example of how to use this tag:

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
```

`width=device-width` sets the width of the viewport to match the width of the device. This is useful for devices (such as mobile devices) that have less width compared to the height of the device.

`initial-scale` sets the zoom factor of the viewport to the value of the scale provided. We set this to `1.0` to set it as the default zoom for the viewport when the webpage is first loaded.

## Mobile-First Design

Mobile-first design refers to the practice of designing your website for mobile devices before designing your website for desktop devices.

A good methodology for this is to design your website to work on smaller screens, and then add additional styling for larger screen resolutions via `Media Queries`.

## Media Queries

A Media query is a way to add additional CSS styling based on the given condition of the query.

The query follows the `@media` syntax, followed by the condition on which it should apply the additional CSS, followed by the additional CSS to be applied.

The following example changes the background color of the body to black
when the browser window's width is 600px or smaller.

```css
@media only screen and (max-width: 600px) {
  body {
    background-color: black;
  }
}
```

The `only` portion of the syntax is used to prevent older browsers that don't support media queries with media features from applying the styles, and does not affect modern browsers.

The `screen` specifies the media type to be used (in this example, it specifies computer screens, mobile devices, etc).

The `and` combines the media feature with the media type, which in the above example it is utilizing the `max-width` media feature.

## Images

An image's CSS can be set to scale up or down depending on the width or height of the device. This can be acheived via the following example:

```css
img {
  width: 100%;
  height: auto;
}
```

## Grid Layout

## Frameworks

## Templates

# References

- https://www.w3schools.com/css/css_rwd_intro.asp
