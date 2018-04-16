# denver_airport-baggage-routing

Problem : Airport Baggage
Denver International Airport has decided to give an automated baggage system another shot. The hardware and tracking systems from the previous attempt are still in place, they just need a system to route the baggage. The system will route baggage checked, connecting, and terminating in Denver.

You have been asked to implement a system that will route bags to their flights or the proper baggage claim. The input describes the airport conveyor system, the departing flights, and the bags to be routed. The output is the optimal routing to get bags to their destinations. Bags with a flight id of “ARRIVAL” are terminating in Denver are routed to Baggage Claim.

Input: The input consists of several sections. The beginning of each section is marked by a line starting: “# Section:”

Section 1: A weighted bi-directional graph describing the conveyor system.
Format: <Node 1> <Node 2> <travel_time>

Section 2: Departure list Format:
<flight_id> <flight_gate> <destination> <flight_time>
Section 3: Bag list Format:
<bag_number> <entry_point> <flight_id>
Output: The optimized route for each bag

<Bag_Number> <point_1> <point_2> [<point_3>, …] : <total_travel_time>
The output should be in the same order as the Bag list section of the input.

Example Input:

# Section: Conveyor System
Concourse_A_Ticketing A5 5
A5 BaggageClaim 5
A5 A10 4
A5 A1 6
A1 A2 1
A2 A3 1
A3 A4 1
A10 A9 1
A9 A8 1
A8 A7 1
A7 A6 1
# Section: Departures
UA10 A1 MIA 08:00
UA11 A1 LAX 09:00
UA12 A1 JFK 09:45
UA13 A2 JFK 08:30
UA14 A2 JFK 09:45
UA15 A2 JFK 10:00
UA16 A3 JFK 09:00
UA17 A4 MHT 09:15
UA18 A5 LAX 10:15
# Section: Bags
0001 Concourse_A_Ticketing UA12
0002 A5 UA17
0003 A2 UA10
0004 A8 UA18
0005 A7 ARRIVAL
Example Output:

0001 Concourse_A_Ticketing A5 A1 : 11
0002 A5 A1 A2 A3 A4 : 9
0003 A2 A1 : 1
0004 A8 A9 A10 A5 : 6
0005 A7 A8 A9 A10 A5 BaggageClaim : 12

**My Approach :**

1) Please refer the attached word document(UseCases_AirportBaggage_Routing_System.doc) that I have explained in details for the four use cases to achieve the solution.[UseCases_AirportBaggage_Routing_System.docx](https://github.com/rgalanki11/denver_airport-baggage-routing/files/1914456/UseCases_AirportBaggage_Routing_System.docx)

2) Unzip "airport-baggage-routing-master" file
                i ) Main Controller of our application : airport-baggage-routing-master\src\main\java\com\barclaycard\interviews\airportbaggagerouting\controller\BaggageRoutingMainController.java
                      (Currently I have used as java main method for the starting point of the application to run , but in real time this can be a main controller class based on the framework we use like Spring,REST webservice rtc)
               ii ) Created a beanmodal package : com.barclaycard.interviews.airportbaggagerouting.beanmodal for defining the bean object based on the input parameters like bag ID,Entry Gate and Flight and also to build the weighted bidirectional graph on top of vertex,DirectedEdge and mapping for the Shortest Path graph 
               iii ) Created AirportBaggageInputUtil class under untility package (com.barclaycard.interviews.airportbaggagerouting.utility) to make use of the all the input use cases (1 - 3)
              iv ) Created a service definition package(interface declaration) : com.barclaycard.interviews.airportbaggagerouting.service to implement the shortest path algorithm using DijkstraAlgorithm
             v ) Created a service implementation package(interface implementation)-  com.barclaycard.interviews.airportbaggagerouting.serviceImpl to generate the path line between each nodes and find the shortest path
            vi ) Created a JUnit test class under airport-baggage-routing-master\src\test\java\com\barclaycard\interviews\airbaggagerouting - AirportBaggageRoutingJUnitTest to execute all the test case from the input parameter file : src/test/data/InputTestData.txt
              Note : Due to time limitations , I have created a one file to execute the required and expected output based on the requirement out of this exercise . But we can modify the input file based on our different test cases in short term and at the same time we can create as many number of input data files to define different test cases and execute all of them in one set to make sure that all test cases are passed.
              
3 ) Install Maven or unzip "apache-maven-3.5.3" file from the attachment
        i ) Set maven path in the windows environment variable - For example --> Path=C:\Users\rgala\Desktop\Raja Galanki\2018\interview\apache-maven-3.5.3\bin
        
4 ) Go to the command prompt and go to our application directory : cd airport-baggage-routing-master
**Run the application along with JUnit :** 

5 ) type : mvn clean install

6 ) java -jar target/denver_denver_airport-baggage-routing.jar src/test/data/InputTestData.txt
