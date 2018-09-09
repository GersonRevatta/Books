# devise + cancancan + rolify
rolify
https://github.com/RolifyCommunity/rolif
```
gem 'devise'
gem 'cancancan'
gem 'rolify'
```

  ## rails generate devise:install

  run bundle install to install all required gems

  Run Devise generator

  ## rails generate devise:install

  Create the User model from Devise

  ## rails generate devise User

  Create the Ability class from CanCanCan

  ## rails generate cancan:ability

  Create the Role class from rolify

  ## rails generate rolify Role User

  Run migrations

  ## rake db:migrate

In view
```
-if current_user.has_role?(:admin)
  %p I'm admin
```
In model ability
```
class Ability
  include CanCan::Ability

  def initialize(user)
    if user.has_role? :admin
      can :manage, :all
    else
      can :read, :all
    end
  end
end

```
and add  in models
example

```
class Link < ApplicationRecord
  resourcify #this line
end
```
Tambien , podrias tu codigo mas chido 
creando un helpers /helpers/roles_helper.rb
```
module RolesHelper
  def has_role?(role)
    current_user && current_user.has_role?(role)
  end
end
```
y en tu view solo deberias comprabar
```
- if has_role?(:admin)
```
# Note
Se le agregara el rol de administrador al user por consola
```
@user = User.find(:id)
@user.add_role "admin"
```