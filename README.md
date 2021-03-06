# JustJson

[![CI Status](http://img.shields.io/travis/fattomhk/JustJSON.svg?style=flat)](https://travis-ci.org/fattomhk/JustJSON)
[![Version](https://img.shields.io/cocoapods/v/JustJson.svg?style=flat)](https://cocoapods.org/pods/JustJson)
[![License](https://img.shields.io/cocoapods/l/JustJson.svg?style=flat)](https://cocoapods.org/pods/JustJson)
[![Platform](https://img.shields.io/cocoapods/p/JustJson.svg?style=flat)](https://cocoapods.org/pods/JustJson)

<!--
<a href="https://placehold.it/400?text=Screen+shot"><img width=200 height=200 src="https://placehold.it/400?text=Screen+shot" alt="Screenshot" /></a> -->


## Example

To run the example project, clone the repo, and run `pod install` from the Example directory first.

## Full Example
You may find an example project [here](https://github.com/fattomhk/AppStore). It uses JustJSON to parse json data to data model.

## Requirements

## Installation

### CocoaPods

[CocoaPods](http://cocoapods.org) is a dependency manager for Cocoa projects. You can install it with the following command:

```bash
$ gem install cocoapods
```

To integrate JustJson into your Xcode project using CocoaPods, specify it in your `Podfile`:

```ruby
use_frameworks!

pod 'JustJson'
```

Then, run the following command:

```bash
$ pod install
```

## Example
### Convert to Dictionary from JSON string
```swift
let dict = jsonStr.toDictionary()
```

### Convert Dictionary [String: Any] to JSON string
```swift
let jsonString = dict.toJSONStr()
```

### Get Data from Dictionary
```swift
let foo = dict[keyPath: "first.second.abc 123"] //return an optional Any
```

```swift
let foo = dict[string: "first.second.abc 123"] //return an optional String
```

```swift
let foo = dict[dict: "first.second.abc 123"] //return an optional Dictionart
```

```swift
let foo = dict[array: "first.second.abc 123"] //return an optional Array
```

### Looping
```swift
for foo in dict[arrayValue: "first.second.foos"] {
  print(foo)
}
```

### Object Mapping
Here comes a Dictionary:
```swift
userGroup = ["users": [
                [
                    "id" : "1",
                    "name" : "Apple",
                    "age" : 18
                ],
                [
                    "id" : "2",
                    "name" : "Boy",
                    "age" : 19
                ],
                [
                    "id" : "3",
                    "name" : "Cat",
                    "age" : 30
                ],
            ]
        ]
```

A User model:
```swift
struct User: JJMappable {
    var id: String?
    var name: String?
    var age: Int

    init(map: JJMapper) {
        id = map[string: "id"]
        name = map[string: "name"]
        age = map[intValue: "age"]
    }
}
```

A UserGroup model:
```swift
struct UserGroup: JJMappable {
    var users: [User]?

    init(map: JJMapper) {
        users = User.from(map[arrayValue: "users"])
    }
}
```

#### If you want to map a user
```swift
let data = userGroup[arrayValue: "users"][1] as! [String: Any]
let user: User? = User.from(data)
```

#### If you want to get users
```swift
let users: [Users]? = User.from(userGroup[arrayValue: "users"])
```

#### Nested mapping
```swift
let _userGroup = UserGroup.from(userGroup)
```



## More Exampes:
[Test case](https://github.com/fattomhk/JustJSON/blob/master/Tests/JustJsonTests.swift)

## Author

Horst Leung

## Thanks
Ole Begemann [https://oleb.net/blog/2017/01/dictionary-key-paths/]


## License

JustJson is available under the MIT license. See the LICENSE file for more info.
