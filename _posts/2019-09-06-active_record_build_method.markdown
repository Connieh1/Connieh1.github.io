---
layout: post
title:      "Active Record Build Method"
date:       2019-09-06 09:05:58 -0400
permalink:  active_record_build_method
---


When Active Record associations are declared, the declaring class automatically gains methods related to the association [[documentation](https://guides.rubyonrails.org/association_basics.html#polymorphic-associations)].

When has_many, or belongs_to associations are declared, the class gains the build method, among others. The build method is an alias [[doc](https://github.com/rails/rails/blob/959fb8ea651fa6638aaa7caced20d921ca2ea5c1/activerecord/lib/active_record/relation.rb#L84)] for the new method, however, the build method has the association present, which new does not. As with new, build will not insert a record into the database, but in working memory. If you would like it to persist to the database, it must be saved.

When declaring a has_many association, the class gains:

collection.build(attributes = {}, ...)


This following example comes from apidock.com [[doc](https://apidock.com/rails/ActiveRecord/Associations/CollectionProxy/build)]

```
class Person
  has_many :pets
end

person.pets.build
#=> #<Pet id: nil, name: nil, person_id: 1>

person.pets.build(name: 'Fancy-Fancy')
 => #<Pet id: nil, name: "Fancy-Fancy", person_id: 1>

person.pets.build([{name: 'Spook'}, {name: 'Choo-Choo'}, {name: 'Brain'}])
 => [
      #<Pet id: nil, name: "Spook", person_id: 1>,
      #<Pet id: nil, name: "Choo-Choo", person_id: 1>,
      #<Pet id: nil, name: "Brain", person_id: 1>
    ]

person.pets.size  # => 5 # size of the collection
person.pets.count # => 0 # count from database
```

When using collection.build, you may choose whether or not to pass in attributes. From the above example, none of the pets have been persisted to the database, because nothing is being saved. The size of the collection in working memory is 5, the database count is 0. 


When declaring a belongs_to association, or has_one, the class gains:

build_association(attributes = {})
pet.build_person(attributes = {}, ...)

"The build_association method returns a new object of the associated type. This object will be instantiated from the passed attributes, and the link through this object's foreign key will be set, but the associated object will not yet be saved[doc](https://guides.rubyonrails.org/association_basics.html)." In this case, you cannot use pet.person.build, because pet.person is nil until defined. 

Using build makes things easier because the associations are already set for you. But remember, as with new, the instance(s) returned must be saved in order to persist to the database.





