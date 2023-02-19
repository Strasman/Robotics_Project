Youtube link for the Working Task demonstrate: https://youtu.be/zXn3l3Pv9v0

In this task, you will take your first steps using the AOS. The AOS advantage is mainly in robotic domains where the code effects are probabilistic, and the current state of the world is not observable to the robot. Decision-making in these domains is complex, and the AOS helps the robot engineer in this challenging task. The engineer should document: a) the robot's skills, b) The robot's environment, c) The robot's goals, and the AOS will automatically schedule the needed skills to reach the required goals.

In this task, you will meet some of the challenges of decision making under uncertainty.


Problem description:
Every afternoon, a mother returns from work, picks up her baby from daycare and comes home. She wants to rest a bit before his big brothers come, but her baby wants to play, and he is crying for her to come. She activates her home assistant robot and sleeps quietly.
The robot is programmed to bring the baby toys he enjoys. He has four toys, which we refer to by their colors: green, blue, black, and red. The baby plays with each toy for a certain amount of time, depending on his mood.
The location of each toy depends on where the baby left them yesterday.
The robot can navigate between the four possible locations of toys and the baby's location (they are described as locations 0-4, where 4 is the baby's location). The pick skill must know the exact toy type for a successful pick ('green,' 'blue,' 'black,' or 'red'), and the baby does not allow the robot to pick the toys he received. The robot cannot pick more than one toy at a time and must be located at the toy location. The pick skill accurately reports success or failure if these conditions were met. A successful pick cost is -1, but when it fails, it takes more time and costs -2.
The place skill return success if the robot is actually holding a toy. The place skill cost is -3 when it fails (if not holding a toy) and -1 otherwise. navigate skill cost is -3, with an additional penalty of -1 if asked to navigate its current location (which may cause orientation loss).


How the toys are ordered:
Every evening the cute baby throws the green toy to one of the locations. The probability of the green toy to be placed in the locations is [0:0.1, 1:0.05, 2:0.8, 3:0.05]. Next, he throws the blue toy to one of the remaining locations with a probability of [0:0.7, 1:0.1, 2:0.1, 3:0.1] (the probability of the already occupied location is evenly distributed to the other locations), then he throws to the black toy (both remaining locations have the same chance here). The red toy is thrown to the fourth location.

Remember that when using automated planning, you need to describe the problem, not solve it. Use the "InitialBeliefStateAssignments" in the environment file to describe the initial location of each object. Just tell the story using code :).

As said, the baby plays with each toy for a different number of minutes, depending on its mood. The mother observed the baby's behavior and saw that he plays with his toys for periods of [10,20,10,40] minutes. First, he thinks about how much he likes the green toy and assigns a play time for it with a discreet distribution of p([10=0.8,20=0.05,10=0.1,40=0.05]), then for the blue toy with p([10=0.1,20=0.7,10=0.1,40=0.1]), next it uniformly selects a period for the black, and the red toy receives the remaining period. These periods are rewards given when the robot places each toy on the baby's lap (they are the positive place skill reward in these cases).

The robot is allowed to use the pick skill only six times. The task ends (terminal states) when the robot gives the baby all of the toys, or when it uses all of its pick actions and is not currently holding a toy, or if it uses the pick skill more times than allowed. The robot's initial location is near the child.
To solve this problem, you will write a default policy.
