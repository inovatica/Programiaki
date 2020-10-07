# Programmers - learning the basics of programming through play for preschool children.
Customer: Kindergartens

**Effects**

_The observations were collected during classes using the lProgramiaki project in kindergartens in Łódź._

## Advatages of getting kieds familiar with programming:

* learning the basics of programming through play with the use of movement;
* making the child aware of what programming is by showing how to get a given behavior through specific activities, e.g. preparing a set of commands / routes for a robot (in a broader context, it will be an assignment to a variable, the sequence of actions, sequencing, grouping values, looping, debugging, optimization of activities, division of actions into subtasks, assigning actions, commands to objects);

### Development of soft skills

* training the skills of conversation, communication in a group directed, inter alia, for problem solving;
* educating the ability to express one's feelings, opinions and thoughts;
* developing computational, systemic, design thinking and analytical thinking skills;

### Development of the skills necessary for learning

* developing the ability to concentrate attention, remembering information;
* training active listening skills;
* experiencing success as a result of completing a task;

## Context and purpose:

Programiaki is a project aimed at pre-school teachers. It allows children to acquaint children with the basics of programming through addictive games and activities. As part of the project, a complete solution was prepared, including:

* class scenarios in line with the material that a child should learn at a given level of development
* didactic tools such as a multimedia table, programmable robot, mats, and blocks
* software that supports teaching tools and an application that enables the group tutor to conduct classes efficiently;

The Programiaki project meets the basic developmental needs of preschoolers related to movement, experiencing the world through the senses, developing cognitive skills, and learning through play. It is based on the assumption that learning to program should be collaborative, i.e. collaborative learning, and adapted to the child's development level. The prepared solution allows you to move away from thinking about programming as a one-on-one interaction to learning programming in the context of activities that can support teamwork. When children program together, they take part not only in collaboration and group work but also in learning to properly shape interpersonal relationships. This is associated with the development of the ability to move around in society and the formation of social patterns that are necessary for negotiation, problem-solving, sharing emotions, or work.
The product meets the criterion of increasing difficulties and missions with the development of the child's skills. Each of the games has several levels adapted to the skills and abilities of a diverse age group of children. Thanks to a specially created application, the preschool teacher can manage the child's access to the appropriate levels. It is the teacher who decides which game levels to include, because knowing his group of children, he knows the skills of his pupils.

## Implementation of tools

### Multimedia table

The multimedia table is an interactive multimedia innovative presentation stand with the function of learning programming by interacting with RFID tags. The table has built-in RFID readers that read data from the blocks. Games on the multimedia table are thematically related to the issues arising in the classroom, gradually educate programming skills from the simplest games in which children learn to assign objects to a variable, to more and more difficult ones, e.g. sequences, loops, retrieving and returning data, to complex problem analysis necessary to choose a better option in a given game.

### Blocks

Based on graphics used in games, 3D prints with tags inside RFID. The appearance of the blocks represents animals, directions, multiplier cards etc. They aim to reduce the level of abstraction while learning programming and, additionally, to facilitate the fulfillment by children of tasks provided for, for example, in the zoo game, which requires children to be able to identify animal sounds by hearing.

### Robot

Own-made prototype built based on LEGO Mindstorm. The robot is designed to execute commands programmed by a code created by children using blocks with RFID tags placed on a multimedia table.

### Software

As part of the project, the software responsible for the operation of the entire set and for conducting classes was prepared.

#### The backend consists of:

1. Application running on Arduino

 The application running on the Arduino microcontroller is designed to read data from RFID readers connected to the microcontroller. After reading the value of the reader, he enters it into the table with cards - if there is no card on the reader, then it substitutes the value 404 meaning "no card". The application uses the i2c communication protocol in the slave mode - when it receives the indicated task (see table below) from the device operating in the "master" mode, the next data request will be the response to the requested task.
 
2. An application that aggregates data from Arduino and sends it to the Websocket server

 Application written in Python, version 3.4. The application runs on a device communicating in the i2c protocol in the master mode. In the loop, Arduino microcontrollers connected to the device (and configured in the application) are queried. If he gets an affirmative answer to the question "is there something new", he starts a request returning a new card. The received information is forwarded to the websocket server.
 
3. Websocket Server

 The websocket server handles incoming connections and propagates incoming content to all connected clients.

|CODE|JOB DESCRIPTION|
|---|---|
|68|Reset Sent Cards.|
|70|How many RFID readers are connected.|
|72|Are there any cards not yet sent among the current cards?|
|74|Which reader has not yet been sent.|
|76|How long will the answer be.|
|78|Enter the next digit from the card number. A request repeated as many times as the answer to the task 76 will be.|

|JOB CODE|ANSWER CODE|DESCRIPTION|
|---|---|---|
|70|int|Number of readers connected to the microcontroller.|
|72|20|	Yes, there are.|
|72|22|	No, they don't exist.|
|74|int|Reader number not yet transmitted.|
|76|int|After reading the card, they have different lengths - it returns the length of the card number.|
|78|int|Returns one number from a string and sets index to the next position.|

### Frontend:
1. **Teacher's app.**

 To supervise the process of learning programming for preschool children, an application for teachers was created that performs the following tasks:
 * Logging in / out of the group supervisor
 * Table lock to draw children away from the table
 * Locking the guardian's panel (to prevent an unauthorized child from managing the application)
 * Launch on a multimedia table
 * Listing, adding, editing, deleting groups
 * Assigning / Removing children to groups
 * Call to add children
 * Handling the request to start a new game:
   * Selecting the children to play the game (to award gamification points later)
   * Approval of the launch of a level in the game
 * Support for approving gamification points.

2. Application with games (for the multimedia table).

 The prepared interface plays various roles, e.g .:
 * programming in terms of subsequent robot or bee movements,
 * drawing shapes,
 * grouping shapes or arranging puzzles,
 * playing sounds.

 It is dedicated to children of various age groups, 3-, 4-, 5-, 6-year-olds who found the product attractive.

### Game examples:

#### Colors and Shapes (Drag & Drop)

Part 1 - Colors

1. Drag and drop the red square onto the red field (only the red drop field) - learning how to use TUI + sorting data.
2. Drag and drop the green triangle onto the green field - learning how to use TUI + data sorting.
3. Drag and drop the blue circle onto the blue field - learning how to use TUI + sorting data.
4. Drag and drop the green square onto the green field (3 field colors available for drop) - data sorting, problem analysis.
5. Drag and drop the blue triangle onto the blue field (3 color fields for drop are available) - data sorting, problem analysis.
6. Drag and drop the red circle onto the red field (3 field colors available for drop) - data sorting, problem analysis.
7. Sort blue square and green circle (3 colors of fields to drop available) - sort multiple data, analyze multiple problems in one task.
8. Sort the blue square and red triangle 2x (3 colors of fields to drop available) - sorting multiple data, analyzing multiple problems in one task.
9. Sort blue square, red triangle, and green circle (3 colors of fields to drop available) - sort multiple data, analyze multiple problems in one task.
10. Sort blue square, red triangle, green circle, green square, blue triangle, red circle (3 colors of fields for dropping available) - sort multiple data, analyze multiple problems in one task.

Part 2 - Shapes

1. Drag and drop the red square onto the square box (only square dropbox) to sort the data.
2. Drag and drop the green triangle onto the triangular field - sort data.
3. Drag and drop the blue circle onto the circular field - collate data.
4. Drag and drop the green square onto the square box (3 box types available to drop) - data sorting, problem analysis.
5. Drag and drop the blue triangle onto the triangular field (3 types of dropable fields available) - data sorting, problem analysis.
6. Drag and drop the red circle onto the circular field (3 types of fields to drop available) - data sorting, problem analysis.
7. Sort blue square and green circle (3 field types available to drop) - Sort multiple data, analyze multiple problems in one task.
8. Sort the blue square and red triangle 2x (3 field types available for dropping) - sort multiple data, analyze multiple problems in one task.
9. Sort blue square, red triangle, and green circle (3 types of drop-down fields available) - sort multiple data, analyze multiple problems in one task.
10. Sort blue square, red triangle, green circle, green square, blue triangle, red circle (3 field types available to drop) - sort multiple data, analyze multiple problems in one task.

Part 3 - Colors and Shapes

1. Drag and drop the red square onto the square box (red square dropbox only) to sort the data.
2. Drag and drop the green triangle onto the triangular box (green dropbox only) to sort the data.
3. Drag and drop the blue circle onto the round box (blue dropbox only) to sort the data.
4. Drag and drop the green square onto the square box (3 types of colored boxes available for dropping) - data sorting, problem analysis.
5. Drag and drop the blue triangle onto the triangular field (3 types of dropable fields available) - data sorting, problem analysis.
6. Drag and drop the red circle onto the circular field (3 types of fields to drop available) - data sorting, problem analysis.
7. Sort blue square and green circle (3 field types available to drop) - Sort multiple data, analyze multiple problems in one task.
8. Sort the blue square and red triangle 2x (3 field types available for dropping) - sort multiple data, analyze multiple problems in one task.
9. Sort blue square, red triangle, and green circle (3 types of drop-down fields available) - sort multiple data, analyze multiple problems in one task.
10. Sort blue square, red triangle, green circle, green square, blue triangle, red circle (3 field types available to drop) - sort multiple data, analyze multiple problems in one task.

#### Bee game part 1:

Reach your destination by using:

1. left arrows - sequences, loops;
2. right arrows - sequences, loops;
3. "up" arrows - sequences, loops;
4. "down" arrows - sequences, loops;
5. left arrows, level with a spider - sequences, loops;
6. "up" and "right" arrows, level with a spider - sequences, loops;
7. "up" and "left" arrows, level with a spider - sequences, loops;
8. "up" and "left" arrows, level with a spider on an alternative path - sequences, loops, problem analysis;
9. "up" and "left" arrows, level with a spider on an alternative path - sequences, loops, problem analysis + choosing a better option;
10. "up", "left" and "right" arrows level with a spider on an alternative path - sequences, loops, problem analysis + choosing a better option;
11. "up", "right" and "down" arrows level with a spider on an alternative path - sequences, loops, problem analysis + choosing a better option;
12. "up", "right" and "down" arrows level with a spider on an alternative path - sequences, problem analysis + choosing a better option, loop in the loop;
13. "up", "right" and "down" arrows level with a spider on an alternative path - sequences, loops, problem analysis + choosing a better option;
14. "up", "right" and "down" arrows level with a spider on an alternative path - sequences, loops, problem analysis (2 wrong paths) + choosing a better option;

#### The Bee 2:

Reach your destination by using:

1. "left" - sequences, loops, data retrieval, data return;
2. right arrows - sequences, loops, data retrieval, data return;
3. "up" and "right" arrows - sequences, loops, data download, data return;
4. "up" and "right" arrows - sequences, loops, getting data from different places, returning data;
5. "left" and "down" arrows - sequences, loops, getting data from different places, returning data, loops;
6. "up", "down" and "left" arrows - sequences, loops, getting data from different places, returning data;
7. "down" and "left" arrows, - sequences, getting data from different places, returning data to different places;
8. "up", "down" and "left" arrows - sequences, loops, getting data from different places, returning data to different places;
9. arrows in all directions level with a spider - sequences, loops, getting data from different places, returning data;
10. "left" arrows; spider level - sequences, loops, getting data from, returning data;
11. arrows in all directions level with a spider on an alternative path - sequences, loops, downloading data from different places, returning data to different places, problem analysis + choosing a better option;
12. arrows in all directions level with a spider on an alternative path sequences, loops, getting data from different places, returning data to different places, problem analysis + choosing a better option;
13. arrows in all directions level with a spider on an alternative path - sequences, loops, getting data from different places, returning data to different places, problem analysis + choosing a better option.

###  Implementation of didactics

The structure of the classes is flexible. It allows you to combine an innovative method of teaching programming using a multimedia table as well as motor games and activities. Here are its main assumptions:

* in the lesson scenarios, introductory fun appears at the beginning,
then the table and carpet activities, movement games, further: programming games, teaching basic skills, and ending games;
* table activities (coloring, work cards, cutting out, etc.) are interwoven with carpet activities - motor games;
* motor games are designed to educate small and gross motor skills, as well as basic programming skills;
*  as part of programming games, some sounds indicate the correct or incorrect way of performing a task and blocks with RFID tags identifying animals, food, and directions or instructions;
* revision activities to revise and consolidate the lessons learned by the children
previous classes. The proposed programming games can be changed depending on what the children liked, at what age preschoolers are, what was difficult - what you need to come back to. Among the physical activities, there are new and known to children. Ready scenarios can be modified;
* the time of classes is not strictly defined, their length depends on the age and abilities of the children (approx. 45-60 minutes);

### Work cards

The cards have been designed to develop hand dexterity or hand-eye coordination and can be performed by both 3-year-olds and 6-year-olds. These are labyrinths, coloring elements according to the guidelines in the task, saving the code according to how the elements of the drawing have been colored. The tasks included in worksheets are compatible with the tasks performed on the mat, and they aim to educate basic programming skills, e.g. the sequence of actions, grouping values, assigning activities to objects, making decisions in the direction of achieving the set goal.
There are 37 worksheets for use in the program, varying in terms of the difficulty of the tasks to be performed. Besides, the program includes worksheets No. 38-57, these are coloring pages with pictures of animals appearing in games on the multimedia table.

## Summary

During the research conducted in operating conditions (kindergartens), it was confirmed that the developed methodology of teaching programming and the associated didactic aid, which is a multimedia table, is an effective implementation of programming competences in preschool children. Tests carried out by children of all ages showed that thanks to the use of TUI (Tangible User Interface) technology and blocks, our product does not require experience with similar technology from the user. Programmers are a solution that engages children in learning, gives positive reinforcement, and is a valuable didactic aid for the teachers.
