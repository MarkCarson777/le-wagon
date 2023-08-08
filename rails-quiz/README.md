# Rails Quiz

## How do you create a Rails app?

> rails new my-app-name

<br />

## How do you start coding a Rails project? Give the right sequence:

> 1. Coding the models
> 2. Coding the controllers
> 3. Coding the views

This is a fundamental architectural pattern that helps organise and structure a Rails application's codebase. Often referred to as the MVC design pattern.

While the order of the components in the acronym might seem misleading, it's important to understand that the pattern's focus is on the roles and responsibilities of each component rather than their literal sequence in the name.

<br />

## How do you generate a Song model with a title and a year?

> rails generate model song title:string year:integer

<br />

## What are the 2 created files?

> db/migrate/\_create_songs.rb<br />
> app/models/song.rb

<br />

## What is the rails command you should type then?

> rails db:migrate

This applies the changes that you specified in the migration file to the database.

<br />

## How do you add a category (ex: "rock", "electro", etc...) to your songs table using the correct Rails generator?

> rails g migration add_category_to_songs

This generates a new migration file for adding a column to the 'songs' table in your Ruby on Rails application's database schema.

<br />

## What is the created file?

> db/migrate/\_add_category_to_songs.rb

<br />

## What is the rails command you should type again?

> rails db:migrate

<br />

## Add a validation on the presence of the song title in the models/song.rb file:

    class Song < ApplicationRecord
      validates :title, presence: true
    end

The **validates :title, presence: true** line specifies a validation for the **title** attribute of the **Song** model.<br />This validation ensures that the **title** attribute is present (not blank or nil) when creating or updating a **Song** record.<br />If a **Song** record is attempted to be saved without a title, the validation will prevent the save operation and add an error message to the record.

<br />

## Now crash-test your model's validation:

    ➜ rails c
    irb> let_the_music_play = Song.new
    irb> let_the_music_play.valid?
    irb> # => false
    irb> let_the_music_play.errors.messages
    irb> # => {:title=>["can't be blank"]}
    irb> let_the_music_play.title = "Let the music play"
    irb> let_the_music_play.valid?
    irb> # => true
    irb> let_the_music_play.save

1. _let_the_music_play = Song.new_: This creates a new Instance of the **Song** model named **let_the_music_play**.
2. _let_the_music_play.valid?_: This checks the validity of the **let_the_music_play** object. Since the **title** attribute is blank, the validation fails and returns **false**.
3. _let_the_music_play.errors.messages_: This returns the error messages for the **let_the_music_play** object. Since the **title** attribute is blank, the error message **"can't be blank"** is returned.
4. _let_the_music_play.title = "Let the music play"_: This sets the **title** attribute of the **let_the_music_play** object to **"Let the music play"**.
5. _let_the_music_play.valid?_: This checks the validity of the **let_the_music_play** object. Since the **title** attribute is no longer blank, the validation passes and returns **true**.
6. _let_the_music_play.save_: This saves the **let_the_music_play** object to the database.

<br />

## What is the Rails flow you need to follow again and again? Give the correct order.

> 1. Everything starts with an HTTP request<br />
> 2. The Router is routing the HTTP request to controller#action<br />
> 3. The action is getting data from models<br />
> 4. The action is rendering the view<br />

1. When a user interacts with a web application by clicking a link, submitting a form, or typing a URL into the browser, it triggers an HTTP request. The HTTP request is sent to the web server that hosts the application.
2. The web server receives the HTTP request and passes it to the Rails router. The router recognises the URL and determines which controller and action to run based on the URL.
3. The controller action receives the HTTP request and interacts with the model to retrieve data. The controller action then passes the data to the view.
4. The view renders the page as HTML and sends it back to the user's browser. The user sees the page in their browser.

<br />

## What are the 4 different parts inside an HTTP request?

> 1. Verb
> 2. URL
> 3. Headers
> 4. Body

1. The HTTP verb (also known as the HTTP method) is the type of action that the request wants the server to take. The HTTP verbs that are commonly used in a RESTful architecture are GET, POST, PUT, and DELETE.
2. The URL (also known as the endpoint) is the location where the resource that the request wants to act on can be found.
3. The headers contain additional information about the request, such as the format of the request body, the format of the response that the client is expecting, and the authentication token.
4. The body (also known as the payload) contains the data that the client wants to send to the server.

<br />

## Are the HTTP requests in the config/routes.rb associated with their 2 routes the same? Why?

> No. These two HTTP requests are not the same since they don't have the same verb.

<br />

## What's the difference between a GET and a POST request?

> A GET request is a request to get data from the server. It doesn’t have a body.<br />
> A POST request is a request to give data to the server. It has a body with the data to give to the server.

<br />

## Complete the controller code using the correct params key:

- HTTP request: GET /search?query=thriller
- Routing in config/routes.rb: get "/search" => "songs#search"

        class SongsController < ApplicationController
          def search
            @songs = Song.where(title: params[:query])
          end
        end

Inside the **search** action, this line queries the database using the **Song** model to retrieve songs with a specific **title**. The **where** method is used to filter records based on the specified conditions.<br />
In this case, it's filtering songs where the **title** matches the value provided in the **params[:query]** parameter.

<br />

## Complete the controller code using the correct params key:

- HTTP request: GET /songs/named/thriller
- Routing in config/routes.rb: get "/songs/named/:name" => "songs#search"

        class SongsController < ApplicationController
          def search
            @songs = Song.where(title: params[:name])
          end
        end

Inside the **search** action, this line queries the database using the **Song** model to retrieve songs with a specific **title**. The **where** method is used to filter records based on the specified conditions.<br />
In this case, it's filtering songs where the **title** matches the value provided in the **params[:name]** parameter.

<br />

## What are the 7 CRUD routes generated by the resources method resources :songs in Rails?

> get '/songs/new, to: 'songs#new'<br />
> post '/songs', to: 'songs#create'<br />
> get '/songs/:id', to: 'songs#show'<br />
> get '/songs', to: 'songs#index'<br />
> get '/songs/:id/edit', to: 'songs#edit'<br />
> put '/songs/:id', to: 'songs#update'<br />
> delete '/songs/:id', to: 'songs#destroy'<br />

<br />

## How do you print your routes and their URL prefix helpers?

> rails routes

When you run **rails routes** in your terminal, you'll see a table that includes information about each route, including the HTTP method, URL pattern, controller and action, and more.

<br />

## How do you generate a controller for your songs?

> rails generate controller songs

When you run rails generate controller songs, Rails will create several files and directories associated with the **SongsController**:

1. _Controller File_: A file named songs_controller.rb will be created in the app/controllers directory. This file contains the definition of the SongsController class and its actions.
2. _View Files_: A directory named songs will be created within the app/views directory.
   Inside the app/views/songs directory, view files corresponding to the actions of the controller will be created.
3. _Test Files_: Test files will be generated in the test/controllers directory or the spec/controllers directory (for RSpec) depending on your testing framework.
4. _Routes_: A route entry for the SongsController will be added to the config/routes.rb file, allowing you to define how requests to the controller's actions are routed.

<br />

## Implement the Read actions in your songs controller:

        class SongsController < ApplicationController
          def show
            @song = Song.find(params[:id])
          end

          def index
            @songs = Song.all
          end
        end

These actions demonstrate common patterns in Rails controllers.<br />The **show** action fetches a single record by its id and prepares it to be displayed in a view (e.g. a song details page).<br />The **index** action fetches a collection of records to be displayed as a list or grid (e.g. a list of all songs).

<br />

## What are the 2 requests needed to create a new song? Implement the songs#new and songs#create actions

        class SongsController < ApplicationController
          def new
            @song = Song.new
          end

          def create
            @song = Song.new(song_params)
            if @song.save
              redirect_to song_path(@song)
            else
              render :new, status: :unprocessable_entity
            end
          end

          private

          def song_params
            params.require(:song).permit(:title, :year, :category)
          end
        end

<br />

1. The **new** action instantiates a new **Song** object and assigns it to the **@song** instance variable. This is used in the view to display the form for creating a new song.
2. The **create** action instantiates a new **Song** object with the data submitted from the form. The **song_params** method is used to retrieve the data from the **params** hash and whitelist the allowed attributes.

<br />

## Why do we have to filter parameters using "strong params" in the controller?

> To avoid malicious users that could forge our forms and damage or take control of our application
> (e.g. by adding an admin = true parameter to a new user form).

<br />

## What is the HTML generated? Fill in the blanks:

- @song = Song.new

- Now what is the HTML code generated by:<br />
  <%= form_for @song do |f| %><br />
  <%= f.text_field :title %><br />
  <%= f.submit %><br />
  <% end %>

          <form action="/songs" method="post">
            <input type="text" name="song[title]" value=" ">
            <input type="submit" value="Create song">
          </form>

The code generates an HTML form that corresponds to the attributes of the **Song** model.<br /> It provides a text field for entering the title of the song and a submit button for submitting the form.<br/> When the form is submitted, the data will be sent to the appropriate controller action (such as the create action in your **SongsController**) for processing.

<br />

## What is the HTML generated? Fill in the blanks:

- @song #=> <#Song: id: 18, title: "Hey jude", year: 1968, category: "rock">

- Now what is the HTML code generated by:<br />
  <%= form_for @song do |f| %><br />
  <%= f.text_field :title %><br />
  <%= f.submit %><br />
  <% end %>

        <form action="/songs/18" method="patch">
          <input type="text" name="song[title]" value="Hey jude"/>
          <input type="submit" value="Update song"/>
        </form>

The form is set up to update a song with an id of 18 using the PATCH method. The name attribute of the input field ensures that the updated title will be included in the form data when the form is submitted. The actual updating of the song record would be handled on the server side, typically by a controller action that corresponds to the PATCH request.

<br />

## Now you want to add reviews to your app. Here are some constraints:

- We don't want our visitors to destroy or update reviews, just to create ones.
- We don't want a separate index page to list all reviews or a show page to display each review. Instead, we want to display reviews on the show page of each song, for better UX.
- Generate your Review model in the terminal. It should have only a content:string and a song: references (the foreign key)

## Generate the model:

> rails generate model review content:string song:references

## Run the migration:

> rails db:migrate

## Add validations & associations:

- Add a validation for the presence of a content
- Add associations between Review and Song

        class Song < ApplicationRecord
          has_many :reviews, dependent: :destroy # or dependent: :nullify
        end

        class Review < ApplicationRecord
          belongs_to :song
          validates :content, presence: true
        end

## Generate the reviews controller:

> rails generate controller reviews

## Add the necessary routes:

        resources :songs do
          resources :reviews, only: [:new, :create]
        end

## Now code your controller:

        class ReviewsController < ApplicationController
          before_action :set_song

          def new
            @review = Review.new
          end

          def create
            @review = Review.new(review_params)
            @review.song = @song
            if @review.save
              redirect_to song_path(@song)
            else
              render :new, status: :unprocessable_entity
            end
          end

          private

          def set_song
            @song = Song.find(params[:song_id])
          end

          def review_params
            params.require(:review).permit(:content)
          end
        end

<br />

## Add a song's reviews on its show page:

        <h1><%= @song.title %></h1>
        <p><%= @song.year %></p>
        <p><%= @song.category %></p>

        <h2>Here are the reviews for this song:</h2>
        <ul>
        <% @song.reviews.each do |review| %>
          <li><%= review.content %></li>
        <% end %>
        </ul>
