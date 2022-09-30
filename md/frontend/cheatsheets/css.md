# Cheat Sheet: useful css-tips

Change border color while hovering without bounces

```css
.el {
  border: 1px solid transparent;
}
.el:hover {
  border: 1px solid blue;
}
```

Put modal strictly at the center of the page

```css
.modal {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%,-50%);
}
```

Put element strictly at the right

```css
.el:after {
  position: relative;
}
```

Put image at the top of the container

```css
img {
  display: block;
  vertical-align: top;
}
```

Hide unnecessary text

```css
.text {
  text-overflow: ellipsis;
  white-space: nowrap;
  overflow: hidden;
}
```
