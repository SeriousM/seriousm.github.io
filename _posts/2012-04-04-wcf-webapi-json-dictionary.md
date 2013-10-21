---
layout: post
title:  "WCF &amp; WebAPI JSON Dictionary"
date:   2012-04-04 11:59:00
categories: Work DotNet
---

Imagine you want to serialize a `Dictionary<string, string>` for wcf json output.  
The JSON output would look like this:

```
    [
        {
            Key: "key1",
            Value: "value1"
        },
        {
            Key: "key2",
            Value: "value2"
        }
    ]
```

But you want a correct JSON dictionary format:

```
    {
        "key1": "value1",
        "key2": "value2"
    }
```

What happens here? Serializing a dictionary is the same as you would serialize a list of objects.

This means that this:

```
Dictionary<string, object> dic = new Dictionary<string, object>();
dic.Add("key1", "value1");
dic.Add("key2", "value2");
```

... is the same as this:

```
public class KeyValue
{
    public string Key { get; set; }
    public string Value { get; set; }
    [...]
}

public class Dictionary
{
    public List<KeyValue> Values { get; set; }
    [...]
}
```

The serializer takes every item from Dictionary.Values and writes the KeyValue object into the output.  
This behaviour is not bad or wrong but it is unsuitable for a JSON dictionary output.

What we want is a "Key: Value" output like this:
```
    {
        "key1": "value1",
        "key2": "value2"
    }
```

What you need to do is implementing a Dictionary-like object that inherits from ISerializable.

Here is the implementation of it:

```
/// <summary>
/// This key value collection is used to serialize a dictionary into json format and back.
/// </summary>
[Serializable]
public sealed class KeyValueCollection : ISerializable
{
    /// <summary>
    /// Holds the internal dictionary.
    /// </summary>
    private readonly Dictionary<string, string> _dictionary;

    /// <summary>
    /// Initializes a new instance of the <see cref="KeyValueCollection"/> class.
    /// </summary>
    public KeyValueCollection()
    {
        this._dictionary = new Dictionary<string, string>(StringComparer.InvariantCultureIgnoreCase);
    }

    /// <summary>
    /// Initializes a new instance of the <see cref="KeyValueCollection"/> class.
    /// </summary>
    /// 
    public KeyValueCollection(Dictionary<string, string> dictionary)
    {
        this._dictionary = new Dictionary<string, string>(dictionary, StringComparer.InvariantCultureIgnoreCase);
    }

    /// <summary>
    /// Initializes a new instance of the <see cref="KeyValueCollection"/> class.
    /// </summary>
    /// 
    /// 
    protected KeyValueCollection(SerializationInfo info, StreamingContext context) : this()
    {
        foreach (var entry in info)
        {
            this._dictionary.Add(entry.Name, entry.Value.ToString());
        }
    }

    /// <summary>
    /// Gets or sets the <see cref="System.String"/> with the specified key.
    /// </summary>
    public string this[string key]
    {
        get
        {
            return !this._dictionary.ContainsKey(key) ? null : this._dictionary[key];
        }
        set
        {
            this._dictionary[key] = value;
        }
    }

    /// <summary>
    /// Gets the internal dictionary as copy.
    /// </summary>
    /// <returns>The internal dictionary as copy.</returns>
    public Dictionary<string, string> GetDictionary()
    {
        return new Dictionary<string, string>(this._dictionary);
    }

    /// <summary>
    /// Populates a SerializationInfo with the data needed to serialize the target object.
    /// </summary>
    /// 
    /// 
    /// <exception cref="T:System.Security.SecurityException">The caller does not have the required permission.</exception>
    void ISerializable.GetObjectData(SerializationInfo info, StreamingContext context)
    {
        foreach (string key in this._dictionary.Keys)
        {
            info.AddValue(key, this._dictionary[key], typeof(string));
        }
    }

    /// <summary>
    /// Adds the item with the specified key.
    /// </summary>
    /// 
    /// 
    public void Add(string key, string value)
    {
        this[key] = value;
    }
}
```

Notes:

* As you might have seen that i use `Dictionary<string, string>(StringComparer.InvariantCultureIgnoreCase);`
  The `StringComparer.InvariantCultureIgnoreCase` argument helps me to treat all the keys case insensitive.

* If you want to work on the directory directly (query) use the method `GetDictionary()`.

Sources:
[http://blog.masonchu.com/2012/03/wcf-webapi-dictionary-json.html](http://blog.masonchu.com/2012/03/wcf-webapi-dictionary-json.html)
[http://stackoverflow.com](http://stackoverflow.com)