## Tabs vs. Spaces
We currently use 4 spaces. Trailing whitespaces should be avoided.
## if/else
```objc
if()
{
}
else if()
{
}
else
{
}
```

## Switch
```objc
switch()
{
    case 0:
        break;
    case 1:
        break;
    default:
        unreachable(); // if the default case should never occur - MLConstants.h
}
```

## Vars (camelCase)
```objc
Type* varName;
```

## Defines (UPPER_CASE)
```objc
#define SHORT_PING 16.0
```


## Functions
Use proper sounding names (should sound like a sentence with a lot of `and` and some `with` or `having`.
To rename functions for swift export, use `NS_SWIFT_NAME`
```objc
-(NSNumber*) functionNameWithName1:(ParamType1) varName1 andName2:(ParamTypeWithPtr*) varName2
{
}

//this would be named isContactBlacklisted(forEncryption:) in Swift-land if we did not use NS_SWIFT_NAME to rename it
+(BOOL) isContactBlacklistedForEncryption:(MLContact*) contact NS_SWIFT_NAME(isContactBlacklistedForEncryption(_:));
```

## Translations
```objc
NSLocalizedString(@"Some text that should be translated", @"a note for our translators");
```
