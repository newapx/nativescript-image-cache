# Nativescript Image Cache

[![npm version](https://badge.fury.io/js/nativescript-image-cache.svg)](https://badge.fury.io/js/nativescript-image-cache)

Nativescript image caching plugin using Fresco for Android and SDWebImageCache for iOS

## Installation 

```
tns plugin add nativescript-image-cache
```

Support NativeScript 3.0.0 with Angular

## Usage

| Property      | Value        | Default  |
| ------------- |:-------------:| --------:|
| stretch       | aspectFill, aspectFit, fill, none | none    |
| src           | image source      |       |
| placeholder   | image source      |       |

Properties
```
stretch = "aspectFill" | "aspectFit" | "fill" | "none"
src = "res://image"
placeholder = "res://placeholder"

// Android Only
placeholderStretch = "aspectFill" | "aspectFit" | "fill" | "none"
radius = "10"
rounded = "true"
```

### Initialization 

#### Nativescript Angular

```
import { initializeOnAngular } from "nativescript-image-cache";

export class AppComponent {
    constructor () {
        initializeOnAngular();
    }
}
```
After initialisation, the markup tag <NSImage></NSImage> can be used in templates of components.

```
<NSImage #myImage stretch="aspectFill" radius="20" src="res://logo">
</NSImage>
```

#### Nativescript VanillaJS/Typescript

IF on android, need to initialise the plugin before using or clearing the cache, initialisation not required for iOS**

**Initialising on android - in app.js**

```
const imageCache = require("nativescript-image-cache");
if (application.android) {
    application.on("launch", () => {
        imageCache.initialize();
    });
}
```

After initialisation, add the namespace attribute    `xmlns:IC="nativescript-image-cache"` to the opening page tag of xml. The markup tag `<IC:NSImage></IC:NSImage>` should be used to denote images.

```
<Page xmlns:IC="nativescript-image-cache">
    <GridLayout rows='*' columns='*'> 
        <IC:NSImage stretch="fill" row="0"
            col="0"  id="my-image-1" placeholder="urlToLocalPlaceholderImage" 
            src="#image-url">
            </IC:NSImage>  
    </GridLayout>
</Page>
```

### Caching Image

Default cache purge time can be specified in number of days.

```
import { setCacheLimit } from "nativescript-image-cache";

const cacheLimitInDays : number = 7;
setCacheLimit(cacheLimitInDays);
```

### Clearing Cache

Import the module, call the method `clearCache()`  , default time is for SDWebImageCache is 7 days, and for Fresco is 60 days,  after which cache is automatically cleared.

```
import { clearCache } from "nativescript-image-cache";

clearCache();
```

**for android, you need to initialize in the application onlaunch event before clearing the cache**


## Credits 
The starting point for this plugin was [this great plugin](https://github.com/VideoSpike/nativescript-web-image-cache).
