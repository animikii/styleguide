# Rails

When seeking guidance on how to design a feature, consult this guide, follow existing conventions in the codebase, or follow Rails conventions.

## Gems

These are the gems we typically use.

* `clearance` for authentication
* `puma` as the application server
* `email_validator` for validation email addresses (included with `clearance`)
* `acts_as_tree` for modelling tree structures in `ActiveRecord`
* `acts_as_list` for modelling list structures in `ActiveRecord`
* `kaminari` for pagination
* `filterrific` for providing filter options on views
* `exception_notification` for notifying us of application errors
* `capistrano` for applicaton deployment
* `state_machines-activerecord` for modelling state machines in `ActiveRecord`
* `kramdown` for rendering Markdown
* `sidekiq` for background job processing
* `paperclip` for file attachments

## Models

Use the following format for models.

```ruby
class User

  include User::HasPermissions

  ##
  # Associations
  #

  ##
  # Validations
  #

  ##
  # Callbacks
  #

  ##
  # Scopes
  #

  ##
  # Class methods
  #

  ##
  # Instance methods
  #

protected

private

end
```

## Permissions

Use [this pattern](http://rails-recipes.clearcove.ca/pages/permissions_and_user_roles.html) for doing permissions.

```ruby
module User::HasPermissions

  extend ActiveSupport::Concern

  class_methods do

    # Checks if `actor` can list these resources.
    #
    # @return [Boolean] true if `actor` can list these resources
    def listable_by?(actor)
      actor.is_a?(User)
    end

    # Checks if `actor` can create an instance of this resource.
    #
    # @return [Boolean] true if `actor` can create an instance of this resource
    def creatable_by?(actor)
      actor.is_a?(User)
    end

  end

  # Checks if `actor` can view an instance of this resource.
  #
  # @return [Boolean] true if `actor` can view an instance of this resource
  def viewable_by?(actor)
    actor.is_a?(User)
  end

  # Checks if `actor` can create this instance of this resource.
  #
  # @return [Boolean] true if `actor` can create this instance of this resource
  def creatable_by?(actor)
    actor.is_a?(User)
  end

  # Checks if `actor` can update this instance of this resource.
  #
  # @return [Boolean] true if `actor` can update this instance of this resource
  def updatable_by?(actor)
    actor.is_a?(User)
  end

  # Checks if `actor` can destroy this instance of this resource.
  #
  # @return [Boolean] true if `actor` can destroy this instance of this resource
  def destroyable_by?(actor)
    actor.is_a?(User)
  end

end
```

## Controllers

### Inheritance

Each controller namespace should have a `BaseController` which all controllers in that namespace should inherit from. The `BaseController` is a place to setup any objects, do permission checks, etc.

```
admin/
  base_controller.rb
  users_controller.rb
  posts_controller.rb
```
