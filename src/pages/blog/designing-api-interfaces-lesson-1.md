---
layout: "../../layouts/PostLayout.astro"
title: "Long Lasting API Interfaces - Lesson 1"
description: "Developer pitfall when designing interfaces for microservices and best Practices, Lesson 1"
pubDate: "Jan 05 2023"
heroImage: "/myblog/img/blog/api-interface.png"
---

Engineers design interfaces every once in a while. What was the last time you created a interface ?

If the earlier developer would have put the structure right, you would not have faced the build failures or migration mess with the apis.

While the Developers design with the best in mind. Every API has its termination and deprecation date where it will become outdated and new API takes over or a new version of the API need to be developed.

Lets take an example, You want to register a customer basic details in your system `first name` and `last name`.

How would you create the interfaces, may be something like this  ?
**Provider**

```java
class CustomerProfile { 

    register(firstName: String, lastName: String){

    }
}
```

now you share the interface with your client and they use it.
**Client**

```java
class SomeLogicalCode { 

    myAwesomeRegistration() {
        CustomerProfile.register(firstName, LastName)
    }
}
```

Happy leaving for 6 months, and now you are asked to add `age` field, you update your interface to this ?
**Updated Provider**

```java
class CustomerProfile { 

    register(firstName: String, lastName: String, age: String){

    }
}
```

But wait, this will break your client isn't it ? or you create one more overloading method and ask your client to migrate from old to new one and then you delete the old overloading ? Developer time is gone in most of time rotating this, building, updating and finding who fails next and cleaning up.

This can be fixed if we would have encapsulated the objects under a class and taken it as object instead of functional parameters.
**Provider**

```java

class CustomerRegistrationInput { 
    String firstName;
    String lastName;
    Integer age;
    //more fields to follow.
}

class CustomerProfile { 
    register(input: CustomerRegistrationInput){
    }
}
```

Now your interface is solid and you don't have to keep changing and worry about client failures.
**Client side**

```java

class SomeLogicalCode { 

    myAwesomeRegistration() {
        CustomerProfile.register(CustomerRegistrationInput.build().name("Rajesh").lastname("Patidar").age(3).build())
    }
}
```

In next design lesson 2 for keeping the design interfaces backward compatible.
