![React Native Map Link](.github/banner.svg)

[![GitHub release](https://img.shields.io/github/release/includable/react-native-map-link.svg)](https://github.com/includable/react-native-map-link/releases)
[![npm](https://img.shields.io/npm/dm/react-native-map-link.svg)](https://www.npmjs.com/package/react-native-map-link)
[![GitHub license](https://img.shields.io/github/license/includable/react-native-map-link.svg)](https://github.com/includable/react-native-map-link/blob/master/LICENSE) [![Greenkeeper badge](https://badges.greenkeeper.io/leanmotherfuckers/react-native-map-link.svg)](https://greenkeeper.io/)

---

An easy way to open a location in a map app of the user's choice, based on the apps they have installed
on their device.

Currently supported apps:

* Apple Maps – `apple-maps`
* Google Maps – `google-maps`
* Citymapper – `citymapper`
* Uber – `uber`
* Lyft – `lyft`
* The Transit App – `transit`
* Waze – `waze`
* Yandex.Navi – `yandex`
* Moovit – `moovit`
* Yandex Maps – `yandex-maps`



## Installation

### 1. Install the package

```shell
npm i -S react-native-map-link         # or yarn add react-native-map-link
```

### 2. Update your Info.plist
To allow your app to detect if any of the directions apps are installed, an extra step is required on iOS. Your app needs to provide the `LSApplicationQueriesSchemes` key inside `ios/Info.plist` to specify the URL schemes with which the app can interact.

Just put this in your `Info.plist` depending on which apps you'd like to support. Omitting these might mean that the library can't detect some of the maps apps installed by the user.

```xml
<key>LSApplicationQueriesSchemes</key>
<array>
    <string>comgooglemaps</string>
    <string>citymapper</string>
    <string>uber</string>
    <string>lyft</string>
    <string>transit</string>
    <string>waze</string>
    <string>yandexnavi</string>
    <string>moovit</string>
    <string>yandexmaps</string>
</array>
```

Using Expo? [Read the instructions](docs/expo.md) to make it work on iOS.



## Usage

### Easiest way: action sheet

Using the `showLocation` function will shown an action sheet on iOS and an alert on Android, without any custom styling:

```js
import { showLocation } from 'react-native-map-link'

showLocation({
    latitude: 38.8976763,
    longitude: -77.0387185,
    sourceLatitude: -8.0870631,  // optionally specify starting location for directions
    sourceLongitude: -34.8941619,  // not optional if sourceLatitude is specified
    title: 'The White House',  // optional
    googleForceLatLon: false,  // optionally force GoogleMaps to use the latlon for the query instead of the title
    googlePlaceId: 'ChIJGVtI4by3t4kRr51d_Qm_x58',  // optionally specify the google-place-id
    dialogTitle: 'This is the dialog Title', // optional (default: 'Open in Maps')
    dialogMessage: 'This is the amazing dialog Message', // optional (default: 'What app would you like to use?')
    cancelText: 'This is the cancel button text', // optional (default: 'Cancel')
    appsWhiteList: ['google-maps'] // optionally you can set which apps to show (default: will show all supported apps installed on device)
    // app: 'uber'  // optionally specify specific app to use
})
```

Notes:

* The `sourceLatitude/sourceLongitude` options only work if you specify both. Currently supports all apps except Waze.


### Alternative: styled popup

Alternatively, it is possible to use a styled popup that displays icons in the app list:

![Popup](https://i.imgflip.com/2avtml.gif)

To use the library in that way, you can import the `Popup` component:

```js
import { Popup } from 'react-native-map-link';

<Popup
    isVisible={this.state.isVisible}
    onCancelPressed={() => this.setState({ isVisible: false })}
    onAppPressed={() => this.setState({ isVisible: false })}
    onBackButtonPressed={() => this.setState({ isVisible: false })}
    modalProps={{ // you can put all react-native-modal props inside.
        animationIn: 'slideInUp'
    }}
    appsWhiteList={[ /* Array of apps (apple-maps, google-maps, etc...) that you want
    to show in the popup, if is undefined or an empty array it will show all supported apps installed on device.*/ ]}
    options={{ /* See `showLocation` method above, this accepts the same options. */ }}
    style={{ /* Optional: you can override default style by passing your values. */ }}
/>
```

The Popup component uses <a href="https://github.com/react-native-community/react-native-modal">react-native-modal</a>. So you can pass all react-native-modal properties inside "modalProps" to modify styling and animations.

Also, you can customize the styling of the popup by passing an object like this in the `style` prop of the `Popup` component:

```js
{
    container: {},
    itemContainer: {},
    image: {},
    itemText: {},
    headerContainer: {},
    titleText: {},
    subtitleText: {},
    cancelButtonContainer: {},
    cancelButtonText: {},
    separatorStyle: {},
    activityIndicatorContainer: {}
}
```


## More information

* [Using this library with Expo](docs/expo.md)
* [Adding support for new maps apps](docs/add-app.md)


## Authors

This library is developed by [Includable](https://includable.com/), a creative app and web platform
development agency based in Amsterdam, The Netherlands.

* Thomas Schoffelen, [@tschoffelen](https://twitter.com/tschoffelen)


## Credits

This library is loosely based on [CMMapLauncher](https://github.com/citymapper/CMMapLauncher), ported to React Native for your pleasure and convenience.

Contributors:

* Johan le Roch, [@JohnLrDev](https://twitter.com/JohnLrDev)
