## Tabs vs. Spaces
We currently use 4 Spaces

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
    case: 0
        break;
    case: 1
        break;
    default:
        unreachable(); // if the default case should never occur - MLDefinitions.h
}
```

## Vars
```objc
Type* varName;
```

## Functions
```objc
-(NSNumber*) functionNameWithName1:(ParamType1) varName1 andName2:(ParamTypeWithPtr*) varName2
{
}
```

## Translations (future)
```objc
NSLocalizedString(@"UNIQUE_STRING_THAT_IDENTIFIES_THIS_STRING", @"a note for our translators");
```