---
layout: post
title: Bloccit
feature-img: "img/bloccit.jpg"
thumbnail-path: "http://res.cloudinary.com/wongkx/image/upload/v1499960611/bloccit_qblvso.jpg"
short-description: Bloccit is awesome!

---
## Summary

Bloccit is a forum posting site where users can create, read, update, and delete posts.


## Explanation

The user can choose to create posts under the appropriate topics, which make the posts easier to read and organize.

## Challenges

Overall, I enjoy learning a lot of unfamiliar concepts, such as symbols, routes, gemfiles, creating unique Rspec tests for each CRUD operation, TDD development style, and using the console to test with live dataset.

However, some of the syntax can be difficult to get used to, especially since Ruby on Rails values "Convention over Configuration," which is not something I was immediately getting used to, because in other languages, everything has to be stated specifically, and instantiate and treated as an object. 

## Solutions

Here are some examples. The name of the controller should be plural, whereas model name should be singular.

To point to a URL path, you'd use <#Action>_path (e.g. edit_path). In some cases, you don't even need the "_path" keyword. For example, either one below should work fine:
```
<% @questions.each do |question| %>
    <%= link_to question.title, question %>
<% end %>

```
```
<% @questions.each do |question| %>
    <%= link_to question.title, questions_path(question) %>
<% end %>
```

To create a route manually, you can use something like this in the routes.rb file:
```
get 'about' => 'welcome#about'
```

I also learned to incorporate "let" and "before" for the Rspec tests. For example, 
```
let(:my_user) { User.create!(name: "BlocHead", email: "blochead@bloc.io")}
```
this will create the instance my_user in every test whether it is called or not, while "before" allows you to use it only when needed.
    

## Conclusion

I enjoy coding in Ruby on Rails a lot. It is very powerful and I understand why sometimes it is built the way it is - one of them is to type less and focus more on the important stuff!
