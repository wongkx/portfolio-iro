---
layout: post
title: BlocChat
feature-img: "img/sample_feature_img.png"
thumbnail-path: "https://d13yacurqjgara.cloudfront.net/users/3217/screenshots/2030974/bloctalk_1x.png"
short-description: BlocChat is awesome!

---
## Summary

BlocChat is a messaging application where users can send and receive to each other.

## Explanation

Users can create and manage their own user account for authentication, and open a new chat room to start sending and receiving messages.

In order to create, read and store user, message, and room information, we need to have a database that can manage these objects. Firebase is the chosen database for this project since it works nicely with Angular.js and is easy and quick to run for the first time.

## Challenges

The essential functions in this project are to be able to create and add objects. How do we store and pull user, room, and message objects, and the attributes inside each of those object?

Another challenge is storing cookies. When user refreshes the browser, we want to retain the same user account, and when user clicks on Logout, the cookie would be deleted.

## Solutions

### Cookies
For this project, I used $cookie as a dependency in Angular. The put() method can store an object like so:

{% highlight javascript %}
$cookies.put('blocChatCurrentUser', firebaseUser.email)
{% endhighlight %}

And the get() method will retrieve the cookie:

{% highlight javascript %}
var currentUser = $cookies.get('blocChatCurrentUser');
{% endhighlight %}

### Firebase
To add a new object, I used the $add(object) function. Here is an example to add a room object. The create(room) method is passed by the Controller, which is also tied to the View that initially calls the "create()" method. 

{% highlight javascript %}
    var ref = firebase.database().ref().child('rooms');
    var rooms = $firebaseArray(ref);

    return {
        create: function(room) {
            rooms.$add(room);
        }
    }
{% endhighlight %}

If user creates a room named "test", it'll be stored in Firebase:

![alt text](/img/firebase2.jpg)

However, this is easy if we are just adding an object with a single attribute (room name), what about an object with multiple attributes like Message? I didn't have much luck with $add, but push() works very nicely. 

{% highlight javascript %}
    var messageInfo = {
        userName: currentUser,
        roomId: room_Id,
        sentAt: dateStr,
        content: content
    };
    firebase.database().ref('messages').push(messageInfo);
            
{% endhighlight %}

To retrieve the object(s), you can think of this as a SQL query. Think about what property/attribute you want to search by, or what key to order by.

Adding to the challenge is linking the room's key to the message's roomID. The solution is to inject the Room and Message factories into the Home Controller, such that every new message will be tied to the currently active chat room. And when you retrieve the message, you'd retrieve by the room ID (so it can display all the messages at once when user clicks on the specific room). 

{% highlight javascript %}
    getByRoomId: function(roomId) {
        var Message = [];
        ref.orderByChild('roomId').equalTo(roomId).on('value', function(snapshot) {
            snapshot.forEach(function(childSnapshot) {
                 Message.push(childSnapshot.val());
            });
        });
        return Message;
    }
{% endhighlight %}

Keep in mind that Firebase doesn't keep rows of records, but rather key/value pairs like nodes down a tree. Without the forEach method, it might grab at the wrong level (or perhaps get nothing or even an error).

For more info, please check out:
<https://firebase.google.com/docs/database/web/read-and-write>

## Conclusion

I was pretty frustrated at the beginning with the lack of instruction. It would've been nice if someone had provided a high-level architecture of the applications, such as what controllers or factories are required, and what functions would they be responsible for. I just couldn't put the above pieces together at first, and had to chase down many examples, many of which are incongruent with the style that Bloc has intended. Nothing like steering a small fishing boat in a raging storm. But I was pleased at the end to have created a working, messaging application!
