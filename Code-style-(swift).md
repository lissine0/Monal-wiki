## Tabs vs. Spaces
We currently use 4 spaces. Trailing whitespaces should be avoided.

## if/else
Don't use parentheses around the if condition like you would in ObjC. Parentheses are okay if you use them to make multi-line conditions more readable.
```swift
if true == true or false == false {
} else if (
    some == other or
    true == false or
    isThisTrue()
) {
} else {
}

// don't use an else branch if not needed because the if branch already returns
// but: use guard statements if checking for some abort condition
// to make clear that these are abort conditions
if someThing {
    return
}
return
```

## Guard statements
Use a guard statement instead of if/else to handle errors/abort conditions to not increase the indentation level
and make clear that these are abort conditions
```swift
guard let result = somethingThatCouldBeNil() else {
    return
}
print(result)
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

## Vars and Constants (camelCase)
```swift
var varName: TypeName
let varName: TypeName

var varName = [...]
let varName = [...]
```

## Global Constants (always defined within ObjC and imported into Swift by SwiftHelpers.swift)
Please define the values in `MLConstants.h` and share them with Swift by updating the `MLDefinedIdentifier` `enum` in `HelperTools.h` and modifying the `getObjcDefinedValue:` in `HelperTools.m`
```objc
typedef NS_ENUM(NSUInteger, MLDefinedIdentifier) {
[...]
    MLDefinedIdentifier_kAppGroup,
[...]
};
```
```objc
+(id) getObjcDefinedValue:(MLDefinedIdentifier) identifier
{
[...]
        case MLDefinedIdentifier_kAppGroup: return kAppGroup; break;
[...]
}
```
Then import them into Swift-land inside `SwiftHelpers.swift`
```swift
let kAppGroup = HelperTools.getObjcDefinedValue(.kAppGroup)
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

## View modifiers
```swift
// indent view modifiers below the view in question (and don't put them into the same line!)
Text("Hello World!")
    .font(.largeTitle)
    .foregroundColor(.primary)

// don't indent when coming after a closing "}" (but still use a new line!)
Button {
}
.font(.largeTitle)
.foregroundColor(.primary)
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
