# Adform Advertising SDK adapter for DFP mediation

## How to use

* First, you need to import Adform Advertising SDK to your project. 
Instructions on how to it you can find [here](https://github.com/adform/adform-ios-sdk).

* Second, you need to import static library `libAdapterAdformAdvertising.a` to your project.
Just drag the *AdformAdvertisingDFPAdapter* folder to your project.

* Then you have to configure banner or interstitial custom event in DFP interface. 
More information on how to do so you can find [here](https://developers.google.com/mobile-ads-sdk/docs/dfp/android/custom-events).
There are two very important steps when defining a custom event:

    1. You must set master tag id provided by Adform in parameter field.
    2. You must use AdformCustomEventBanner class for inline ads and 
    AdformCustomEventInterstitial class for interstitial ads (class name field).
    
That's it, you can try loading the ads now.

*(Don't worry if ads are not loading straight away, it may need some time for
DFP servers to handle newly created custom event.)*

### Passing additional parameters to Adform banners

Additionally you can pass key values and custom impression to 
mediated Adform banners. To do so you have to use `GADCustomEventExtras` class.
Create and instance of this class and set a NSDictionary with parameters.
When you are setting the extras you must make sure to use the same label as you 
set in DFP interface when creating a custom event.

NSDictionary may contain parameters for these keys:
* `kAFAKeyValuesKey` - use this key to set a NSDictionary with key value pairs.
* `kAFACustomImpressionKey` - use this key to set a NSURL with custom impression.

```objc

    DFPRequest *adRequest = [DFPRequest request];
    
    GADCustomEventExtras *extras = [GADCustomEventExtras new];
    
    NSDictionary *parameters = @{kAFAKeyValuesKey: @{@"gender": @"male", @"age": @"25"},
                                 kAFACustomImpressionKey: [NSURL URLWithString:@"http://your.custom.impression.com"]};
    [extras setExtras:parameters forLabel:@"AdformCustomEventInterstitial"];
    [adRequest registerAdNetworkExtras:extras];

```