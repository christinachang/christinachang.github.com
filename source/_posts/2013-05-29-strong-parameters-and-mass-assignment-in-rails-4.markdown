---
layout: post
title: "Strong Parameters and Mass Assignment in Rails 4"
date: 2013-05-29 18:13
comments: true
categories: 
---

One of the new features in Rails 4.0 is "Strong Parameters" (a gem) which moves mass assignment out of the model and into the controller.

Mass assignment allows multiple attributes of a class to be assigned simultanteously upon instantiation.

Sometimes you don't want all attributes to be mass assign-able. To provide mass assignment protection, you can specify which attributes can be mass assigned using "attr_accessible" in the model.

Example:
<pre>
class User < ActiveRecord::Base
	attr_accessible :name, :email
end
</pre>

If you want to mass assign different attributes for different roles, you would specify what is attr_accessible for each role.

Example:
<pre>
class User < ActiveRecord::Base
	attr_accessible :name, :email				# default role
	attr_accessible :eat_cake, :as => :admin	# admin role
end
</pre>

There has been a lot of discussion within the community about whether mass assignment security belongs in the model layer. If an application has complex authorization requirements, adding separate code for each "role" can become cumbersome. Since the controller handles the flow between user and application including the authentication and authorization, it seems reasonable to move mass assignment protection into the controller.

DHH built the Strong Parameters gem to address this issue and as I mentioned at the beginning of the post, this feature is integrated in Rails 4.0 by default. Below is an example of how it could be implemented.

Example:
<pre>
class UsersController < ApplicationController
  
  def update
    user = User.find(params[:id])
    if user.update_attributes(user_params)
      redirect_to home_path
    else
      render :edit
    end
  end
 
  private

  def user_params
    params.require(:user).permit(:name, :email)
  end

end
</pre>

The 'require' method ensures that the specified key is available in the params hash and the 'permit' method specifies which attributes can be mass assigned.

To implement the mass assignment protection in the controller in Rails 3.2.x, you would need to install and require the Strong Parameters gem and then add the following code in addition to the code above:

In the config/application.rb file:
<pre>
	config.active_record.whitelist_attributes = false
</pre> 
or just remove the code completely.

In the model:
<pre>
	class User < ActiveRecord::Base
	  include ActiveModel::ForbiddenAttributesProtection
	end
</pre>

<ul>Additional resources:
	<li><a href="http://railscasts.com/episodes/371-strong-parameters">http://railscasts.com/episodes/371-strong-parameters</a></li>
	<li><a href="http://rubysource.com/rails-4-quick-look-strong-parameters/">http://rubysource.com/rails-4-quick-look-strong-parameters/</a></li>
	<li><a href="http://modernlegend.github.io/blog/2013/03/16/what-is-mass-assignment/">Yanik's blog post on mass assignment</a></li>
</ul>

