## Tabs vs. Spaces
We currently use 4 spaces. Trailing whitespaces should be avoided.
## if/else
```swift
if [...] {
} else if [...] {
} else {
}
```

## Switch
```swift
switch([...]) {
    case [...]:
        [...]
    case [...]:
        [...]
    default:
        unreachable("this should never happen");    // if the default case should never occur - SwiftHelpers.swift
}
```

## Vars (camelCase)
```swift
var varName: TypeName
let varName: TypeName

var varName = [...]
let varName = [...]
```

## Constants (always shared with objc and imported in SwiftHelpers.swift)
```swift
let kAppGroup = HelperTools.getObjcDefinedValue(.kAppGroup)
```
Please define the values in MLConstants.h and share them with swift by updating the `MLDefinedIdentifier` enum in HelperTools.h and modifying the `getObjcDefinedValue:` in HelperTools.m
```objc
+(id) getObjcDefinedValue:(MLDefinedIdentifier) identifier
{
[...]
        case MLDefinedIdentifier_kAppGroup: return kAppGroup; break;
[...]
}
```

```objc
typedef NS_ENUM(NSUInteger, MLDefinedIdentifier) {
[...]
    MLDefinedIdentifier_kAppGroup,
[...]
};
```

## Array/Dictionary literals
```swift
return [
    MyNewObject(
        bla: "yes",
        someMore: true,
        hasToBeDefinedHere: callThisMethodFor(moreInformation:"cool data", withSolution:42)
    ),
    MyNewObject(
        bla: "no",
        someMore: false,
        hasToBeDefinedHere: callThisMethodFor(moreInformation:"uncool data", withSolution:-1)
    ),
]
```

## Order of properties and methods in `structs` or `classes`
```swift
struct SomeView: View {
    // First of all, list all @Environment vars
    @Environment(\.presentationMode) private var presentationMode
    // Then list all @State, @StateObject etc. vars
    @State var mySolution = 42
    // Then list all normal vars or let constants
    var xmppAccount: xmpp
    let seconds = 42

    // Firs methods should always be init and deinit (if existing)
    init(contact: ObservableKVOWrapper<MLContact>) {
        [...]
    }

    deinit {
        [...]
    }

    // computed properties should come next
    var accountID: NSNumber {

    }

    // then all normal functions
    func doSomething(with solution: Int = 42) {
        // do it now!
    }

    // and last but not least the body of our view (if we are writing a View at all, of course)
    var body: some View {
        Text("Hello World!")
    }
}
```

## Functions
Make sure to almost always add proper labels to your arguments to make sure the naming is in line with the objc world.
You can use @objc([...]) to rename a method for objc export.
```swift
@objc(makeAccountPickerForContacts:andCallType:)
func makeAccountPicker(for contacts: [MLContact], and callType: UInt) -> UIViewController {
```

## Translations
For now only string literals in Text() views (and very few others) are translatable. Make sure to use NSLocalizedString in all other cases!
```swift
Text("This will be translatable)
someCoolFunction("This will NOT be translatable, even if this function uses LocalizedStringKey!")
someCoolFunction(NSLocalizedString("This is translatable again", comment:"a note for our translators")
```
