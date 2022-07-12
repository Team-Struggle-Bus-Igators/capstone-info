# capstone-info struggle-bus-igators

- Has requirements for capstone
- Has project details for capstone

## links etc
#### Passwords are in DMs

- GitHub Org
    - https://github.com/Team-Struggle-Bus-Igators
- Figma
    - https://www.figma.com/file/nBN6dMFT7umGBq9cHC00P9/Capstone-Wireframe?node-id=0%3A1
- Email
    - teamstrugglebusigators@gmail.com
- Trello
    - https://trello.com/b/CLjqduie/capstone-project
- Heroku 
    - firstname: Team
    - LastName: StruggleBusIgators


# Setting up environment
## Adding RSpec
- $ bundle add rspec-rails
- $ rails generate rspec:install
## Adding React
- $ bundle add webpacker
- $ bundle add react-rails
- $ rails webpacker:install
- $ rails webpacker:install:react
- $ yarn add @babel/preset-react
- $ yarn add @rails/activestorage
- $ yarn add @rails/ujs
- $ rails generate react:install
- $ rails generate react:component App
## Adding Devise
- $ bundle add devise
- $ rails generate devise:install
- $ rails generate devise User
- $ rails db:migrate

**config/environments/development.rb**
```ruby
config.action_mailer.default_url_options = { host: 'localhost', port: 3000 }
```

- Add the following:

**config/initializers/devise.rb**
```ruby
# Find this line:
config.sign_out_via = :delete
# And replace it with this:
config.sign_out_via = :get
```

### Rails Routing
- $ `rails generate controller Home`
- Add a file in *app/views/home* called *index.html.erb*
- Add the following:

**app/views/home/index.html.erb**
```html
<%= react_component 'App', {
  logged_in: user_signed_in?,
  current_user: current_user,
  new_user_route: new_user_registration_path,
  sign_in_route: new_user_session_path,
  sign_out_route: destroy_user_session_path
} %>
```

- Add the following:

**app/views/layouts/application.html.erb**
```javascript
// Find this line:
<%= javascript_importmap_tags %>

// And replace it with this:
<%= javascript_pack_tag 'application', 'data-turbolinks-track': 'reload' %>
```
- Add the following:

**config/routes.rb**
```ruby
get '*path', to: 'home#index', constraints: ->(request){ request.format.html? }
root 'home#index'
```

### React Routing
- $ `yarn add react-router-dom@5.3.0`

**app/javascript/components/App.js**
```javascript
import {
  BrowserRouter as  Router,
  Route,
  Switch
} from 'react-router-dom'
```

### Adding Reactstrap
- $ `bundle add bootstrap`
- $ `mv app/assets/stylesheets/application.css app/assets/stylesheets/application.scss`
- $ `yarn add reactstrap`

**app/assets/stylesheets/application.scss**
```css
@import 'bootstrap';
```

### Apartment Resource
The Devise User model is going to have an association with the Apartment model. In this situation, the User will have many apartments and the Apartments will belong to a User.

- $ `rails g resource Apartment street:string city:string state:string manager:string email:string price:string bedrooms:integer bathrooms:integer pets:string image:text user_id:integer`
- $ `rails db:migrate`

### User and Apartment Associations
The Apartments will belong to a User and a User will have many apartments.

**app/models/apartment.rb**
```ruby
class Apartment < ApplicationRecord
  belongs_to :user
end
```

**app/models/user.rb**
```ruby
class User < ApplicationRecord
  # Include default devise modules. Others available are:
  # :confirmable, :lockable, :timeoutable, :trackable and :omniauthable
  devise :database_authenticatable, :registerable,
         :recoverable, :rememberable, :validatable
  has_many :apartments
end
```

### Getting Started with React
To keep the files organized, it is a good practice to create three directories in your React application: assets, components, and pages.

We want to ensure the Devise data is getting to `App.js` properly. We can write some code that will be removed once we further the development process. We can destructure the values out of props and log the data.

**app/javascript/components/App.js**
```javascript
import React, { Component } from 'react'

class App extends Component {
  render() {
    const {
      logged_in,
      current_user,
      new_user_route,
      sign_in_route,
      sign_out_route
    } = this.props
    console.log("logged_in:", logged_in)
    console.log("current_user:", current_user)
    console.log("new_user_route:", new_user_route)
    console.log("sign_in_route:", sign_in_route)
    console.log("sign_out_route:", sign_out_route)
    return(
      <>
        <h1>Apartment App</h1>
      </>
    )
  }
}

export default App
```

---
