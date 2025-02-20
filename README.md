![CalendarKit](https://user-images.githubusercontent.com/8013017/86503522-a26def80-bdb7-11ea-9610-01f3da015d33.jpg)
[![License](https://img.shields.io/cocoapods/l/CalendarKit.svg?style=flat)](http://cocoadocs.org/docsets/CalendarKit)
[![Platform](https://img.shields.io/cocoapods/p/CalendarKit.svg?style=flat)](http://cocoadocs.org/docsets/CalendarKit)
[![Version](https://img.shields.io/cocoapods/v/CalendarKit.svg?style=flat)](http://cocoadocs.org/docsets/CalendarKit)
[![SwiftPM compatible](https://img.shields.io/badge/SwiftPM-compatible-orange.svg)](#swift-package-manager) 



# CalendarKit
**CalendarKi** is a fully customizable calendar library written in Swift. It was designed to look similar to the iOS Calendar app, but allow customization if needed. To make modifications easier, CalendarKit is composed of multiple small modules. They can be used together, or on their own.


## Need Help?
If you have a **programming question** about how to use CalendarKit in your application, ask it on StackOverflow using the [CalendarKit](https://stackoverflow.com/questions/tagged/calendarkit) tag.

Please, use [GitHub Issues](https://github.com/richardtop/CalendarKit/issues) only for reporting a **bug** or requesting a new **feature** in the library.


## Demo
You can try CalendarKit with CocoaPods. Just enter in Terminal:
```ruby
pod try CalendarKit
```
[Watch demo video](https://streamable.com/zsnu1)

[Try it live in your browser](https://appetize.io/app/k85kqpdr1fp79e59f1c4ar8cx4)



## Installation
### Swift Package Manager (Xcode 11 or higher)

The preferred way of installing CalendarKit is via the [Swift Package Manager](https://swift.org/package-manager/).

>Xcode 11 integrates with libSwiftPM to provide support for iOS, watchOS, and tvOS platforms.

1. In Xcode, open your project and navigate to **File** → **Swift Packages** → **Add Package Dependency...**
2. Paste the repository URL (`https://github.com/richardtop/CalendarKit.git`) and click **Next**.
3. For **Rules**, select **Branch** (with branch set to `master`).
4. Click **Finish**.

A more detailed guide can be found here: [Adding Package Dependencies to Your App](https://developer.apple.com/documentation/swift_packages/adding_package_dependencies_to_your_app)

### CocoaPods

To install it, add the following line to your Podfile:

```ruby
pod 'CalendarKit'
```


## Usage
Subclass DayViewController and implement `DayViewDataSource` protocol to show events.
CalendarKit requires `DayViewDataSource` to return an array of objects conforming to `EventDescriptor` protocol, specifying all the information needed to display a particular event:

```swift
// Return an array of EventDescriptors for particular date
override func eventsForDate(_ date: Date) -> [EventDescriptor] {
  var models = // Get events (models) from the storage / API

  var events = [Event]()

  for model in models {
      // Create new EventView
      let event = Event()
      // Specify StartDate and EndDate
      event.startDate = model.startDate
      event.endDate = model.endDate
      // Add info: event title, subtitle, location to the array of Strings
      var info = [model.title, model.location]
      info.append("\(datePeriod.beginning!.format(with: "HH:mm")) - \(datePeriod.end!.format(with: "HH:mm"))")
      // Set "text" value of event by formatting all the information needed for display
      event.text = info.reduce("", {$0 + $1 + "\n"})
      events.append(event)
  }
  return events
}
```
There is  no need to do layout, CalendarKit will take care of it. CalendarKit also creates `EventViews` for you and reuses them.

If needed, implement DayViewDelegate to handle user input

```swift
override func dayViewDidSelectEventView(_ eventview: EventView) {
  print("Event has been selected: \(eventview.data)")
}

override func dayViewDidLongPressEventView(_ eventView: EventView) {
  print("Event has been longPressed: \(eventView.data)")
}
```

## Localization
CalendarKit supports localization and uses iOS default locale to display month and day names. First day of the week is also selected according to iOS locale. Here are few examples:


<img src="https://cloud.githubusercontent.com/assets/8013017/22315567/8ba5f9c2-e378-11e6-860d-b94e87a2a45c.PNG" alt="German" width="320"><img src="https://cloud.githubusercontent.com/assets/8013017/22315600/c87e826a-e378-11e6-9280-732982b42077.PNG" alt="Norwegian" width="320"><img src="https://cloud.githubusercontent.com/assets/8013017/22315259/bda72b46-e376-11e6-8d0b-20cb5fa2dc95.png" alt="Finnish" width="320">


## Styles
CalendarKit's look can be easily customized. The steps needed for customizations are as follows:

1. Create a new `CalendarStyle` object (or copy existing one)
2. Change style by updating the properties.
3. Invoke `updateStyle` method with the new `CalendarStyle`.


```Swift
let style = CalendarStyle()
style.backgroundColor = UIColor.black
dayView.updateStyle(style)
```
<img src="https://cloud.githubusercontent.com/assets/8013017/22717896/a2a6c6f2-edae-11e6-8ac3-d9add3d61fb9.png" alt="Light theme" width="320"> <img src="https://user-images.githubusercontent.com/8013017/69188457-3dfe6880-0b25-11ea-9674-39b9f3c1cd00.png" alt="Dark theme" width="320"> 

## Requirements

- iOS 9.0+
- Swift 4+ (Library is written in Swift 5)

## Dependencies
- **[DateTools](https://github.com/MatthewYork/DateTools)** is used for date manipulation

## Contributing
The list of features currently in development can be viewed on the [issues](https://github.com/richardtop/CalendarKit/issues) page.

Before contributing, please review [guidelines and code style](https://github.com/richardtop/CalendarKit/blob/master/CONTRIBUTING.md).
## Author

Richard Topchii

## License

**CalendarKit** is available under the MIT license. See the LICENSE file for more info.
