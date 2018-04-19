# Web

## Part 1

Mark Thompson is back again! This time, you've found his online shop, but it is clear that he is still developing it. Show him that his site is vulnerable!

https://bigbenbargains.biz/briongshop

Submit the usual CMSC389R flag with your writeup to demonstrate that you successfully completed the homework assignment.


I began with trying an xss attack by adding this to the URL ```https://bigbenbargains.biz/briongshop/item?id=<script>alert('OhNo!');</script>```, this seemed to cause a server error:

![alt text]()


Next, I built upon my assumption that all the "items" and their information were stored in an SQL table somewhere, so I thought using some sort of SQL injection could work. I began buidling my injection by taking the SQL injection from the slides and modifying it to get this URL: ```https://bigbenbargains.biz/briongshop/item?id=1' OR '1'='1' -- -``` hoping that I could get ```id``` to evaluate to true, and then dump all the information. This proved succesful and I got this page with this flag: ```CMSC389R-{u_ar3_th3_SQL_ninja}``` 

![alt text]()


## Part 2

Complete all 6 levels of:

https://xss-game.appspot.com/

#### Level 1

In order to beat this level, I simply queried ```<script>alert()</script>``` in the applications search bar, this was the correct answer and allowed me to move on to the next level.

#### Level 2

This level was more difficult to figure out than the last one, initially I tried to insert ```<script>alert();<\script>``` as a new status and in the URL, neither of these seemed to work. I tried an SQL injection using ```'1'='1' -- -``` just like I did in part 1 of this assignment, and that didn't work. While, looking at the source code I noticed that they did not do a good job of sanitizing input, and if I couldnt run javascript the same way I ran in Level 1 that I could hide it in some other form. In order to do this I simply added ```onerror = alert()``` to the URL which would run the javascript alert when the application encountered an error. Using this I suceeded and was allowed to move to the 3rd level.


### Level 3


