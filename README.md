# easy-header-footer-adapter [![Release](https://jitpack.io/v/rubengees/easy-header-footer-adapter.svg)](https://jitpack.io/#rubengees/easy-header-footer-adapter) ![API](https://img.shields.io/badge/API-14%2B-blue.svg) [![CircleCI](https://circleci.com/gh/rubengees/easy-header-footer-adapter.svg?style=shield)](https://circleci.com/gh/rubengees/easy-header-footer-adapter)

Add a header and/or footer to your `RecyclerView` - the easy way.

![Sample](art/sample.gif)

You can download the latest sample app [here](https://github.com/rubengees/easy-header-footer-adapter/releases/download/3.0.0/sample-release.apk).

### Features

- Completely hassle-free. You don't have to change your existing implementation.
- Support for `LinearLayoutManager`, `GridLayoutManager` and `StaggeredGridLayoutManager`.
- `LayoutParams` of your `View`s are honoured.
- The `SpanSizeLookup` of your `GridLayoutManager` continues to work without adjustments.
- Support for stable ids.

### Include in your Project

Add this to your root `build.gradle` (usually in the root of your project):

```groovy
repositories {
    maven { url "https://jitpack.io" }
}
```

And this to your module `build.gradle` (usually in the `app` directory):

```groovy
dependencies {
    compile 'com.github.rubengees:easy-header-footer-adapter:3.0.0@aar'
}
```

If that doesn't work, look if there is a new version and the Readme was not updated yet.

### Usage

There is almost zero configuration if you already have an adapter.  
You wrap your adapter in the `EasyHeaderFooterAdapter` and set it to the `RecyclerView` like this:

```java
YourAdapter adapter = new YourAdapter();
EasyHeaderFooterAdapter easyHeaderFooterAdapter = 
                new EasyHeaderFooterAdapter(adapter);

//Always set the LayoutManager BEFORE the adapter.
recyclerView.setLayoutManager(new SomeLayoutManager());
recyclerView.setAdapter(easyHeaderFooterAdapter);
```

You can then set a `header` or `footer` through the `setHeader` and `setFooter` methods:

```java
headerFooterAdapter.setHeader(anyView);
headerFooterAdapter.setFooter(anotherView);
```

Those can be removed by setting null to the aforementioned methods:

```java
headerFooterAdapter.setHeader(null);
headerFooterAdapter.setFooter(null);
```

And that's it! Easy right?

There are a view things to look out for though.

##### Positions

If you are using the positions returned by the `ViewHolder`s `getAdapterPosition` method, you have to calculate the real position in your adapter. The method `getRealPosition` does exactly that:

```java
adapter.setCallback(new MainAdapter.MainAdapterCallback() {
    @Override
    public void onItemClick(int position) {
        int positionInYourDataSet = headerFooterAdapter.getRealPosition(position);

        // Do whatever you wanted to do with it.
    }
});
```

You can find more info on that in the [sample](sample/src/main/java/com/rubengees/easyheaderfooteradaptersample/MainActivity.java#L58).

##### ViewTypes and Ids

The following ViewTypes and IDs are used internally, so don't use them yourself:

```java
TYPE_HEADER = Integer.MIN_VALUE;
TYPE_FOOTER = Integer.MIN_VALUE + 1;
ID_HEADER = Long.MIN_VALUE;
ID_FOOTER = Long.MIN_VALUE + 1;
```

##### Changing the `LayoutManager` at runtime

As the `EasyHeaderFooterAdapter` needs to configure your `LayoutManager`, you have to reset the adapter to the `RecyclerView` if you want to change the `LayoutManager`:

```java
recycler.setLayoutManager(new YourNewLayoutManager());

// Remember, always set if after the LayoutManager
recycler.setAdapter(headerFooterAdapter);
```

### Further reading

The sample features almost all use cases. Have a look [here](sample/src/main/java/com/rubengees/easyheaderfooteradaptersample).  
You can find the JavaDoc [here](https://jitpack.io/com/github/rubengees/easy-header-footer-adapter/3.0.0/javadoc/).

### Metrics

<a href="http://www.methodscount.com/?lib=com.github.rubengees%3Aeasy-header-footer-adapter%3A3.0.0"><img src="https://img.shields.io/badge/Methods and size-83 | 10 KB-e91e63.svg"/></a>

### Contributions and contributors

A guide for contribution can be found [here](.github/CONTRIBUTING.md).
