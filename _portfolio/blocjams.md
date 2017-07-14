---
layout: post
title: BlocJams
feature-img: "img/bloc_jams_bg.jpg"
thumbnail-path: "https://d13yacurqjgara.cloudfront.net/users/3217/screenshots/2030966/blocjams_1x.png"
short-description: BlocJams is awesome!
url: https://github.com/wongkx/BlocJams

---
## Summary

BlocJams is a simple application that allows the user to choose from a list of albums and listen to the selected song. The user is able to control the song position as well as volume control.


## Explanation

The user will not only be able to listen to any music, but also control the music, such as skip forward and volume control. For this project, the objective is to build this application with Javascript, then jQuery, and finally, Angular.js.

## Problems

With just HTML and Javascript, it wasn't too bad for creating a simple application with a few user interactivities, such as volume control and changing the song and song position.

The next challenge was to rework this into Angular.js, and be able to leverage API's that actually help to control and play the music. 

I find the most interesting problem in this project to be coding the seekbar for the music player control.


## Solutions

One of the important concepts in learning HTML is DOM (Document Object Model). DOM binding enables the application to know when user has clicked on the mouse, the position where the mouse is pressed down and where it is lifted up, etc.

To be able to console the seekbar, we need to know the position of the thumb in relative to the starting position (at 0), and the position of the starting position in relative to the left edge of the window. From there, we can calculate the percentage of how far the thumb has moved in the bar. Whenever it detects the thumb is moving, the value will change and will constantly affect other values like the volume, time position of the song, or the width of the bar filling.

Seekbar is used as an Angular Directive, which can help to make the DOM elements interactive when compiled into HTML.

{% highlight javascript %}
angular.directive('seekbar', function(){
    return {
        ...
        scope: {
            onChange: '&'
        },
        link: function(scope, element, attributes) {
            scope.value = 0;
            scope.max = 100;
            
            attributes.$observe('value', function(newValue) {
                scope.value = newValue;
            });

            attributes.$observe('max', function(newValue) {
                scope.max = newValue;
            });
            
            var seekBar = $(element);
            
            var calculatePercent = function(seekBar, event) {
                var offsetX = event.pageX - seekBar.offset().left;
                var seekBarWidth = seekBar.width();
                var offsetXPercent = offsetX / seekBarWidth;
                offsetXPercent = Math.max(0, offsetXPercent);
                offsetXPercent = Math.min(1, offsetXPercent);
                return offsetXPercent;
            };

            $document.bind('mousemove.thumb', function(event) {
                var percent = calculatePercent(seekBar, event);
                scope.$apply(function() {
                    scope.value = percent * scope.max;
                    notifyOnChange(scope.value);
                });
            });

            var notifyOnChange = function(newValue) {
                if (typeof scope.onChange === 'function') {
                    scope.onChange({value: newValue});
                }
            };
        }
    };
}
{% endhighlight %}
                    
## Results

After refactoring with jQuery and Angular.js, the user is still able to control the music player just like with plain ol' JavaScript before.


## Conclusion

In the beginning of the project, which is my very first application, I never thought it was possible to replicate something like a Spotify application without collaborating with a dozen of developers.

One of the bonus challenges was to enable the ability to create user accounts, add/remove songs, etc. However, I have not done anything with CRUD operations or integrate with any sort of database. If I have more time to make improvement, I'd take advantage of Firebase to at least allow users to create their own account, since I also reworked this into Angular style.

I definitely learned a lot about JavaScript, jQuery, and Angular with this project. There are many ways to skin a cat, but it is important to learn the basics first, like how Javascript works with HTML, or how the Angular MVC works. I also learned a few CSS concepts such as float, clear, border, padding, and margin. 

Github repository (jQuery): <https://github.com/wongkx/BlocJams>
Github repository (Angular.js): <https://github.com/wongkx/bloc-jams-angular>