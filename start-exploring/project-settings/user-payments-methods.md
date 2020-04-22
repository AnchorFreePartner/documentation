---
description: The list of User Payment methods of the project.
---

# User Payment methods

Your application can include paid functions. For example, free users can have only a 100MB bandwidth limit per day but paid user - without any bandwidth limitation. To support this logic the application should provide to the Platform a purchase receipt for verification and registration.

There is the client-side method POST /user/purchase \(included in SDK methods too\) with parameter "type". This parameter decides what the user payment method used for user application. Each method should be registered in the project. 

The project can use more than one User Payment methods.

The Platform support next Payment methods:

### apple

...

### google

...

### custom methods

...

