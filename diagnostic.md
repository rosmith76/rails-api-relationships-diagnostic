# Rails API Relationships Diagnostic

Place your responses inside the fenced code-blocks where indivated by comments.

1.  Describe a reason why a join tables may be valuable.

```sh
  A join table allows you to establish a relationship between two different tables.
```

1.  Provide a database table structure and explain the Entity Relationship that
describes a many-to-many relationship for `Profiles`, `Movies` and `Favorites`
(Think of Netflix). A `Profile` has a `given_name`, `surname` and `email` and a
`Movies` have `title`, `release_date`, and `length` and `Favorites` would be the
join table with references to `Movies` and `Profiles`.

```sh
A Profile has many favorite movies. Movies can be a favorite of many different profiles.
The favorite table helps establish this relationship.
```

1.  For the above example, what needs to be added to the Model files?

```rb
class Profile < ActiveRecord::Base
  has_many :movies, through :favorites
  has_many :favorites
end
```

```rb
class Movie < ActiveRecord::Base
  has_many :profiles, through: :favorites
  has_many :favorites, dependent: :destroy
end
```

```rb
class Favorite < ActiveRecord::Base
  belongs_to :movies, inverse_of: :profiles
  belongs_to :profiles, inverse_of: :movies
end
```

1.  What is the purpose of a serializer? What would our `Profile` serializer look
like to show all movies favorited by a profile on
`http://localhost:3000/profiles/1`

```sh
  A Serializer shows what data from the Profile table that will be shown. You can
  also list attributes from other tables via a join table.
```

```rb
class ProfileSerializer < ActiveModel::Serializer
  attributes :given_name :surnamr :email :movies :favorites
end
```

1.  What would the command be to _scaffold_ out a **join table** for Favorites from
the above `Movies` and `Profiles`.

```sh
bundle exec rails g scaffold Favorites movie:references prifile:references
```

1.  What is `Dependent: Destroy` and where/why would we use it?

```sh
Depenedent destroy will remove relationships if one of the items is removed. For example
a if someone deletes their profile all of their favorites will be deleted without
deleting the movies they favorite. 
```

1.  Think of **ANY** example where you would have a one-to-many relationship as well
as a many-to-many relationship in an application. You only need to list the
description about the resources and how they relate to one another.

```sh
  # < Your Response Here >
```
