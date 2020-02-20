## Setup
- Fork repo
- Open fork in GitPod
- Downgrade bundler
```
gem uninstall -i /home/gitpod/.rvm/gems/ruby-2.6.3 bundler
gem install bundler --version '1.17.3'
````
## 1 Setting up new App
- Install Rails
```
gem install rails --version=4.2.10
```
- Create app skeleton
```
rails new rottenpotatoes --skip-test-unit --skip-turbolinks
```
- Downgrade SQLLite
```
gem 'sqlite3', '~> 1.3.0'
cd rottenpotatoes
bundle update
```
- Start app
```
rails server
```
- Find what routes are defined
```
rake routes
```

## 2. Create the database and initial migration
- Create the migration

```
rails generate migration create_movies
```
- Edit migration to add movies and store movie's title, rating, description, and release date. 
```
class CreateMovies < ActiveRecord::Migration
  def change
    create_table :movies do |t|
        t.string 'title'
        t.string 'rating'
        t.text 'description'
        t.datetime 'release_date'
        # Add fields that let Rails automatically keep track
        # of when movies are added or modified:
        t.timestamps
    end
  end
end
```
- Apply the migration to the development database. Rails defines a rake task for this.
```
rake db:migrate
```
- Create `Movie` model in `app/models/movie.rb`
```
class Movie < ActiveRecord::Base
end
```
- Add seed data
```
# Seed the RottenPotatoes DB with some movies.
more_movies = [
  {:title => 'Aladdin', :rating => 'G',
    :release_date => '25-Nov-1992'},
  {:title => 'When Harry Met Sally', :rating => 'R',
    :release_date => '21-Jul-1989'},
  {:title => 'The Help', :rating => 'PG-13',
    :release_date => '10-Aug-2011'},
  {:title => 'Raiders of the Lost Ark', :rating => 'PG',
    :release_date => '12-Jun-1981'}
]

more_movies.each do |movie|
  Movie.create!(movie)
end
```
- Seed the database
```
rake db:seed
```

## Add routes
- Edit config/routes.rb
```
Rails.application.routes.draw do
  resources :movies
  root :to => redirect('/movies')
end
```
- Run rake routes to see new routes
- Go to appp rootUrl/movies
- Check out log/development.log
