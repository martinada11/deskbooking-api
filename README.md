# Desk Booking API
An api for booking & paying for desks in a multistorey workspace

## Problem
A desk booking api system 

## Actors
* Admin  
* Customer

## Entities
* Users
* Booking
* Desks
* Rooms
* Payments

## Core Use Cases
* auth
* list available desks
* reserve desk
* cancel desk booking
* change desk booking
* create user
* update user
* delete user

## Key Rules
* A customer cannot book more than 1 desk in a single day
* once a customer has reserved a desk, itit;s not available for anyone else for the rest of the selected day to book
* a customer can only make a single booking for a single desk for a given day
* a customer can book multiple days in advance
* a customer cannot book the same seat 3 days back to back

## Endpoints
### GET `/availability?date=xx` - lists available seats for a given day  
Response - 200 OK
```
{
    "availableDesks": {
        A: {
            1, 2, 4, 5
        },
        B: {
            1, 2, 3, 4, 5
        },
        ...
    }
}
```

### POST `/user` - create a new standard user  
Request
```
{
    "firstName": "John",
    "lastName": "Doe"
}
```

Response
```
{
    "userId": "12345",
    "password": "sdofihwefwef"
}
```

### GET `/user/{userId}` - view user details*  
```
{
    "firstName": "",
    "lastName": "",
    "status": active
    "bookingHistory": {
        {
            "date": "xx/xx/xx",
            "deskNumber": ""
        },
        {
            "date": "xx/xx/xx",
            "deskNumber": ""
        },
        {
            "date": "xx/xx/xx",
            "deskNumber": ""
        }
    }
}
```

### PATCH `/user/{userId}` - update user details*  
find out how this endopint's http method should work

### DELETE `/user/{userId}` - delete user*  
Response - 202 Accepted
```
{
    "userId": "",
    "status": deleted
}
```

### POST `/booking` - create a specific desk*  

Request
```
{
    "deskNumber": "A3",
    "room": "",
    "floor": "",
    "date": xx/xx/xx
}
```
Response - 200 CREATED
```
{
    "bookingId": 12345,
    "deskNumber": "A5",
    "room": "Cube",
    "floor": "1"
}
```

### POST `/booking/amend/{bookingId}`  - change desk booking*
Request
```
{
    "newDeskNumber": 1,
    "newRoom": "",
    "newFloor": ""
    "newDate": xx/xx/xx
}
```

Response - 200 ACCEPTED
```
{
    "bookingId": 12345
}
```
// new id, amend existing booking's status to amended

### POST `/booking/cancel/{bookingId}` - cancel a specific desk*
Request
```
{
    "bookingId": "",
    "deskNumber": "A5"
    "date": xx/xx/xx
}
```

Response
```
{
    "bookingStatus": "cancelled"
}
```

### POST `/pay/{bookingId}` - pay for a booking
Response
```
{
    "status": "Payment Accepted"
}
```


\* authenticated endpoint