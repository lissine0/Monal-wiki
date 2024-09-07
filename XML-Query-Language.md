# Introduction
To query single values out of a complex XML stanza, we use a XML query language inspired by XPath, but **not** compatible with it.
Instead, our language, as implemented in Monal, is a strict superset of Prosody's query language as documented in [Prosody's documentation of util.stanza](https://prosody.im/doc/developers/util/stanza#stanzafind_path). This makes it possible to copy over queries from Prosody and directly use them in Monal without any modification.

## The `MLXMLNode` methods
All incoming and outgoing XMPP stanzas are parsed to/from an instance of nested `MLXMLNode` elements.
This class therefore provides some methods for creating such elements as well as querying them.

### Creating an `MLXMLNode`
There are several initializers for `MLXMLNode`:
```objc
-(id) initWithElement:(NSString*) element;
-(id) initWithElement:(NSString*) element andNamespace:(NSString*) xmlns;
-(id) initWithElement:(NSString*) element andNamespace:(NSString*) xmlns withAttributes:(NSDictionary*) attributes andChildren:(NSArray*) children andData:(NSString* _Nullable) data;
-(id) initWithElement:(NSString*) element withAttributes:(NSDictionary*) attributes andChildren:(NSArray*) children andData:(NSString* _Nullable) data;
-(id) initWithElement:(NSString*) element andData:(NSString* _Nullable) data;
-(id) initWithElement:(NSString*) element andNamespace:(NSString*) xmlns andData:(NSString* _Nullable) data;
```

The initializers not taking a namespace argument will create XML nodes that automatically inherit the namespace of their containing node, once added to a tree of XML nodes.

When nesting `MLXMLNode`s , it looks like this:
```objc
MLXMLNode* exampleNode = [[MLXMLNode alloc] initWithElement:@"credentials" andNamespace:@"urn:xmpp:extdisco:2" withAttributes:@{} andChildren:@[
    [[MLXMLNode alloc] initWithElement:@"service"  withAttributes:@{
        @"type": service[@"type"],
        @"host": service[@"host"],
        @"port": service[@"port"],
    } andChildren:@[] andData:nil]
] andData:nil]
```

### Querying a (possibly nested) `MLXMLNode`
All XML queries are implemented as an interface of `MLXMLNode` as well. For XML queries this class has three different methods:
```objc
-(NSArray*) find:(NSString* _Nonnull) queryString, ... NS_FORMAT_FUNCTION(1, 2)
-(id) findFirst:(NSString* _Nonnull) queryString, ... NS_FORMAT_FUNCTION(1, 2)
-(BOOL) check:(NSString* _Nonnull) queryString, ... NS_FORMAT_FUNCTION(1, 2)
```

`find:` will return an `NSArray` listing all results matching your query, `findFirst:` will only return the first result of your query. This should be used, if you are certain that there should only be one element matching (or none at all). `check:` can be used to determine if `find:` would return an empty `NSArray`.

All three methods take a string argument possibly containing `printf` style format specifiers including the `%@` specifier as supported by `NSString.stringWithFormat:` and a variable argument list for providing these format specifiers.

## The Query Language
The query language consists of a `path` followed by an optional `extraction command` and `conversion command` and is parsed by complex regular expressions in `MLXMLNode.m`. These regular expressions and the usage of the xml language throughout Monal were [security audited in 2024](https://monal-im.org/post/00011-security-audit-1/). If the following description talks about the `find:` method, the `findFirst:` and `check:` methods are automatically included.

### Path Segments
The path is built of `/`-separated segments each representing an XML node, selected by either an XML namespace or an element name or both. The XML namespace is wrapped in `{ }` and prefixes the element name. 
Each path segment is used to select all XML nodes matching the criteria listed in this path segment.
The special wildcard value `*` for element name or namespace mean "any namespace" or "any element".

If the namespace is omitted, the namespace of the parent node in the XML tree the query is acted upon is used (or `* `, if there is no parent node). The parent node is used even if the `find:` method is executed on a child XML node, see _example 1_.
The element name can not be omitted and should be set to `*` if unknown.

If the path begins with a '/' that means the following first path segment is to be used to select the node the `find:` method is called upon, if the leading `/` is omitted, the first path segment is used to select the **child nodes** the of the node the `find:`method is called upon.

#### More selection criteria
- **Not element name:**
If you want to select all XML nodes **not** having a specified name, you'll have to prefix the element name with `!`. This will negate the selection, e.g. `!text` will select all XML nodes **not** named `text`, see _example 2_.
- **Element attribute equals value**:
If you want to select XML nodes on the basis of their XML attributes, you can list those attributes as `attributeName=value`pairs each inside `< >`, see _example 3_. You can use format string specifiers in the value part of those pairs to replace those with the variadic arguments of `find:`. The order of variadic arguments has to resemble _all_ format specifiers of the complete query string given to `find:` Note: the value part of those pairs can not be omitted, use regular expression matching to select for mere XML attribute presence (e.g. `<attributeName~^.*$>`).
- **Element attribute matches regular expression**:
To select XML nodes on the basis of their XML attributes, but using a regular expression, you'll have to use `attributeName~regex` pairs inside `< >`. No format string specifiers will be repaced inside your regular expression following the `~`. You'll have to use `^` and `$` to match begin and end of the attribute string yourself, e.g. `<attributeName~.>` will match all attribute values having **at least** one character, while `<attributeName~^.$>` will match all attribute values having **exactly** one character.

Example:
```xml
<outerWrapper xmlns="
```



