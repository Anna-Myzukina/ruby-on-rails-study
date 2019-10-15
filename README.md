# ruby-on-rails-study
useful info
### Learning Outcomes:
* [Wiki Ruby on Rails](https://ru.wikipedia.org/wiki/Ruby_on_Rails)
- What is Rails?

      Rails is a software library that extends the Ruby programming language. David Heinemeier Hansson is its creator. He gave       it the name “Ruby on Rails,” though it is often just called “Rails.”
      Rails is a framework for building websites
- What language is Rails written in?
       
       Ruby
       
        David Heinemeier Hansson, the creator of Rails, describes building an online project management application named BaseCamp in 2004. He had been using the PHP programming language because he could get things done quickly but was frustrated because of a lack of abstraction and frequently repetitive code that made PHP “dirty.” Hansson wanted to use the “clean” software enginering abstractions supported in the Java programming language but found development in Java was cumbersome. He tried Ruby and was excited about the ease of use (he calls it pleasure) he found in the Ruby language.
- Refresher: What are gems?

      The package manager that makes it easy to create and share software libraries (gems) that extend Ruby

- What are the seven gems that make up Rails?

- What is the purpose of the gemfile?

- What is the command to create a new Rails app from the command line?

- How is a GET request different from a POST request?

- What is REST?

- What is a view?

- What is a controller?

- What is a model?


![wiki](https://upload.wikimedia.org/wikipedia/commons/thumb/4/43/MVC_Scheme_ru.png/220px-MVC_Scheme_ru.png "Architecture")


## ROUTING
* What is the “Root” route?  Good article about Root route https://www.sitepoint.com/an-in-depth-look-at-basic-rails-routing/

            The root route gets called upon when a request is made to the domain name of your web application 
            depending on the rule you have stated in your routes file. Let’s say your domain name is http://test.com, 
            when someone tries to connect to it, this rule gets executed. Now what is the rule?

      The rule in your routes file can look like this:

                  #config/routes.rb

                  root to: 'welcome#index'


* What are the seven RESTful routes for a resource?

1. GET all the posts (aka “index” the posts)
2. GET just one specific post (aka “show” that post)
3. GET the page that lets you create a new post (aka view the “new” post page)
4. POST the data you just filled out for a new post back to the server so it can create that post (aka “create” the post)
5. GET the page that lets you edit an existing post (aka view the “edit” post page)
6. PUT the data you just filled out to edit the post back to the server so it can actually perform the update (aka “update” the post)
7. DELETE one specific post by sending a delete request to the server (aka “destroy” the post)

* Which RESTful routes share the same URL but use different verbs?

      get "/posts", to: "posts#index"
        get "/posts/:id", to: "posts#show"
        get "/posts/new", to: "posts#new"
        post "/posts", to: "posts#create"  # usually a submitted form
        get "/posts/:id/edit", to: "posts#edit"
        put "/posts/:id", to: "posts#update" # usually a submitted form
        delete "/posts/:id", to: "posts#destroy"
      Each of these routes is basically a Ruby method that matches that particular URL and HTTP verb with the correct controller action. Two things to notice:

      The first key thing to notice is that several of those routes submit to the SAME URL… they just use different HTTP verbs, so Rails can send them to a different controller action. That trips up a lot of beginners.
      
* How do you specify an ID or other variable in a route?

      The other thing to notice is that the “id” field is prepended by a colon… that just tells Rails “Look for 
      anything here and save it as the ID in the params hash”. It lets you submit a GET request for the first
      post and the fifth post to the same route, just a different ID:
      
        /posts/1  # going to the #show action of the PostsController
        /posts/5  # also going to the #show action of PostsController
        
      You will be able to access that ID directly from the controller by tapping into the params hash where it got stored.
* How can you easily write all seven RESTful routes in Rails?

             # in config/routes.rb
              ...
              resources :posts
              ...
* What is the Rails helper method that creates the HTML for links?

            Rails gives you a helper method that lets you create links called link_to, but you’ll need to 
            supply it with the text that you want to show and the URL to link it to.

              link_to "Edit this post", edit_post_path(3) # don't hardcode 3!
