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

3. Assuming the migration succeeded, update the test database's schema by running rake db:test:prepare.
4. Run your tests, and if all is well, apply the migration to the production database and deploy the new code to production. The process for applying migrations in production depends on the deployment environment; we'll do that for Heroku in a later part of the exercise.

- Add migration to add movies and store movie's title, rating, description, and release date. 

