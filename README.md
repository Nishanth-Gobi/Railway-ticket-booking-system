# Railway-ticket-booking-system
### A simple railway ticket booking system implemented using assembly language programming in Emu-8086 

The booking system localised for a particular railway station includes,

-> An user portal, wherein users can enquire ticket availability and book tickets to one of the destinations (pre-programmed) given that the particular train has seats available. The users are given a unique key after payment.

-> An administrator portal, to authenticate the unique keys of users, modify the base value for the unique key and to add to or remove from available destinations.

#### Limitations:

1) In regards to this code, there's assumed to be only one train between any two stations. 
2) The unique identification key has been implemented using a really simple addition algorithm from a base value and anyone would get to know the base value if the found the first person to book tickets.
