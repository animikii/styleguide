# Rails

When seeking guidance on how to design a feature, consult this guide, follow existing conventions in the codebase, or follow Rails conventions. [The API](http://api.rubyonrails.org/) is your friend.

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
* `rspec` for testing

## Defaults

Use the default configuration files in `/rails` for new projects.

## Models

Use the following format for models.

```ruby
class User

  ##
  # Constants
  #

  ##
  # Attributes
  #

  ##
  # Extensions
  #

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

end
```

### Validations

Use the new syntax for validations

```ruby
# Bad
validates_presence_of :title

# Good
validates :title, presence: true
```

## Permissions

Use [this pattern](http://rails-recipes.clearcove.ca/pages/permissions_and_user_roles.html) for doing permissions.

```ruby
module User::HasPermissions

  extend ActiveSupport::Concern

  class_methods do

    # Checks if `actor` can list these resources.
    #
    # @param actor [User]
    # @return [Boolean] true if `actor` can list these resources
    def listable_by?(actor)
      actor.is_a?(User)
    end

    # Checks if `actor` can create an instance of this resource.
    #
    # @param actor [User]
    # @return [Boolean] true if `actor` can create an instance of this resource
    def creatable_by?(actor)
      actor.is_a?(User)
    end

  end

  # Checks if `actor` can view an instance of this resource.
  #
  # @param actor [User]
  # @return [Boolean] true if `actor` can view an instance of this resource
  def viewable_by?(actor)
    actor.is_a?(User)
  end

  # Checks if `actor` can create this instance of this resource.
  #
  # @param actor [User]
  # @return [Boolean] true if `actor` can create this instance of this resource
  def creatable_by?(actor)
    actor.is_a?(User)
  end

  # Checks if `actor` can update this instance of this resource.
  #
  # @param actor [User]
  # @return [Boolean] true if `actor` can update this instance of this resource
  def updatable_by?(actor)
    actor.is_a?(User)
  end

  # Checks if `actor` can destroy this instance of this resource.
  #
  # @param actor [User]
  # @return [Boolean] true if `actor` can destroy this instance of this resource
  def destroyable_by?(actor)
    actor.is_a?(User)
  end

end

```

## Controllers

* Use [symbols](http://guides.rubyonrails.org/layouts_and_rendering.html#the-status-option) instead of numerical HTTP status codes.

### Inheritance

Each controller namespace should have a `BaseController` which all controllers in that namespace inherit from. The `BaseController` is a place to setup any objects, do permission checks, etc.

```
admin/
  base_controller.rb
  users_controller.rb
  posts_controller.rb
```

## Documentation

Often an application requires some additional documentation, such as how-to guides for performing a certain task, or development notes about a large change that occurred. Documentation like this should be stored in `doc/how_to`, and `doc/dev_notes` respectively. Prefix documents with `ymd` timestamps (i.e. `20160413_example_title.txt`). Use whatever extension makes sense, such as `.rb`, `.md`, `.sql`, `.txt`, etc.

Here's an example `doc/` folder structure.

```
doc/
  how_to/
    20100101_generate_user_report.sql
    20110101_mark_user_as_denied.rb
  dev_notes/
    20120101_transition_to_postgres.md
    20130101_reset_postgres_sequences.sql
    20140101_pci_compliance.md
```

Over time, `doc/dev_notes/` may become quite large, and contain documentation that isn't relevant to current development. When this occurs, move older documentation to `doc/dev_notes/archive` to keep the working set of documentation small and manageable.

## Mailers

* Name mailers with the `Mailer` suffix (i.e. `CommentMailer`).

## ActiveSupport

* Use Ruby 2.3's `&.` over `try`.
* Prefer Ruby's built-in methods over `ActiveSupport`s.

## Time

* Set the timezone in `config/application.rb`.
* Use `Time.current` over `Time.now`.
* Prefer the use of localizations for custom time formats over an initializer.

  In `config/locales/en.yml`, add your time formats.

  ```yaml
  en:
    time:
      formats:
        full: "%B %-d, %Y @ %-l:%M%P"
  ```

  Use the `l` or `localize` method to use the format.

  ```ruby
  # In a template, use the time format like this
  <%= l datetime_object, format: :full %>
  ```

## Testing

    Coming Soon ...

    Include this in the gem file so the spec files will be generated.

    group :test do

      gem 'database_cleaner'

    end

    group :development, :test do

      gem 'rspec-rails', '~> 3.4'
      gem "factory_girl_rails", "~> 4.0"

    end
