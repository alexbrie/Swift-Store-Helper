# SwiftStoreHelper
No-fluff helper classes for InAppPurchase handling in Swift 3


## How to use:
1. Copy the files in your Swift project. In the PurchasesIds.plist file, enter your IAP identifiers (the product identifiers for your in-app purchases, as defined in iTunesConnect)
2. in your AppDelegate.swift, the application:didFinishLaunchingWithOptions method, add

```swift
let _ = StoreListener.sharedInstance
```

3. in your StoreViewController.swift (or equivalent), add notification observers for the main events (I usually do this in viewWillAppear)

```swift
NotificationCenter.default.addObserver(self, selector: #selector(StoreViewController.handleProChanged(_:)), name: NSNotification.Name(rawValue: NOTIF_PURCHASED), object: nil)
NotificationCenter.default.addObserver(self, selector: #selector(StoreViewController.handleUpdated(_:)), name: NSNotification.Name(rawValue: NOTIF_RESTORED), object: nil)
```
(make sure to remove the observers when exiting the controller, such as in viewWillDisappear)

   You can now call purchase/restore with 
```swift
StoreListener.sharedInstance.purchaseProduct(PRO_VERSION_PRODUCT_ID)

StoreListener.sharedInstance.restorePurchases()
```