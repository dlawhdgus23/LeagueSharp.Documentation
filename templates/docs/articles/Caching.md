# Caching #
------------------------
 A cache is a component that stores data so future requests for that data can be served faster. The SDK already provides us with a simple and fast Cache.

## Uses ##
Typically for LeagueSharp projects, the only major use of caching is getting game objects in the world. You can implement your own cache with our helpful `Cache` class, or get access to pre-cached game objects by using `GameObjects` (Not to be confused with `GameObject`)

## How it Works ##
The `GameObjects` class works by subscribing to the `GameObject.OnCreate` and `GameObject.OnDelete`, and deleting/adding that game object to that types list.

## GameObjects Class ##
The `GameObjects` class has a fairly simple and robust method of getting GameObjects. You can use the `GameObjects.Get<T>()` to get the game objects of that type, or use the built in properties the class offers. 

Here's an example getting an `IEnumerable<Obj_AI_Hero>` which just contains all of the players in game.

With the `GameObjects.Get<T>()` method:

    var heroes = GameObjects.Get<Obj_AI_Hero>();

With the built in properties:

    var heroes = GameObjects.Heroes;

## Cache Class ##
It it worth noting that the Cache is an implementation of the `ObjectCache` class ([More Info](https://msdn.microsoft.com/en-us/library/system.runtime.caching.objectcache(v=vs.110).aspx)) and is just a general Cache. It can cache all types of objects, not just limited to LeagueSharp game objects. The cache class is a singleton (a design pattern that restricts the instantiation of a class to one object), the instance can be acccessed by it's `Instance` property. (`Cache.Instance`)

In this cache design, each item has a name (referred to as "key"), a value, and optionally a region name (a region in the cache). By default, if a region name is not specified, items will be placed in a default region of the cache, and other items that have the same key can override your value, causing malfunctions. **Region names are highly recommended! If you do use a region name, please make sure you use it in all of your Cache calls!** 

### AddOrGetExisting ###
The `AddOrGetExisting` does exactly what its name says. It will add an item to the cache, but if the cache already has an item in the same region with the same name, it will return the value. This is best if you're using a property.

Example(Taken from the SDK):

```
  public static string LogDirectory
  {
      get
      {
          return
              Cache.Instance.AddOrGetExisting(
                  "LogDirectory", 
                  () => Path.Combine(LeagueSharpAppData, "Logs", "CommonEx")).ToString();
      }
  }
```

Notice the `ToString()` method called. This is because **all objects in the cache are boxed (converted into the 'object' type)**. You will need to cast them back into the type you need!

### Set ###
The `Set` method simply sets the value of an item in the cache. The object does not have to be created for the set method to work.
    
    Cache.Instance.Set("Foo", "Bar", ObjectCache.InfiniteAbsoluteExpiration);
    Cache.Instance.Set("Foo", "Fighters", ObjectCache.InfiniteAbsoluteExpiration);

If you're wondering what the `ObjectCache.InfiniteAbsoluteExpiration` is, it is an expiration. If you do not wish to have your item removed you can set it to `ObjectCache.InfiniteAbsoluteExpiration` (Make sure System.Runtime.Caching is referenced) or set it to `DateTimeOffset.MaxValue` (Does not require the reference). Or better yet, use the indexer!

    Cache.Instance["Foo"] = "Bar";
    Cache.Instance["Foo"] = "Fighters";

**However, by using the indexer, you cannot set a region name!**

### TryGetValue ###
This method will *try* to get the value of key, and returns a boolean if the cache contains any item with the same key in the same region. If the cache does contain the item, its value will be set with an out argument in the TryGetValue method. **This is much faster then the `Contains` method!**

```
  object value;
  if (Cache.Instance.TryGetValue("Foo", out value))
  {
    	// Cache contains an item with a key of "Foo"!
    	// We can use value!
  }
  else
  {
      // Cache does not contain an item with a key of "Foo!"
      // We cannot use value!
  }
```




