# Engineering Decomp Interview Questions

```
There is a factory that is operated by employees 24 hours a day
  - A day is broken down into three groups of 8 hour shifts (first shift, second shift, third shift)
  - Each shift requires the following
    - An (1) operations manager
    - A fixed (20) number of line workers (as determined by the plant manager) 
    - A fixed (3) number of maintenance people (determined by plant manager)
  - An employee can only work 40 hours a week or else they will need to give permission and will also be paid overtime

There is also an HR system that keeps track of employee information in the following format
  - employee_id (primary key)
  - first name
  - last name
  - employee_social
  - employee_role (OPERATIONS_MGR, LINE_WRKR, MAINTENANCE)

You are asked to build a system that schedules employees for a given work week

You can assume your timeline for an MVP would be in 2 weeks
```

## An explanation of decomp:

  - This is often a type of question you will be asked by companies who fill more of a consulting role

  - I have also been asked this question in a couple of interviews with big tech companies

  - The general goal is to come up with a loose design doc that someone of your skill level could take and build this system within the given timeline

  - The key objective for the interviewee is to use this question to highlight your strengths
    - If you're good at backend, prove it. write a bunch of interesting api's and walk through the more challenging business logic
    - If you're good at UI design, this might be your only chance. Slide over to the whiteboard app and build something both beautiful and intuitive
    - If you know about architecture and APIs, talk about how you would build this in the cloud, or what rest APIs you know exist that you could pull from
  - This is your chance to show off anything you feel the other interviews might have missed

  - The key objective here for the interviewer is to understand a slew of things:
    - How you think about system design
    - Are you independent and willing to jump into uncomfortable situations
    - Are you not afraid to ask questions
    - Do you understand the needs of the user
    - Can you balance the needs of the user with the needs of the customer (they often aren't the same)
    - What are your strengths in system architecture
    - What are your weaknesses

  - This question is the most flexible question to allow the interviewing team to dig into parts of you that they don't feel they already have a comfortable grasp on
    - For example: if they didn't get a good grasp of your UI design they might push that on you here
    - If they thought you're understanding of cloud services was week they might ask you about cloud architecture

## Jumping into the problem:

  - Because the  problem is vague the intro will also be vague. You should jump right in and 
    begin talking as soon as you get the chance
  
  - There are many good ways to start
    1. Start with the big picture and talk your way down
      - This is the way I do it, because it's how my brain works but this may not be the
        best way for you
      - Looks something like "If we need a system to do scheduling, it will have to run asynchronously every week or so to generate schedules, maybe monthly so they have some time to prepare in advance... Given the time frame I would probably build this as an aws lambda function, that sends an email to the employee... Since we have this api let's start by building the backend service..."
    2. Start from the data layer
      - This is always a solid choice as IMO how you structure your data means everything
      - Looks like "I see we have this api, I probably don't want all the data provided so I'll build my employee table with these columns... I also probably need a employee_shift join table..."
    3. Start from the UI
      - I am not a UI designer but if you are this is a really good way to start
      - Most interviews (unless hiring for a pure UI role) won't cover UI questions so this is probably your only opportunity, don't miss it
      - Looks like "Users should be able to go to a website and see their schedule. (moves over to whiteboard section) I would build them a nice UI where they can click here and... If they want to make changes to their schedule they can click here... We could also make this a mobile app so they can check their schedule on the go..."
    4. Start from the framework
      - This option is good if you have real world experience already and want to highlight it
      - Looks like "I've built a scheduler like this before actually. Since I have the most experience deploying containers on kubernetes, this would probably be the quickest way for me to build an mvp. I'd build this with flask based on the time frame, if I had more time I might go with something like Django but we could always migrate fairly easily. You need some form of authentication for the manager to log in and make changes so let's start with how we would do that"
      - NOTE: I don't think the above is a great example of how to do this, but it get's the point across. It may come across as avoiding the question if you name drop too much so there's more of an art to doing this

## Ask questions

  - This is a big part where this style of interview differs from a normal technical interview. You are actually somewhat encouraged to ask questions.
  
  - Asking questions here demonstrates that you understand this is a "real" scenario and not a test. In the real world, you don't have all the answers, and you need to work with others to solve problems.
  
  - Your interviewer will be ready to act as the customer, the user or god, so you should take advantage of this.
  - Examples of good questions:
    1. "I know in the real world most systems that store employee information will have a contact email, can I assume that exists in the API you provided?"
      - The answer to this will probably be yes as a reward for asking questions. Now you have a way to notify users of their schedule and you don't have to do any work figuring out how to collect email addresses
      - If the answer is no, then this is also a good thing. A no to this question is intentional. It means that they left out email on purpose because they want you to talk about how to notify your customers. You have been rewarded for asking the question by now knowing exactly where to begin you problem solving, by figuring out notification.
    2. "Do the users want to be able to change their schedule?"
      - "For now lets assume that they do whatever they are told and don't care" i.e. No
        - This means that you don't have to waste time figuring this out. Your problem is now much simpler to solve
      - "Yes, I could see users wanting to change their schedule"
        - BINGO! you now know where to spend your time, walking through schedule management
    3. "At my last job we used mailchimp for email notifications, can I assume that exists here?"
      - "Yes"
        - No UI for you, just state that your notification is you making a simple api call with an email and a message
      - "No"
        - Again, you now know where to spend your time, user notification

  - The key here is that you should ask a few questions throughout your interview (maybe 4 or so)
    - There is a healthy balance here where if you ask too many questions, it may come off like you are avoiding your the problem itself

## Go with the flow

  - Best case scenario, at this point you are in your comfort zone whether it's UI, backend or data. When you're here, you should ride the wave. Don't feel like you have to jump to somewhere you're less comfortable right away. These questions are intentionally vague so you can often hand-wave stuff you don't feel comfortable addressing. 
    -  Example 1: "Most of the work here can be done in the backend, for now we can probably just get away with sending an email to the employee with their schedule"
      - I just removed UI from the conversation here
    - Example 2: Most of work here is the Manager setting their preferences and the Employees being able to easily view there schedules, the backend will pretty much be a rest passthrough to the database, with an asynchronous job that builds the schedule and calls the provided api.
      - Now I can focus on vibing in my UI space. Unfortunately UI devs often don't get the respect they deserve so the interviewer may ask you to go into at least the data layer a bit, but remember, you can define the data layer by what shows up on the screen 
  
  - Do keep in mind that at the end you should have, at least briefly, addressed the whole system in your decomp interview. So, although you should stay in the zone when possible, if there are 15 minutes left in your interview and you feel like you haven't described a complete system, it's a good idea to step out and wrap up some of the other sections you may have not addressed.

  - In a perfect scenario, with about 10 minutes left in the interview you get to a point where you feel like you've defined the system well enough on all ends to say "At this point I would probably get to work and start coding."

## Listen to your interviewer

 - An interview is like a first date. Not only do you have to be able to talk, you also have to be able to listen, and understand the subtle queues that your interviewer may be giving you

 - An interviewer speaking during your decomp isn't bad but it is a sign. It's a sign that they want to you to talk about something else.
    - This could be because they want to gauge your understanding of a specific concept
    - It could also be because you might have made a mistake
    - Example 1: "This is a pretty good looking data structure. Do you think we need to keep this column?"
      - If your interviewer asks this question in this style, then they want you to expand on this.
      - This could be for 2 reasons
        1. The decision you made here doesn't make sense
        2. The decision you made here isn't understood by your interviewer
      - The best move here is to talk it out. Think through what could be wrong with the decision you made.
      - You can move on from this once either you or your interviewer comes to an "ah-hah, now I get it" moment
    - Example 2: " This looks good, how would you build the backend to support this?"
      - A question like this means, you've convinced your interviewer that you are good on the current piece and now they want to see how good you are on something else
      - The move here is to follow where they point and start spending time there, or if you don't feel super comfortable where your interviewer has lead you, just hand-wave and move to something else where you do feel more comfortable.
        - This is less recommended but can be good if you feel like you are struggling.
        - (assuming they were talking about the UI) "Right, the backend would build the schedule, and save it to the database, then just query the database whenever the UI made rest calls for data. Speaking of data, I think our database would store fields like this..."
          - This is an example of a pivot from UI (through the backend) to the database
          - Again ideally you are comfortable in all parts of system design and don't need to do this. But it's better to pivot than to get nervous and say the dreaded sentence "I don't know"

## Change-up

 - You may find that you come to your solution a little early, this is generally ok as long as you are around the 40 minute mark in a 1hr interview. At this point the interviewer might add complexity to the problem.

 - If you've gotten to this point, the interview has gone well. Now you can answer whatever follow up question with whatever focus makes the most sense to you. It's really just a way to give you the extra time to show off anything else that you think your interviewer might have missed.

## Example extensions:
  - Add a feature to allow employees to swap shifts
  - Maintenance workers can be a variable number with a min of 1 and a max of 4
  - A plant manager now wants to change the number of line workers to 40 and add a second operations manager
  - So you built this system and they love it, now they want to deploy it across the enterprise. What improvements would you make with a longer timeline?