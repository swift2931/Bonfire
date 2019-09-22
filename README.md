# Bonfire
Networking library for SwiftUI inspired by Siesta
![dark souls](/ds3.jpg)

### SwiftUI and Combine
You'd want 
```swift
@ObservedObject var profile = api.getUserProfile // api.getUserProfileis of ObservableObject
```
so you can do this
```swift
var body: some View {
    VStack {
        Text(profile.firstName)
        Text(profile.lastName)
        Button("refresh") {
            profile.load()
        }
    }
}
```
because SwiftUI updates view whenever @ObservedObject changes.

In old days you have to use property observer to trigger view update, now it's automatic.

For those who are familiar with [Siesta](https://github.com/bustoutsolutions/siesta), this is core Siesta built from scratch with SwiftUI and Combine features.

It is already powerful and easy to customize in its current form. This is a glimp into how networking is done with SwiftUI.

### Simplicity without dependency
Source code < 200 lines. 

I don't even bother making a repo. 

[gist here](https://gist.github.com/jimlai586/d99229b14b946aec8622511017c87b38)

Copy it to your project and customize however you want it.

### Resource-centric
Let's assume 
```swift
    var getUserProfile: Resource
```
Resource must conform to ObservableObject and manage underlying networking data, which is typically JSON.

So in SwiftUI, you naturally have resource-based networking as compared to request-based one in Alamofire. 

Instead of making requests and handle network states for each request, you start with a resource that manages network states, then let it handle request details.

This is not a new concept, Siesta has been doing this for years.

### DataTaskPublisher
While Siesta supports different networking provider like Alamofire, in practice URLSession is all you need.

Combine also makes it to URLSession, which now provides a dataTaskPublisher.

We can rewrite the netowrking provider part of Siesta using dataTaskPublisher as building blocks.

It also removes the extra complexity of networking provider abstraction and third-party Request type. 

### Network manager
I want to have some of the most frequently-used functionalities, including cache, config, decoration and overall resource management.

Currently they are not much more than placeholders, but you should be able to build them from which once you know what these do.






