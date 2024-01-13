# Mastering Solutions Architecture with Design Katas

TLDR: Architects get relatively few opportunities to practice their craft, so we will group up to formulate architectural visions for "real world" business problems. Attendees will then evaluate each group's solution to gain insight into the pros and cons of different approaches.

Fred Brooks said, "How do we get great designers? Great designers design, of course." So how do we get great architects? Great architects architect, but architecting a software system is a rare opportunity for the non-architect. For this, we turn to an ancient tradition, born of the martial arts, designed to give the student the opportunity to practice more than basics in a semi-realistic way. The coding kata, created by Dave Thomas, is an opportunity for the developer to try a language or tool to solve a problem slightly more complex than "Hello world". The architectural kata, like the coding kata, is an opportunity for the student-architect to practice architecting a software system.

In this workshop, attendees will be split into small groups and given a "real world" business problem (the kata). Attendees will be expected to formulate an architectural vision for the project, asking questions (of the instructor) as necessary to better understand the requirements, then defend questions (posed by both the instructor and their fellow attendees) about their choice in technology and approach, and then evaluate others' efforts in a similar fashion. No equipment is necessary to participate--the great architect has no need of tools, just their mind and the customers' participation and feedback.

## Morning Notes

Show Me the Money!

New Accounting System for a Local Community College
1000+ users, staff, faculty, (most local, but some nationwide/overseas)
No Web App (president hates internet), minimal software costs
Enforce accounting workflow, but individual departments to amen that workflow to suit their own needs. Keep complete audit trail records of third-party applications

Questions:

* What infrastructure do they have? (On-Prem vs Cloud)
  * Could use Cloud, but no experience. Basic On-Prem, only hosting basic websites 
* What does "suck" mean?
  * Coming from Excel/Terribly built apps
* Who are all the users?
  * Students, staff/faculty
* What are the third parties?
* What are the acceptable changes to the workflow?
  * Who can approve what?
* What is "minimal" software costs?
  * Looking for pre-built/piece mealing solutions or custom solutions?

To Determine Later:

* Attendance?

Requirements:

* Internal
  * Payroll
  * Benefits/Medical
  * Revenue
  * Expenses

Assumptions:

* Online Only! No offline or syncing process
  * Due auditing trails or other data integrity issues
* Use software that allows converting Web Apps into an Installed App
* Transactional SQL (financial system)
* Have a timeline, by start of 2025
* On-Prem Active Directory
* Staff are On-Prem/VPN

Ideas:

* Minimal Software Cost
  * License Costs Down

Considerations:

* User Personas

TODO:

* Take a look at Microsoft Threat Modeler

## Afternoon Notes

Auction Kata:

Designed around enhancing the live auction and not replacing it (aka making people in person do online activities).
They designed it around having the online act as a "live" person, but remotely. They can see the live room as it goes on and Spotters/Stenographers take note of all online and physical bids. That is what they designed around

Vs. a previous group of the presenter who focused on the crux of making an online auction/bidding system that live people can use

Mainly focusing this point on the difference in mindset that happens when you design a system, do you focus on UI/UX, Infrastructure, the workflow, data or anything else that may present itself as the focus of the system.