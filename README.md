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

