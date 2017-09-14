# Level Two:  Would You, Could You With a Badge?

### 2.2 Draw a circle
```sh
<?xml version="1.0" encoding="utf-8"?>
<svg version="1.1" xmlns="http://www.w3.org/2000/svg" height="340" width="340" style="background-color:#F6F7F7;">
  <!-- Bg Circle -->
  <circle cx="170" cy="170" r="162" fill="#068C70"> </circle>

  <!-- Chimney -->
  <rect x="98" y="127" fill="#FBF6A7" width="14" height="21"/>
  <rect x="95" y="123" fill="#E04E27" width="20" height="4"/>

  <!-- House -->
  <rect x="90" y="198" fill="#FBF6A7" width="162" height="84"/>
  <rect x="80" y="148" fill="#E04E27" width="184" height="56"/>

  <!-- Door -->
  <rect x="153" y="222" fill="#E04E27" width="36" height="60"/>
  <rect x="183" y="252" fill="#FBF6A7" width="2" height="8"/>
</svg>
```

### 2.3 Outer Stroke for Circle
```sh
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>You, Me & SVG</title>
</head>
<body>
  <svg version="1.1" xmlns="http://www.w3.org/2000/svg" height="340" width="340" style="background-color:#F6F7F7;">
    <!-- Bg Circle -->
    <circle cx="170" cy="170" r="162" fill="#068C70" stroke="#FFFFFF" stroke-width="15"/>

    <!-- Chimney -->
    <rect x="98" y="127" fill="#FBF6A7" width="14" height="21" />
    <rect x="95" y="123" fill="#E04E27" width="20" height="4" />

    <!-- House -->
    <rect x="90" y="198" fill="#FBF6A7" width="162" height="84" />
    <rect x="80" y="148" fill="#E04E27" width="184" height="56" />

    <!-- Door -->
    <rect x="153" y="222" fill="#E04E27" width="36" height="60" />
    <rect x="183" y="252" fill="#FBF6A7" width="2" height="8" />
  </svg>
</body>
</html>
```

### 2.4 Inline SVG - move SVG into index.html
```sh
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>You, Me & SVG</title>
</head>
<body>
  <?xml version="1.0" encoding="utf-8"?>
<svg version="1.1" xmlns="http://www.w3.org/2000/svg" height="340" width="340" style="background-color:#F6F7F7;">
  <!-- Bg Circle -->
  <circle cx="170" cy="170" r="162" fill="#068C70" stroke="#FFFFFF" stroke-width="15" />

  <!-- Chimney -->
  <rect x="98" y="127" fill="#FBF6A7" width="14" height="21" />
  <rect x="95" y="123" fill="#E04E27" width="20" height="4" />

  <!-- House -->
  <rect x="90" y="198" fill="#FBF6A7" width="162" height="84" />
  <rect x="80" y="148" fill="#E04E27" width="184" height="56" />

  <!-- Door -->
  <rect x="153" y="222" fill="#E04E27" width="36" height="60" />
  <rect x="183" y="252" fill="#FBF6A7" width="2" height="8" />
</svg>


</body>
</html>
```

### 2.5 rounding edges
```sh
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>You, Me & SVG</title>
</head>
<body>
  <svg version="1.1" xmlns="http://www.w3.org/2000/svg" height="340" width="340" style="background-color:#F6F7F7;">
    <!-- Bg Circle -->
    <circle cx="170" cy="170" r="162" fill="#068C70" stroke="#FFFFFF" stroke-width="15"/>

    <!-- Chimney -->
    <rect x="98" y="127" fill="#FBF6A7" width="14" height="21"/>
    <rect x="95" y="123" fill="#E04E27" width="20" height="4"/>

    <!-- House -->
    <rect x="90" y="198" fill="#FBF6A7" width="162" height="84"/>
    <rect x="80" y="148" fill="#E04E27" width="184" height="56"/>

    <!-- Door -->
    <rect x="153" y="222" fill="#E04E27" width="36" height="60"/>
    <rect x="153" y="218" fill="#E04E27" width="36" height="10" rx="5" ry"5"/>
    <rect x="183" y="252" fill="#FBF6A7" width="2" height="8"/>
  </svg>
</body>
</html>
```





### 2.7 Flowers gotta have a stem
```sh
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>You, Me & SVG</title>
</head>
<body>
  <svg version="1.1" xmlns="http://www.w3.org/2000/svg" height="340" width="340" style="background-color:#F6F7F7;">
    <!-- Bg Circle -->
    <circle cx="170" cy="170" r="162" fill="#068C70" stroke="#FFFFFF" stroke-width="15"/>

    <!-- Chimney -->
    <rect x="98" y="127" fill="#FBF6A7" width="14" height="21"/>
    <rect x="95" y="123" fill="#E04E27" width="20" height="4"/>

    <!-- House -->
    <rect x="90" y="198" fill="#FBF6A7" width="162" height="84"/>
    <rect x="80" y="148" fill="#E04E27" width="184" height="56"/>

    <!-- Door -->
    <rect x="153" y="222" fill="#E04E27" width="36" height="60"/>
    <rect x="153" y="218" fill="#E04E27" width="36" height="10" rx="5" ry="5"/>
    <rect x="183" y="252" fill="#FBF6A7" width="2" height="8"/>

    <!-- Flower -->
    <line x1="228" y1="267" x2="228" y2="282" stroke="#068C70" stroke-width="1"> </line>
    <circle fill="#EC7E23" cx="228" cy="267" r="6"/>
    <circle fill="#FBCE1D" cx="231" cy="266" r="2"/>
  </svg>
</body>
</html>
```

### 2.8 Adding Text to our icon
```sh
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>You, Me & SVG</title>
  <link rel="stylesheet" href="stylesheets/style.css">
</head>
<body>
  <svg version="1.1" xmlns="http://www.w3.org/2000/svg" height="340" width="340" style="background-color:#F6F7F7;">
    <!-- Bg Circle -->
    <circle cx="170" cy="170" r="162" fill="#068C70" stroke="#FFFFFF" stroke-width="15"/>

    <!-- Chimney -->
    <rect x="98" y="127" fill="#FBF6A7" width="14" height="21"/>
    <rect x="95" y="123" fill="#E04E27" width="20" height="4"/>

    <!-- House -->
    <rect x="90" y="198" fill="#FBF6A7" width="162" height="84"/>
    <rect x="80" y="148" fill="#E04E27" width="184" height="56"/>

    <!-- Door -->
    <rect x="153" y="222" fill="#E04E27" width="36" height="60"/>
    <rect x="153" y="218" fill="#E04E27" width="36" height="10" rx="5" ry="5"/>
    <rect x="183" y="252" fill="#FBF6A7" width="2" height="8"/>

    <!-- Flower -->
    <line x1="228" y1="267" x2="228" y2="282" stroke="#068C70" stroke-width="1"/>
    <circle fill="#EC7E23" cx="228" cy="267" r="6"/>
    <circle fill="#FBCE1D" cx="231" cy="266" r="2"/>

    <!-- TEXT -->
    <text x="85" y="97" font-size="70" fill="#3E9FD8" stroke="#FFFFFF" stroke-width="2" font-family="Filmotype Major">HOME</text>
  </svg>
</body>
</html>
```

### 2.10 styles
CSS
```sh
svg {
  background-color:#F6F7F7;
}
.background-circle {
  fill: #068C70;
  stroke: #FFFFFF;
  stroke-width: 15px;
}
.chimney {
  fill: #FBF6A7;
}
.chimney-topper {
  fill: #E04E27;
}
.body {
  fill: #FBF6A7;
}
.roof {
  fill: #E04E27;
}
.door {
  fill: #E04E27;
}
.door-knob {
  fill:#FBF6A7;
}
line {
  fill: #068C70;
  stroke: #068C70;
  stroke-width: 1px;
}
.flower-outer {
  fill: #EC7E23;
}
.flower-inner {
  fill: #FBCE1D;
}
text {
  font-family: Filmotype Major;
  font-size: 70px;
  fill: #3E9FD8;
  stroke: #FFFFFF;
  stroke-width: 2px;
}
```

HTML
```sh
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>You, Me & SVG</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <svg version="1.1" xmlns="http://www.w3.org/2000/svg" height="340" width="340">
    <!-- Bg Circle -->
    <circle class="background-circle" cx="170" cy="170" r="162"/>

    <!-- Chimney -->
    <rect class="chimney" x="98" y="127" width="14" height="21"/>
    <rect class="chimney-topper" x="95" y="123" width="20" height="4"/>

    <!-- House -->
    <rect class="body" x="90" y="198" width="162" height="84"/>
    <rect class="roof" x="80" y="148" width="184" height="56"/>

    <!-- Door -->
    <rect class="door" x="153" y="222" width="36" height="60"/>
    <rect class="door" x="153" y="218" width="36" height="10" rx="5" ry="5"/>
    <rect class="door-knob" x="183" y="252" width="2" height="8"/>

    <!-- Flower -->
    <line x1="228" y1="267" x2="228" y2="282"/>
    <circle class="flower-outer" cx="228" cy="267" r="6"/>
    <circle class="flower-inner" cx="231" cy="266" r="2"/>

    <!-- TEXT -->
    <text x="85" y="97">HOME</text>
  </svg>
</body>
</html>
```

### 2.11 Polygon Roof
CSS
```sh
svg {
  background-color:#F6F7F7;
}
.background-circle {
  fill: #068C70;
  stroke: #FFFFFF;
  stroke-width: 15px;
}
.chimney {
  fill: #FBF6A7;
}
.chimney-topper {
  fill: #E04E27;
}
.body {
  fill: #FBF6A7;
}
.roof {
  fill: #E04E27;
}
.door {
  fill: #E04E27;
}
.door-knob {
  fill:#FBF6A7;
}
line {
  fill: #068C70;
  stroke: #068C70;
  stroke-width: 1px;
}
.flower-outer {
  fill: #EC7E23;
}
.flower-inner {
  fill: #FBCE1D;
}
text {
  font-family: Filmotype Major;
  font-size: 70px;
  fill: #3E9FD8;
  stroke: #FFFFFF;
  stroke-width: 2px;
}
```
HTML
```sh
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>You, Me & SVG</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <svg version="1.1" xmlns="http://www.w3.org/2000/svg" height="340" width="340">
    <!-- Bg Circle -->
    <circle class="background-circle" cx="170" cy="170" r="162"/>

    <!-- Chimney -->
    <rect class="chimney" x="98" y="127" width="14" height="21"/>
    <rect class="chimney-topper" x="95" y="123" width="20" height="4"/>

    <!-- House -->
    <rect class="body" x="90" y="198" width="162" height="84"/>
    <polygon class="roof" points="256,148 262,203 80,203 87,148 327,148"> </polygon>


    <!-- Door -->
    <rect class="door" x="153" y="222" width="36" height="60"/>
    <rect class="door" x="153" y="218" width="36" height="10" rx="5" ry="5"/>
    <rect class="door-knob" x="183" y="252" width="2" height="8"/>

    <!-- Flower -->
    <line x1="228" y1="267" x2="228" y2="282"/>
    <circle class="flower-outer" cx="228" cy="267" r="6"/>
    <circle class="flower-inner" cx="231" cy="266" r="2"/>

    <!-- TEXT -->
    <text x="85" y="97">HOME</text>
  </svg>
</body>
</html>
```

### 2.12 order matters - ordering of one line and two circle elements
```sh
<?xml version="1.0" encoding="utf-8"?>
<svg width="12px" height="21px" viewBox="0 0 12 21" version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:sketch="http://www.bohemiancoding.com/sketch/ns">
  <!-- Generator: Sketch 3.4.4 (17249) - http://www.bohemiancoding.com/sketch -->
  <title>Group</title>
  <desc>Created with Sketch.</desc>
  <defs></defs>
  <g id="Page-1" stroke="none" stroke-width="1" fill="none" fill-rule="evenodd" sketch:type="MSPage">
    <g id="Group" sketch:type="MSLayerGroup">
      <line x1="6" y1="6" x2="6" y2="21" stroke="#068C70" stroke-width="1" sketch:type="MSShapeGroup"/>

      <circle id="Oval" fill="#EC7E23" sketch:type="MSShapeGroup" cx="6" cy="6" r="6"/>
      <circle id="Oval" fill="#FBCE1D" sketch:type="MSShapeGroup" cx="9" cy="5" r="2"/>
    </g>
  </g>
</svg>
```
