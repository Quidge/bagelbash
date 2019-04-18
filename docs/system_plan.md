# bagelbash System Design

##### Process adapted do and inspired by by [Nirosh's article on codeproject](https://www.codeproject.com/Articles/16105/A-Practical-Approach-to-Computer-Systems-Design-an)

## Main questions:

1. What are the inputs
   User selection of various items and submission of orders detailing those selections.
2. What are the processes of the system?
   bagelbash is a product browsing and ordering system. Users may initiate two processes processes are _product purchasing_ (which contains _ordering_, _browsing_, and _paying_.) and _menu alteration_ (product creation, removal, or modification).

   2.1. Do users have to be signed in to browse or purchase?
   Users do not have to be signed in to browse, create, and submit orders.

   2.1.1. What are the benefits of having an account and being signed in?
   User information (payment details, email address, etc) can be saved and reused for a second visit.

3. What are the outputs?
   Allow the users to select entrees from the menu, group those selections into orders, pay for those orders, and submit those orders.
