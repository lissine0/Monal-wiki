# Introduction
To query single values out of a complex XML stanza, we use a XML query language inspired by XPath, but **not** compatible with it.
Instead, our language, as implemented in Monal, is a strict superset of Prosody's query language as documented in [Prosody's documentation of util.stanza](https://prosody.im/doc/developers/util/stanza#stanzafind_path). This makes it possible to copy over queries from Prosody and directly use them in Monal without modification.

## The `MLXMLNode` methods
All incoming and outgoing XMPP stanzas are parsed to/from an instance of nested `MLXMLNode` elements.
This class therefore provides some methods for creating such elements as well as querying them.

### Querying a (possibly nested) `MLXMLNode`
All XML queries are implemented as an interface of `MLXMLNode` as well. For XML queries this class has three different methods:
```objc
-(NSArray*) find:(NSString* _Nonnull) queryString, ... NS_FORMAT_FUNCTION(1, 2)
-(id) findFirst:(NSString* _Nonnull) queryString, ... NS_FORMAT_FUNCTION(1, 2)
-(BOOL) check:(NSString* _Nonnull) queryString, ... NS_FORMAT_FUNCTION(1, 2)
```

`find:` will return an `NSArray` listing all results matching your query, `findFirst:` will only return the first result of your query. This should be used, if you are certain that there should only be one element matching (or none at all). `check:` can be used to determine if `find:` would return an empty `NSArray`.

