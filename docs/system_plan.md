# bagelbash System Design

Process adapted to and inspired by by [Nirosh's article on codeproject](https://www.codeproject.com/Articles/16105/A-Practical-Approach-to-Computer-Systems-Design-an)

## Glossary

-  **User**: The user currently viewing the system from the website.
   -  They may or may not need to have an account.
   -  Purchases can be made with or without an account.
-  **Menu**: The listing of items available for purchase.
   -  Accessed through the Menu API at /menu/v1/api
-  **MenuItem**: An item in the Menu listing.
-  **Order**: An attribute on a User containing OrderItems (if any).
   -  Users always have an Order, even if it is empty.
-  **OrderItem**: An entity that links an Item to a User.
   -  OrderItems also have quantity.
-  **Cheque**: A 'calcified' representation of an Order at the time of Cheque creation. Contains ChequeItems.
-  **ChequeItem**: A 'calcified' representation of an OrderItem at the time of ChequeItem creation.

## Main questions:

1. **What are the inputs?** User selection of various items and submission of orders detailing those selections.

2. **What are the processes of the system?** bagelbash is a product browsing, selectiont, and ordering system.<!--  Ordering involves _product purchasing_ (which contains _ordering_, _browsing_, and _paying_.). -->

   1. **Do users have to be signed in to browse or purchase?** Users do not have to be signed in to browse or order.

   2. **What are the benefits of having an account and being signed in?** User information (payment details, email address, current order, past cheques, etc) can be persisted with a bagelbash account and reused for a second visit.

   3. **Where are the menu items for browsing and selection coming from?** Menu Item information is coming from the Menu API (Menu API is considered external to bagelbash and will not be covered here).

      1. **Where is the Menu API located?** Menu API is located at /menu/v1/api
      2. **What information will the Menu Item contain?** WIP

   4. **What is involved in Menu Item selection?** When a Menu Item is selected from the menu, a corresponding OrderItem is created. The OrderItem has, quantity, User, and Item attributes.

   5. **Where does the Order Item go?** Each user has _one_ Order attached to themselves. An Order is composed of zero or more Order Items. When an Order Item is created, it is added to the User's Order.

   6. **Can multiple Order Items be purchased?** Yes. Multiple Menu Items can be added to an Order. This will create corresponding OrderItems for each Menu Item.

   7. **How is a purchase completed?** When the user is finished selecting items for their order, they may initiate checkout and creation of a Cheque.

      1. **What is a Cheque?** A Cheque is a record of an Order at a point in time.
      2. **What is the checkout process?** A user may initiate checkout from the website. They will enter their payment information to do so. When their payment information has validated, a Cheque will be created containing ChequeItems corresponding to the OrderItems.
      3. **How is an OrderItem different from a ChequeItem?** ChequeItems are 'calcified' OrderItems. If the price an Item changes (OrderItem.item.price) changes after a ChequeItem is created, the ChequeItem reflects the previous price.

3. **What are the outputs?** Allow the users to select Menu Items, group those selections into Orders, checkout and pay for those Orders, and submit those Orders.
