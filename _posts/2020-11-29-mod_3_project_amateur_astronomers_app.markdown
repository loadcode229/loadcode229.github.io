---
layout: post
title:      "Mod 3 Project(Amateur Astronomers App)"
date:       2020-11-29 18:39:20 +0000
permalink:  mod_3_project_amateur_astronomers_app
---


What can this app do?
* Fully CRUD users, planets, moons, and comments.
* Creates planets & moons based on current_user and allows comments for planets.
* Uses neat features like Omniauth for logging in with Google and image and thumbnail gems 'carrierwave' & 'mini_magick'

I know this seems like day one Rails stuff but I gotta say. Starting my project off felt easier than expected. Then the roadblocks start forming. Could easily create and log in as a user within 20 minutes but spent days trying to successfully create planets.

HELPER METHODS ARE KEY!

Creating anything from that logged in user will need you to call these helper methods to well, help!

Now, in your `application_controller.rb`, you might have a few helper_methods similar to these: 

```
private

      def current_user
          @current_user ||= User.find_by_id(session[:user_id]) if session[:user_id]
      end

      def logged_in?
          !!current_user
      end

      def redirect_if_not_logged_in
          redirect_to '/' if !logged_in?
      end
```

Specifically, this helper_method: 

 ```
      def current_user
          @current_user ||= User.find_by_id(session[:user_id]) if session[:user_id]
      end
```

When creating a user's planet, user's post, user's recipe, etc. We need to call these helper methods to verify it is that said user creating, editing, or viewing all or that planet, post, or recipe.

So, in our controller, instead of the normal syntax in our index for example :

```
     def index
         @planets = Planet.all
		end
```

We will need to verify we are calling that current,  logged in user to then create their planet like so:

```
    def index
        @planets = current_user.planets.all
	  end
```

The same goes for our create, show, and edit methods:

```
def create
        @planet = current_user.planets.build(planet_params)
        if @planet.save
            redirect_to planets_path
        else
            render :new
        end
    end 

    def show
        @planet = current_user.planets.find_by_id(params[:id])
    end

    def edit
        @planet = current_user.planets.find_by_id(params[:id])
    end
```

Now, you should be able to create planets under that corresponding current_user and if you log into another account. You shouldn't be able to see the others posted planets.

