# swop-mvp

Trustless peer-to-peer marketplace for non-rebookable/refundable airline flight tickets.

## Problem Statement

Customers booked airline tickets in advance and most of these tickets are not refundable. Since these tickets are booked earlier, plans may change due to personal circumstances and when these happen, customers may lose substantial amount of money due to the non-refundable nature of the tickets. 

On the part of the airline, the chance that some passengers will not turn up on the day of the flight provides an opportunity for them to do overbooking. But overbooking creates a lot of issue and creates an unpleasant experience for passengers and airline staffs on the day of the flight if all passengers turn up. This also adds more overhead costs for them as they need to compensate passengers who got bumped off from the flight.

## Proposed Solution

swop application provides an option for customers to swop their booking to other passengers if they will not be able to take their flight. This prevents them from losing all their money used to book their tickets by posting their ticket on the application for swopping. Swoppers who buy the posted tickets have an advantage as most of the tickets bought in advance are cheaper than the current ticket price on the market. For airlines, since the chance of passenger not turning up is lower because they can swap their tickets, they can lessen, if not remove, their overbooking threshold. This can bring a more favourable experience for passengers and airline staffs and lessen the costs incurred by the airlines.

## dApp Architecture Design

The current design was made with the assumption that AMADEUS or Airlines had partnered with this system by providing custom API to make it work.


#### Sell Ticket - Sequence Diagram

![](https://user-images.githubusercontent.com/47552061/61999843-0d875000-b098-11e9-9342-edee73c54de7.png)

#### Buy Ticket - Sequence Diagram

![](https://user-images.githubusercontent.com/47552061/61999844-18da7b80-b098-11e9-9db4-d36a5371580e.png)

## Rebooking Fees

Airlines will still earn from the rebooking transactions as swop will deduct the fees from the seller's potential earning from the sold ticket.

## Data Storage

#### On-Chain

Only data regarding the locked funds and transaction states were stored in the blockchain as follows:
- amount
- swopRefNo
- address (sender/buyer)

#### Off-Chain

All flight details were stored in Firebase Database for easy lookup and flight search filter as follows:

**/ticketDetail/swopRefNo**
- amount
- status
- airline
- airportCode
- arrivalDateTime
- departureDateTime
- origin
- destination

**/origin**
- /countryCode/ticketId

**/destination**
- /countryCode/ticketId

**/departureDay**
- /date/fightId

**/arrivalDay**
- /date/fightId


## Source Codes

- [Smart Contracts](https://github.com/karlptrck/swop-contracts-mvp) 
- [Backend](https://github.com/karlptrck/swop-backend-mvp)
- [Frontend](https://github.com/abielvillarosa/swop)
- [Amadeus - Frontend](https://github.com/abielvillarosa/swop-amadeus)


## Deployments
- Smart Contracts : [Ropsten TestNet](https://github.com/karlptrck/swop-contracts-mvp/blob/master/ropsten_deployment_details.txt)
- Backend : DigitalOcean
- Frontend : [Demo URL](https://abielvillarosa.github.io/swop/)


## Screenshots

#### Landing Page
![](https://raw.githubusercontent.com/karlptrck/swop/master/landing.png)

#### Ticket Verification
![](https://raw.githubusercontent.com/karlptrck/swop/master/ticket_verification.png)

#### Post Ticket
![](https://raw.githubusercontent.com/karlptrck/swop/master/post.png)

#### Search Ticket
![](https://raw.githubusercontent.com/karlptrck/swop/master/search_result.png)

### Front-End Testing Instructions

Post Booking - Steps to test
1) Go to https://abielvillarosa.github.io/swop
2) Click on Post Booking button
3) On another browser, access this [airline api simulator](http://68.183.204.206:3000/testBookings?fbclid=IwAR35cCJEmkGWKyb7ZYMoLAZ8jI46AgZgxnfRg5wCvqsVLh5eiEJcvXAo3Yo) and select any booking ID
4) Enter the selected booking ID on the Booking ID field and click on the Submit button
5) The browser will issue an error as it is trying to connect to insecure Test API Endpoints. Click on the icon and click on "Load unsafe scripts" and go again to https://abielvillarosa.github.io/swop/postbooking page and enter the Booking ID.
![](https://github.com/karlptrck/swop/blob/master/swop-browser-sec.JPG)
6) On the Post Details page, the booking details are retrieved. Click on the Post link
7) This will open up a Metamask window and login, if not yet logged in. Click on the Confirm button
8) For the purpose of this testing, the transaction hash is displayed on the screen once it has connected and posted the transaction on the blockchain.
