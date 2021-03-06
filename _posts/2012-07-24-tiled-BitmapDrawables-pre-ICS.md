---
layout: post
title: Tiled ActionBar Background in Android Prior To ICS
tags:
  - android
  - java
  - xml
comments: true
published: true
---

<p>Trying to prettify an Android app with any kind of image assets has proven to be a bit of a challenge. I'm using the excellent <a href="http://www.actionbarsherlock.com" alt="I dont't get the name">ActionBarSherlock</a> to handle the ActionBar for OS versions prior to ICS. </p>

<p>It's certainly made life much easier, but styling it left me wanting. I tried setting the Action Bar's background to a tiled image drawable: </p>

```xml
<?xml version="1.0" encoding="utf-8"?>
<bitmap xmlns:android="http://schemas.android.com/apk/res/android"
    android:src="@drawable/bg_stripe_tile"
    android:tileMode="repeat" >
</bitmap></script>
```

<p>But the repeating attribute seem to have not been recognized at all. According to <a href="http://code.google.com/p/android/issues/detail?id=15340" alt="Android bug? no!">this bug report</a> it's a problem with pre-ICS Android. The tile mode must be set in code and is not supported in the XML declaration. Example: </p>

```java
public class MyActivity extends Activity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.main);
        if (Build.VERSION.SDK_INT < Build.VERSION_CODES.ICE_CREAM_SANDWICH) {
            BitmapDrawable bg = (BitmapDrawable)getResources().getDrawable(R.drawable.bg_striped);
            bg.setTileModeXY(TileMode.REPEAT, TileMode.REPEAT);
            getSupportActionBar().setBackgroundDrawable(bg);
        }
    }
}
```

If anyone knows a better way to handle this, I'd love to know. I'm growingly increasingly hesitant to add any images anywhere in an Android project if I can avoid it.
