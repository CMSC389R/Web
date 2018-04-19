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

For this level, I used a hint that told me ```To locate the cause of the bug, review the JavaScript to see where it handles user-supplied input.```, so I looked over the code and realized this line: ```html += "<img src='/static/level3/cloud" + num + ".jpg' />";``` had a potential vulnerability. I could cause the image source to be something non-existant and then use ```onerror = alert();``` to be able to create an alert. My first attempt I used this URL: ```https://xss-game.appspot.com/level3/frame#' onerror = alert()``` but got this page:

![alt text]()

But after realizing that I needed to format the html element in a way that would be equivelent to ```html += "<img src='/static/level3/cloud" + num + ".jpg' />";```, I used this to produce the desired result: ```https://xss-game.appspot.com/level3/frame#0.jpg' onerror=alert();'```

### Level 4

For this level I took what I learned from the last level and searched for where the user input was bieng handled, I located one line of code that could be potentially vulnerable: ```<img src="/static/loading.gif" onload="startTimer('{{ timer }}');" />```. I thought that if I could replace the user input {{timer}} with something that would run my alert. So after some trial and error I used ```')alert('``` to produce the desired result.

### Level 5

Originally I tried injecting new things into the sign up bar, just like the previous few levels, but after a long run of unsuccesful attempts, I decided to try a different approach, the only other vulnerabilities I could think of is changing authorization using cookies, or manipulating the URL. Cookies were not relevant here so I tried messing with the URL, while looking over the code I noticed the ```next``` parameter would change with each new template render, so I thought i'd target that. I tried substituting ```alert()``` for confirm in the URL: ```https://xss-game.appspot.com/level5/frame/signup?next=confirm```, but this did not work. I noticed that I needed some way for the alert() to actually run, and not be just treated as part of the URL. So after some research I discovered that I could use ```javascript:alert()``` to achieve what I wanted to do, using this URL I managed to beat this level: ```https://xss-game.appspot.com/level5/frame/signup?next=javascript:alert()```

### Level 6

For this problem I realized that the only 



