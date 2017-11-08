# Domain-Driven-Design 

Links:

https://www.mirkosertic.de/blog/2013/04/domain-driven-design-example/
http://dddcommunity.org/


What is DDD?

Domain-driven design is not a technology or a methodology. DDD provides a structure of practices and terminology 
for making design decisions that focus and accelerate software projects dealing with complicated domains.

Understanding the Domain.
Ubiquitous Language.
Contexts and Bounded Contexts.
Entities and Value Objects.
Aggregates and Aggregate Roots.
Persistence Ignorance. 
Repository. 
Domain Service. 

Understanding the Domain
A sphere of knowledge, influence, or activity. The subject area to which the user applies a program is the domain of the software.
- Wikipedia
Do you get a feeling what is domain from this definition?  Can you tell what is the domain of the project you are 
working on at this moment? Can you tell what is the domain of the famous website YouTube?

In this article I would like to go through a real world example to give you the feeling how to start analyzing your project
driven by your domain. This example may not be related with application development but as the goal is to tune our thinking 
top to bottom manner, it will be useful. But again, we will go through the technical terms of DDD too! 

Let’s say you are engaged to design a building. The requirement is:

You have a defined amount of land
Your building will have 6 floors.
Each floor will have 4 apartments.

What is your domain here?

The domain is Building(?). It could be. But note that, if you consider Building as your domain you may miss few granular details 
for your requirement. The building you are going to design must have design for apartments where people will live. So, a general 
term “Building” can make us miss few details. So, we may narrow down our domain to “Residential Building”.

Now, when you talk about your work with engineers and also with the people who engaged you to design the building, the term
“Residential Building” is more meaningful for everybody concerned. Did you mark very small change in language here? The 
contractor is telling you to design a building where there will be 4 apartments in each of the 6 floors. Now, if you send an
engineer to the site telling him we will need to construct a building there, they might not consider many attributes that a 
residential building must have. On the other hand if you use the term “Residential Building”, most likely he will come with
a valid analysis.
This is how we come to an “Ubiquitous Language”.


Ubiquitous Language
The concept is simple, that developers and the business should share a common language that both understand to mean
the same things, and more importantly, that is set in business terminology, not technical terminology.
More Example of Ubiquitous Language:
Example 1:

Wrong Language:

The length and width ratio of the smaller bed rooms would be 4:3.
Correct Language:

The children's bed room’s length will be 20 ft and width will be 15 ft.
Note that, to the owner of the building “smaller room”, “ratio” - all these things could be very technical terms. 
Rather it is easier for him to understand children's room, guest room, living room etc. And explicit measurement is more meaningful 
to him.
Example 2:

Let us see an example from software perspective.

Contexts and Bounded Contexts
A Bounded Context can be considered as a miniature application, containing itss own Domain, own code and persistence mechanisms. 
Within a Bounded Context, there should be logical consistency; each Bounded Context should be independent of any other Bounded Context.
More Example of Bounded Context:
Think of an e-Commerce system. Initially you can tell it is an application of shopping context. But if you look more closely, 
you will see there are other contexts too. Like: Inventory, Delivery, Accounts etc.
Dividing a large application among different bounded contexts properly will allow you to make your application more modular,
will help you to separate different concerns and will make the application easy to manage and enhance. Each of these Bounded Contexts
has a specific responsibility, and can operate in a semiautonomous fashion. By splitting these apart it becomes more obvious to find
where logic should sit, and you can avoid that BBOM (Big ball of mud) J

What is BBOM? 

A Big Ball of Mud is a haphazardly structured, sprawling, sloppy, duct-tape-and-baling-wire, spaghetti-code jungle. These systems show unmistakable signs of unregulated growth, and repeated, expedient repair. Information is shared promiscuously among distant elements of the system, often to the point where nearly all the important information becomes global or duplicated. The overall structure of the system may never have been well defined. 

- Brian Foote and Joseph Yoder, Big Ball of Mud. Fourth Conference on Patterns Languages of Programs (PLoP '97/EuroPLoP '97) Monticello, Illinois, September 1997
Our all time objective should be to avoid BBOM

Again with the “Residential Building Domain”. So, we could have several bounded contexts:

Electricity supply
Car parking
Apartment 
Etc.
Let’s talk about the apartment. The apartment is basically a combination of different rooms. The rooms have different elements 
inside like windows, doors etc. Now I have 2 questions to you about the windows of the room.
Question1: Can you imagine a window without a room?

Question2: Does a window have any identity without the room it is residing in?

Answering these questions will expose the following concepts of DDD.

Entity.
Value Object.
Aggregates & Aggregate root.
Entity
“This is my Entity, there are many like it, but this one is mine.” 
The key defining characteristic of an Entity is that it has an Identity – it is unique within the system, and no other Entity, 
no matter how similar is, the same Entity unless it has the same Identity.

Examples: 

Your bed room in the apartment.
Contract in Facebook.
Article in CodeProject.
Value Object 
The key defining characteristic of a Value Object is it has no Identity. Ok, perhaps a little simplistic, but the intention of a Value
Object is to represent something by its attributes only. Two value objects may have identical attributes, in which case they are 
identical. They don’t however have any value other than by virtue of their attributes. Another aspect common to value objects is that
they should probably be immutable, once created they cannot be changed or altered. You can create a new one, and as they have no 
identity, that is just the same as changing another one.
Example:

Windows in the rooms
Address of any person in your website.
SearchCriteria of your search.

Note:  A value object can become an entity depending on the situation. Can you find a scenario like that? If the requirement of the 
search functionality of your application says that, the search criteria should be saved in the database and the user can do the same 
search from the list of saved search criteria’s. In this scenario SearchCriteria has its own identity and thus it is an entity instead
of being a value object. 

Hide   Shrink    Copy Code
Now you know what entity is and what value object in DDD is. In domain driven design entities and value objects can exist independently.
But in some cases the relation can be such that, an entity or VO has no value without its context.

Example: 

A window can only be defined if there is a room. 
An order note can only exist if an order is placed.
A question detail can only be there if a question is asked.
Very simple is not it? Believe me, now you know what Aggregate and Aggregate root is in DDD.

Aggregate and Aggregate Root
In the examples given above – 
Room, Order and Question are our aggregate roots. 
On the other hand window, order note and question detail are our aggregates. 
“A cluster of associated objects that are treated as a unit with regard to data changes.”
All objects of the clusters should be treated as aggregate.
All external access to the cluster is through a single root Entity. This root entity is defined as aggregate root.

Example:

A question detail should no way be saved unless the corresponding question is saved.
A question detail should no way be retrieved unless the  corosponding question is retrieved. 
Here Question is the Aggregate root and Question Detail is the aggregate. Aggregates and Aggregates Root are very important concepts of
DDD.

So far we have talked about domain, objects/entities, contexts, aggregates etc. What about the Database? Is that something we have
missed? Isn’t it something should come in the design?

The answer is NO!  DDD is a persistence ignorant approach.

Persistence Ignorance

In domain driven design your objective is to create a model of the domain. You need to identify what are the items (objects) you need to
accomplish the desired functionalities of your application. You need to identify the relationships among different objects and how they
interact among themselves. You need to find if the business goal of your client is achievable using your domain model. Where is the
existence of database here?  You do not need to know how and where the data of your domain will persist or even if the data do need to
persist while you do the model of the domain.
This ignorance about your persistence medium will make your domain model free from any coupling with the persistence layer of the
application. This will eventually separate the concerns of the persistence and its communication mechanism from your domain model.
In result your application will be free from coupling with any data store and will be very easily unit testable.
But Yes! In a real application you do need to have a database. But your domain model will have no knowledge about that. All it will
know is the “Repository” which will eventually manage your application’s persistence concern.

Repository
Can you tell me what the meaning of the English word “Repository” is? 
Repository commonly refers to a location for storage, often for safety or preservation.
- Wikipedia

your domain model will not know any database. What it will know is, there is a repository in the system and 
that repository will be responsible to store your data and to retrieve your data. It is no way a concern of your domain model how and
where data will persist. So, it can be Sql server, oracle, xml, text file or anything else. I hope now you got a sense what a repository
means in DDD.

Let’s become little more technical.

Repository Mediates between the domain and data mapping using a collection-like interface for accessing domain objects. 
It is more like a facade to your data store that pretend like a collection of your domain.

Repository Is Not A Data Access Layer. 

Note that repository doesn’t talk in terms of “data”, it talks in terms of Aggregate Roots. You can tell your repository to add an
Aggregate Root into its collection, or you can ask it for a particular Aggregate Root. When you remember that Aggregate Roots may
comprise one or many Entities and Value Objects, this makes it fairly different to a traditional DAL that returns you back a set of
rows from your database tables. 

Implementation Strategy of Repository:

Repository is a design pattern that is used in DDD to handle the persistence concern. The detail of this pattern is out of
the scope of this article. However, here I am trying tell in minimum how we may achieve a repository implementation. 
1st of all you will have an interface - IRepository that should be generic.
You will have an abstract implementation of the IRepository interface.
You will have interface INhRepository  for your persistence mechanism (i.e. Nhibernate) this will inherit from IReposiroty. 
You will have implementation of INhReposiroty in a class like “NhReposirory”.
Finally you may have a generic implementation of the repository that will have default implementations of all the common methods of the
repository. 
Like NHGenericRepository that inherits from NhRepository and implments IGenericNhReposirtory.
You will specific repository for you Aggregate Roots, that will be extended from NHGenericRepository.
Your application will use service locator to find which repository the application will use. 
Domain Service
Domain service is another important concept of DDD. If Entities and Value Objects are the “things” in your domain, the services are a
way of dealing with actions, operations and activities.
Shouldn’t Logic Be on the Entities Directly?

Yes, it really should. We should be modeling our Entities with the logic that relates to them and their children. But, there are
occasions when we need to deal with complex operations or external responsibilities or maybe we need to expose the actions of the
aggregate roots to the external world. This is why creating a domain service for different aggregate root is a good idea. You can
consider the domain services as façade layer of the business logics and operations of your domain.  


