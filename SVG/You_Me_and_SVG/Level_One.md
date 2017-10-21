# SVG 

## Level One: Oh, the Shapes You Can Make

### 1.3 First SVG
```sh
<?xml version="1.0" encoding="utf-8"?>
<svg
     height = "340" width="340"
     xmlns="http://www.w3.org/2000/svg"
     version="1.1"> </svg>
```

### 1.4 House Icon
```sh
<?xml version="1.0" encoding="utf-8"?>
<svg version="1.1" xmlns="http://www.w3.org/2000/svg" height="340" width="340">
  <rect height="84" width="162" fill="#FBF6A7" x="90" y="198"> </rect>
</svg>
```


### 1.5 A roof
```sh
<?xml version="1.0" encoding="utf-8"?>
<svg version="1.1" xmlns="http://www.w3.org/2000/svg" height="340" width="340">
  <rect height="84" width="162" fill="#FBF6A7" x="90" y="198"/>
  <rect
        x="80"
        y = "148"
        height="56" width="184" fill="#E04E27"/>
</svg>
```

### 1.6  A chimney
```sh
<?xml version="1.0" encoding="utf-8"?>
<svg version="1.1" xmlns="http://www.w3.org/2000/svg" height="340" width="340">
  <!-- Chimney -->
  <rect height="21" width="14" fill="#FBF6A7" x="98" y="127"/>

  <!-- Chimney Topper -->
  <rect height="4" width="20" fill="#E04E27" x="95" y="123"/>

  <!-- House -->
  <rect height="84" width="162" fill="#FBF6A7" x="90" y="198"/>
  <rect height="56" width="184" fill="#E04E27" x="80" y="148"/>
</svg>
```

### 1.7  A Door
```sh
<?xml version="1.0" encoding="utf-8"?>
<svg version="1.1" xmlns="http://www.w3.org/2000/svg" height="340" width="340" style="background-color:#F6F7F7;">
  <!-- Chimney -->
  <rect height="21" width="14" fill="#FBF6A7" x="98" y="127"/>
  <rect height="4" width="20" fill="#E04E27" x="95" y="123"/>

  <!-- House -->
  <rect height="84" width="162" fill="#FBF6A7" x="90" y="198"/>
  <rect height="56" width="184" fill="#E04E27" x="80" y="148"/>

  <!-- Door -->
  <rect height="60" width="36" fill="#E04E27" x="153" y="222"/>
  <rect
        height = "8" width="2" fill="#FBF6A7" x="183" y="252"> </rect>
</svg>
```
