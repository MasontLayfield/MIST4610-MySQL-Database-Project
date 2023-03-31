# MIST4610-MySQL-Database-Project
The first project for my data analytics class that entailed creating a data model, database, and writing queries based on them.

# Flight Tracker
## Problem Description
A Flight has many actors involved in getting a customer from one place to another, making it complex and difficult to track all of its moving parts. Many different types of managers need access to the same intertwined data to streamline a guest’s flying experience.  The managers from airlines need information about flight status and the number of people on a flight and crew managers need to know who they are supervising for a given flight. All of these managers have their own sets of data, but by connecting all entities they are able to have access to every detail of a trip including passenger information, seat information, passenger’s luggage, flight information including arriving and departing airport, what type of aircraft a passenger’s trip is using, the crew aboard that trip, and also the airline that a trip is affiliated with. This data model/database allows all entities to be connected to ensure a positive customer experience and streamlined operations between all airport personnel.

## Group Name and Members

Group 21482_ 6

[Aaron Fritchley](https://github.com/aafritch/MIST-4610)

[Mason Layfield](https://github.com/MasontLayfield/MIST4610-MySQL-Database-Project)

[Alexandra Shalikashvili](https://github.com/als94377/4610_project)

[Simran Singh](https://github.com/simranhk/MIS)

[Ashley Skaggs](https://github.com/skaggsashley1/MIST4610_Project)

## Data Model
![project data model  73](https://user-images.githubusercontent.com/128408107/228953445-a43ebdff-0630-4f7c-a080-b53fe4ba4204.jpg) <br />

**Explanation:** An arriving airport has many flights and a departing airport has many flights. Although a flight can have only one arriving and one departing airport. A flight can have one airline and an airline can have many flights. A flight can have many trips and a trip can only have one flight. An aircraft can have many trips but a trip can only have one aircraft. A trip can have many crew members and crew members can have many trips. A crew member can also act as a supervisor for other crew members. A trip has many seats but a seat can have only one trip. A seat can have many passengers and passengers can have many seats. A trip can have many passengers, but a passenger can only have one trip. A trip can have many pieces of luggage, but one piece of luggage can only have one trip. Finally, A Passenger can have many pieces of luggage, but a piece of luggage can only belong to one passenger. <br />

## Data Dictionary

**Table: AIRCRAFT**
| Column Name     | Description                                        | Data Type | Size | Format | Key? |
| --------------- | -------------------------------------------------- | --------- | ---- | ------ | ---- |
| aircraftID      | Unique sequential number identifying each aircraft | Text      | 45   |        | PK   |
| aircraftType    | Type of aircraft                                   | Text      | 45   |        |      |
| seatingCapacity | Indicates the number of seats in the aircraft      | Text      | 45   |        |      |

**Table: AIRLINE**
| Column Name | Description                           | Data Type | Size | Format | Key? |
| ----------- | ------------------------------------- | --------- | ---- | ------ | ---- |
| airlineID   | Unique number identifying the airline | Text      | 45   |        | PK   |
| airlineName | The airline’s name                    | Text      | 45   |        |      |
| websiteURL  | The airline’s website                 | Text      | 45   |        |      |
| homeCountry | The airline’s home country            | Text      | 45   |        |      |

**Table: AIRPORT**
| Column Name | Description                                 | Data Type | Size | Format | Key? |
| ----------- | ------------------------------------------- | --------- | ---- | ------ | ---- |
| airportID   | Unique number identifying the airport       | Text      | 45   |        | PK   |
| airportName | The airport’s name                          | Text      | 45   |        |      |
| city        | The city in which the airport is located    | Text      | 45   |        |      |
| state       | The state in which the airport is located   | Text      | 45   |        |      |
| country     | The country is which the airport is located | Text      | 45   |        |      |

**Table: CREW**
| Column Name     | Description                                           | Data Type | Size | Format | Key?         |
| --------------- | ----------------------------------------------------- | --------- | ---- | ------ | ------------ |
| crewMemberID    | Unique sequential number identifying each crew member | Text      | 45   |        | PK           |
| crewType        | The crew member’s role/position                       | Text      | 45   |        |              |
| crewFullName    | The crew member’s name                                | Text      | 45   |        |              |
| crewPhoneNumber | The crew member’s phone number                        | Text      | 45   |        |              |
| crewHomeCountry | The crew member’s home country                        | Text      | 45   |        |              |
| supervisorID    | The supervisor’s ID number                            | Text      | 45   |        | FK(ref.CREW) |

**Table: FLIGHT**
| Column Name             | Description                                                       | Data Type | Size | Format | Key?             |
| ----------------------- | ----------------------------------------------------------------- | --------- | ---- | ------ | ---------------- |
| flightID                | Unique sequential number identifying each flight                  | Text      | 45   |        | PK               |
| Airline_airlineID       | Indicates the ID of the airline that is carrying out the flight   | Text      | 45   |        | FK(ref. AIRLINE) |
| Airport_airportIDdepart | Indicates the departing time of the airport supporting the flight | Text      | 45   |        | FK(ref. AIRPORT) |
| Airport_airportIDarrive | Indicates the arrival time of the airport supporting the flight   | Text      | 45   |        | FK(ref.AIRPORT)  |

**Table: LUGGAGE**
| Column Name           | Description                                         | Data Type | Size | Format | Key?              |
| --------------------- | --------------------------------------------------- | --------- | ---- | ------ | ----------------- |
| luggageID             | Unique sequential number identifying each bag       | Text      | 45   |        | PK                |
| luggageWeight         | The weight of each bag(luggage)                     | Text      | 45   |        |                   |
| luggageDesc           | The description of the luggage                      | Text      | 45   |        |                   |
| Trip_tripID           | Indicates the trip that the luggage is on           | Text      | 45   |        | FK(ref.TRIP)      |
| Passenger_passengerID | Indicates the passenger that the luggage belongs to | Text      | 45   |        | FK(ref.PASSENGER) |

**Table: Passenger**
| Column Name  | Description                                         | Data Type | Size | Format | Key?          |
| ------------ | --------------------------------------------------- | --------- | ---- | ------ | ------------- |
| passengerID  | Unique sequential number identifying each passenger | Text      | 45   |        | PK            |
| firstName    | The passenger’s first name                          | Text      | 45   |        |               |
| lastName     | The passenger’s last name                           | Text      | 45   |        |               |
| emailAddress | The passenger’s email address                       | Text      | 45   |        |               |
| phoneNumber  | The passenger’s phone number                        | Text      | 45   |        |               |
| city         | The city in which the passenger resides             | Text      | 45   |        |               |
| state        | The state in which the passenger resides            | Text      | 45   |        |               |
| country      | The country in which the passenger resides          | Text      | 45   |        |               |
| Trip_tripID  | Indicates the trip the passenger is taking          | Text      | 45   |        | FK(ref. TRIP) |

**Table: SEAT**
| Column Name | Description                                 | Data Type | Size | Format | Key?          |
| ----------- | ------------------------------------------- | --------- | ---- | ------ | ------------- |
| seatNumber  | Unique number identifying the specific seat | Text      | 45   |        | PK            |
| Trip_tripID | Indicates the trip that the seat is on      | Text      | 45   |        | FK(ref. TRIP) |

**Table: SEAT_HAS_PASSENGER**
| Column Name           | Description                             | Data Type | Size | Format | Key?              |
| --------------------- | --------------------------------------- | --------- | ---- | ------ | ----------------- |
| Seat_seatNumber       | Indicates the seat the passenger is in  | Text      | 45   |        | FK(ref.SEAT)      |
| Passenger_passengerID | Indicates the passenger that has a seat | Text      | 45   |        | FK(ref.PASSENGER) |

**Table: TRIP** 
| Column Name         | Description                                          | Data Type | Size | Format      | Key?              |
| ------------------- | ---------------------------------------------------- | --------- | ---- | ----------- | ----------------- |
| tripID              | Unique sequential number identifying the trip        | Text      | 45   |             | PK                |
| tripDate            | The date of the trip                                 | Text      | 45   | MM/DD/YYYY |                   |
| tripDepartTime      | The departure time for the trip                      | Text      | 45   |             |                   |
| tripArriveTime      | The arrival time for the trip                        | Text      | 45   |             |                   |
| Flight_flightID     | Indicates the flight that is carrying out the trip   | Text      | 45   |             | FK(ref. FLIGHT)   |
| Aircraft_aircraftID | Indicates the aircraft that is carrying out the trip | Text      | 45   |             | FK(ref. AIRCRAFT) |

**Table: TRIP_HAS_CREW**
| Column Name       | Description                                   | Data Type | Size | Format | Key?          |
| ----------------- | --------------------------------------------- | --------- | ---- | ------ | ------------- |
| Trip_tripID       | Indicates the trip that has a crew member     | Text      | 45   |        | FK(ref.TRIP)  |
| Crew_crewMemberID | Indicates the crew member that is on the trip | Text      | 45   |        | FK(ref. CREW) |

## Queries

**Query 1:** <br />
**Description-** Write a query to list airports from most busy to least busy and the total number of departing passengers in each. <br />

<img width="583" alt="Screenshot 2023-03-31 at 12 35 19 PM" src="https://user-images.githubusercontent.com/128408107/229178811-8165656c-037b-4324-b656-470f142495a0.png"> <br />

**Justification:** A manager may want to know which airports are the most/least bust to ensure the airports are properly staffed with the correct amount of TSA employees, Receptionists, Flight Attendants, and Security to account for the number of passengers departing from that airport. An understaffed busy airport could be unsafe for guests and lead to a unpleasant flying experience. <br />

**Query 2:** <br />
**Description-** Write a query to list the number of passengers from each country (if at least one citizen was present) who flew from Hartsfield-Jackson to John F. Kennedy <br />

<img width="659" alt="Screenshot 2023-03-30 at 5 14 02 PM" src="https://user-images.githubusercontent.com/128408107/228966024-2797ede2-7548-4afc-8c78-ab015dc60220.png"> <br />

**Justification:** A manager would want to know the number of passengers from each country who flew from Hartsfield-Jackson to John F. Kennedy to ensure the passengers are adhering to proper visa rules. This also gives insight on where people from other countries are traveling within the United States during their time here. <br />

**Query 3:** <br />
**Description-** Write a query to list out the names of supervisors and the crew members they supervised on if the number they supervise is greater than 3 <br />

<img width="710" alt="Screenshot 2023-03-30 at 5 15 29 PM" src="https://user-images.githubusercontent.com/128408107/228966243-015a39ba-4808-4340-83e4-8e1de739ccef.png"> <br />

**Justification:** A manager may want to see how many crew members supervisors are in charge of to ensure one employee is not in charge of too many people (more than 3). Unless they are the 3 lead supervisors, in that case one of the three is assgined to many crew members due to their experience/seniority. <br />

**Query 4:** <br />
**Description-** Write a query to display the passenger ID, first name, last name, and luggage weight for those passengers whose luggage weighs more than the average luggage weight <br />      

<img width="808" alt="Screenshot 2023-03-31 at 11 58 15 AM" src="https://user-images.githubusercontent.com/128408107/229170955-5a8c8b6d-e951-47c5-907e-fad05218358f.png">
<img width="311" alt="Screenshot 2023-03-31 at 11 58 00 AM" src="https://user-images.githubusercontent.com/128408107/229171005-3ab84804-3b86-4240-bc9a-e132d6148c18.png"> <br />

**Justification:**  A manager may want to know how many people per flight have above average luggage to enure the flight stays within its weight restrictions. This may lead to people being asked to switch flights or the flight being cancelled due to being overweight. This would also allow managers to see the full range of luggage weight and set restrictions for future passengers if flights being overweight becomes a constant issue.. <br />

**Query 5:** <br />
**Description-** Write a query to display the percentage of Chinese passengers on each trip <br />

<img width="851" alt="Screenshot 2023-03-30 at 6 12 54 PM" src="https://user-images.githubusercontent.com/128408107/228975463-3c2747ce-3be6-44c9-8e0f-bd492362d406.png"> <br />

**Justification:** A manager may want to find the percentage of chinese passengers on each flight, as it could be beneficial when it comes to visa issues or anything of that nature. A manager would be able to see what percent of people are from different countries on their flights, in this case China. This information could also help the Customs office gage what percent of people coming into the United States are Chinese and have their employees properly trained on policies for people traveling from that country. <br />

**Query 6:** <br />
**Description-** Write a query to list the names of all passengers who have at least one luggage item with weight greater than the average weight of all luggage items for their trips <br />

<img width="563" alt="Screenshot 2023-03-30 at 6 16 02 PM" src="https://user-images.githubusercontent.com/128408107/228975980-e6dd24c8-9536-4107-8691-446343069567.png">
<img width="183" alt="Screenshot 2023-03-30 at 6 14 56 PM" src="https://user-images.githubusercontent.com/128408107/228975845-bb203441-c359-4939-85ea-94d379b5773b.png"> <br />

**Justification:** A manager may want to find the names of all passengers who have at least one luggage item with weight greater than the average weight of all luggage items for their trips. This will allow manager to get a gage of how many bags will fit within the weight limit of an aircraft with the extra weight. <br />

**Query 7:** <br />
**Description-** Write a query that lists the aircraft ID and number of trips taken for each Boeing aircraft <br />

<img width="598" alt="Screenshot 2023-03-30 at 6 18 35 PM" src="https://user-images.githubusercontent.com/128408107/228976292-c674b59b-b910-4501-a674-736390aced29.png"> <br />

**Justification**:  A manager may want to know how many flights an aircraft has taken to make sure it gets the right maintenance checks and is in good working condition. The average amount of flights an aircraft takes is about 35,000, so a manager would want to retire an aircraft once that number is passed. Past 35,000 flights the metal on a plane can decay, which is unsafe for both crew and passengers. <br />

**Query 8:** <br />
**Description-** Write a query that lists aircrafts that have a seating capcacity that is larger than the average seating capacity <br />

<img width="629" alt="Screenshot 2023-03-30 at 6 19 48 PM" src="https://user-images.githubusercontent.com/128408107/228976457-9d4d184b-bf57-40b6-9f05-546276660348.png"> <br />

**Justification:** A manager may want to reserve the larger aircrafts for more popular flight routes, such as international flights. Using a larger aircraft on a short unpopular flight would not me cost/time effective. Knowing which flights have an above average seating capacity would also help a manager assign them to flights that are frequently overbooked to improve customer relations.

**Query 9:** <br />
**Description-** Write a query to list customers names who’s luggage were not given a description. <br />

<img width="670" alt="Screenshot 2023-03-30 at 6 21 14 PM" src="https://user-images.githubusercontent.com/128408107/228976656-fa1eb91a-f450-4075-bba0-d33e8d8bdf71.png"> <br />

**Justification:** When a customer reaches out about lost luggage, a manager may want to see if that passenger's luggage did not have a description and add one if the customer is able to provide a description. An airline would be able to more easily find lost luggage if there is a description attached to it.

**Query 10:** <br />
**Description-** Write a query that displays the seat number, name, and contact information of passengers who are not from the USA who flew on July 1, 2022. <br />

<img width="553" alt="Screenshot 2023-03-31 at 7 35 48 AM" src="https://user-images.githubusercontent.com/128408107/229109965-68122c03-96b7-49d7-9319-566f967ad2f8.png"> <br />

**Justification:** A manager may want to be able to locate which seat has a passenger that is not from the USA in order to make sure they are accommodated and taken care of just like every other passenger. Oftentimes in situations with elderly international travelers, airlines help those passengers navigate (especially in situations with a language barrier), and provide extra assistance to those passengers during their flight. This query shows passengers not from the USA who flew on 7/1/2022, but the query could be used for other dates upon manager request. <br />


## Query Matrix
|                       | Q1 | Q2 | Q3 | Q4 | Q5 | Q6 | Q7 | Q8 | Q9 | Q10 |
| --------------------- | -- | -- | -- | -- | -- | -- | -- | -- | -- | --- |
| Multiple table join   | X  | X  |    |    |    | X  |    |    | X  | X   |
| subquery              |    |    |    | X  |    | X  |    | X  | X  |     |
| Correlated subquery   |    |    |    |    |    | X  |    |    |    |     |
| GROUP BY              | X  |    |    |    | X  |    |    |    |    |     |
| GROUP BY with HAVING  |    |    | X  |    |    |    |    |    |    |     |
| Multi condition WHERE |    | X  |    |    |    | X  |    |    |    | X   |
| Built-in function     |    | X  |    | X  | X  | X  |    | X  |    |     |
| REGEXP                |    |    |    |    |    |    | X  |    |    |     |
| ROUND                 |    |    |    |    | X  |    |    |    |    |     |
| CONCAT                |    |    |    |    | X  |    |    |    |    |     |
| NOT EXISTS            |    |    |    |    |    |    |    |    | X  |     |

## Database Information
Our queries are stored as Procedures in the ns_21482_6 server in the format TP_Qx.


