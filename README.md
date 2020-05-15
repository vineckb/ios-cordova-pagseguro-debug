## About

PagSeguroDirectPayment.onSenderHashReady has returning undefined response only on ios. On browser &  android it's working fine.

## Requirements

* xcode
* cordova & yarn installed globaly

## Steps to reproduce

```
yarn install

cd src-cordova
cordova platform add ios
cd ...

yarn cordova-build-only-www-ios && cd src-cordova && cordova build ios --prod && cordova run ios
```
