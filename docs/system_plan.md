# bagelbash System Design

Process adapted do and inspired by by [Nirosh's article on codeproject](https://www.codeproject.com/Articles/16105/A-Practical-Approach-to-Computer-Systems-Design-an)

## Main questions:

1. **What are the inputs?** User selection of various items and submission of orders detailing those selections.

2. **What are the processes of the system?** bagelbash is a product browsing and ordering system. Ordering involves _product purchasing_ (which contains _ordering_, _browsing_, and _paying_.).

   1. **Do users have to be signed in to browse or purchase?** Users do not have to be signed in to browse, create, or submit/pay for orders.

   2. **What are the benefits of having an account and being signed in?** User information (payment details, email address, etc) can be persisted with a bagelbash account and reused for a second visit.

   3. **Where are the menu items for browsing and order selection coming from?** Menu Item information is coming from the Menu API (Menu API is considered external to bagelbash and will not be covered here).

      1. **Where is the Menu API located?** Menu API is located at /menu/v1/api

3. **What is involved with ordering?** Product selection, payment processing, and order submission.

4. What are the outputs?
   Allow the users to select entrees from the menu, group those selections into orders, pay for those orders, and submit those orders.
