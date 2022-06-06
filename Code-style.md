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
catch()
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
```objc
-(NSNumber*) functionNameWithName1:(ParamType1) varName1 andName2:(ParamTypeWithPtr*) varName2
{
}
```

<!---
## Translations (future)
```objc
NSLocalizedString(@"UNIQUE_STRING_THAT_IDENTIFIES_THIS_STRING", @"a note for our translators");
```
-->