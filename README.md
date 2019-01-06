# build-a-blog-web2py

Implementing and providing the steps to create a blog using web2py and python. Full Stack Web development. 

**Designing Our Blog App**

 Fullstack web development is creating a frontend that has a backend i.e a database associated with the frontend. Therefore, we have two designs of concern.   Our application design and our database design.

 # Application Design  

 **Post**

 This is where the user posts information 

 **View**

 This is where the public views the blog post. 

# Data Base Design 

- Blog title - typically shows up as the headline to the blog post 
- Blog details - describe the information we want to display in the post 
- Blog Image  - a url that points to the image in the URL
- Blog URL 
- Blog Category - divides the post into different sections 
- Blog Date Posted

To begin let's start off with the database design. The database administration works within the Models section.  

- Go to your project or create one if neccessary. If you have not downloaded web2py http://web2py.com/init/default/download choose windows or mac for normal users. Then proceed to extracting the files and then starting the web2py server. From there you will want to click admin and get into the settings. Create a new project and then you are ready to proceed. 
- Click manage then edit next to the project name 
- Under Models click edit for the db.py file. 
- scroll down to the bottom of the page.   The very last line. 
- SQLite is embedded with web2py 
- some knowledge of SQL may be needed. There are many sites that will provide you with this knowledge but I will recommend a couple   codecademy.com free resource that will give you enough to understand.  though using python with a database will still be a bit different.  For this reason I will supply the SQL code but SQL is not a hard language to learn it really often times reads like plain english its just knowing whats all available that coould make it tough. Repetition is the key to mastery.   
- db.define_table is how we will define a table   
- add the following at the bottom of the db.py file. 
- 
db.define_table('blog', 

    Field('blog_title), 

    Field('blog_details'), 
    Field('blog_image'),


    Field('blog_url),

    Field('blog_category'),

    Field('blog_date_posted')

    )

Hopefully, you notice that each field representents everything we outlined at the begining as needed properties.  If you are familar with Microsoft Excel a database is alot like it.   You have these cells columns and rows.   each column in a database has to be set up. usually you give it a name, and you give it a type. You can even set some fields to accept no data and others to require something be entered in. Which makes it different than excel. With excel you enter data on the fly. With database adminstration you have to architect everything.  Best practice is writting it down or drawing it out before you start coding. Similar to this read me defining what we needed then implementing it. 

We then use these paramaters or fields to create and update information we plan to save in the table.  For a full web site  you would be likely storing usernames and passwords,  messages on the board as well as messages between users. You would also have to protect certain information so that it is not available to others if private.  This is a bit complex for this repo but provides understanding of real world uses for databases.

Imagine amazon, how do they know what others purchase?  Think about it the last time you made a purchase you were recommended another product and they stated others have purchased this with what your ordering or considering ordering.  Well database adminstration comes into play.  They save the orders and then analayze it.  This is what tells them what the top pairs are to recommend items.  Imagine walmart or target you go to these department stores and do you consider they randomly placed items on shelves or in a particular order? Its very likely they have analyzed each purchase and group items based off their popularity of being purchased together.  Least likely to be purchased will be positioned along the route of most likely to be purchased items. This gives you a chance to walk past and see these items on the way to the items you came to purchase.  They do not design the store so you can come in see what you came to buy and leave quickly they want to lure you into purhcasing other items.  This is a very common business practice and the algorithm while simple is only complex due to the size of the items the store carries. It is often a practice I have notice where these fequently bought together items receive  price changes.  Maybe the next time you go to the store you can spot it out.  Here you have  item A  marked down 10cents.   But item B  (frequently bought with item A) is not discounted or even marked a bit.   You think you are getting a sale but not always if you purchase both items together. Sometimes though both items will be marked down together but not often. Again all of these is complex information for our simple blog but hopefully it excites you along the journey of being the go to person when the general manager of the store wants advice on what items should be grouped together.  For assistance for more deep learning in web2py take a look at the following http://www.web2pyref.com/  

Back to the blog. A high occurence of certain keywords on your blog could point out that your blog is good for advertising that key word if there are products associated with the keyword. The keywords may also tell you more about the type of users you have. But all of these can be analyzed with ages as sign up parmaters and other key information. 

http://www.web2py.com/examples/static/web2py_cheatsheet.pdf has  some references the of what we can use.   Take a look at the validators section. 

CLEANUP, CRYPT, IS_ALPHANUMERIC, IS_DATE, IS_DATETIME,
IS_DATETIME_IN_RANGE, IS_DATE_IN_RANGE,
IS_DECIMAL_IN_RANGE, IS_EMAIL, IS_EMPTY_OR, IS_EQUAL_TO,
IS_EXPR, IS_FLOAT_IN_RANGE, IS_GENERIC_URL, IS_HTTP_URL,
IS_IMAGE, IS_INT_IN_RANGE, IS_IN_DB, IS_IN_SET,
IS_IN_SUBSET, IS_IPV4, IS_LENGTH, IS_LIST_OF, IS_LOWER,
IS_MATCH, IS_NOT_EMPTY, IS_NOT_IN_DB, IS_NULL_OR, IS_SLUG,
IS_STRONG, IS_TIME, IS_UPLOAD_FILENAME, IS_UPPER, IS_URL

Validators work within the models to make sure the data is accurate. For example making sure we are getting a url for our url field. Making sure our date field has an actual date etc. Let's add validation to the table fields. 

Before I continue with the steps lets point out some potential issues we can run into.  After your field title you need a comma and then the validation.  All validation will be functions so they must be called (). 
To declare the type we need use  type=   and if the field is required   use requires =   if you need to set the type and requires  perform the type first.  Alright let's continue. Also use underscores not dashes or it will produce an error. 

- update your code at the bottom of the db.py file to the following: 
    
        db.define_table('blog',
                Field('blog_title', requires=IS_NOT_EMPTY()),
                Field('blog_details', type='text'),
                Field('blog_image', requires = IS_URL()),
                Field('blog_url', requires=IS_URL()),
                Field('blog_category', requires=IS_IN_SET(['News', 'Events', 'Sports', 'Business'])),
                Field('blog_date_posted', type='date', requires=IS_DATE())
                )

Let's go over what we have done and while we do so be sure to make sure you have commas in between everything needed and () at the end of functions.  

**Field**
This is similar to a class syntax in python.   We are accepting paramaters within the Field class so each parmater needs to be seperated by a comma.  The field name comes first and will always be a string. For SQL is best to use single qoutes for your string ' ' instead of "". For a full list of field attributes  see that section at http://www.web2py.com/examples/static/web2py_cheatsheet.pdf

**Field Types**
Under the Field Types section at http://www.web2py.com/examples/static/web2py_cheatsheet.pdf 
You will see the following: 
string, text, boolean, integer, double, decimal(n,m), date,
time, datetime, password, upload, blob, json, list:string,
list:integer, reference table, list:reference table

What this indicates is these are the avialble for us to have in the Field. 
This is where we see type = 'text'  by default a string or text which is why for the date we set the type = 'date'  because we don't want a string. 

**Validation**

This is where we make use of the requires by default if you examined the field attributes requires=None here we are updating the fields and making them require certain parmaters.  For example you can't have a blog with a empty title  that wouldn't make sense so we say requires=IS_NOT_EMPTY(). Behind the scenes its a function that is checking if something exisits as the title.  Blog-details doesn't have a requires only a type but if we wanted to would could require that the length be less than or greater than a certain amount.  I think most of the others is self explanatory as the function name speaks for itself as far as what the function does.  By the way this is good practice for when you are creating functions as a programmer. The one that may not make sense though would be IS_IN_SET(). Well a set in python is a unique list.  This means there cannot be the same item in the list twice. Similar to what we are doing with the square brackets here. We don't want the same item in here twice because its not effiecient. Only one is needed.  This will work as a drop down later for our caategory section as available to choose from. If we are later down the line after getting a million users seeing the same category often is getting used there is either a probelm with our drop down selection we need to check or our blog now has a niche.  It might be wise to tailor the blog around this category if has gained popularity give the people what they want. This is another use for the data we are collecting not just saving it for user access but managerial analaysis.  Our data can be viewed and help us problem solve. 

- save your db.py file
- start building the controller for the post page 
- create a new controller named blog
- edit the blog.py file you just created. 
- We will leave the default index function 
- implemente a function post  

        def post():
            form = SQLFORM(db.blog).process()
            return locals()
SQLFORM is an object we are saying  reference the table db.blog and then process() we return the locals of course because we want access to the form in our views page. SQLFORM will build an entire form that includes data validation(very powerful). 

- create view function  featuring a row  variable where we will select the rows by descending order based off the id. 

        def view():
            rows = db(db.blog).select(orderby=~db.blog.id)
            return locals()
rows now selects the rows in db.blog (our table) and orders the return by db.blog.id now we didn't implement id as a parmater but every row in your table will have an id by default usually its numbers  0 1 2 3 4 5 etc.  When we say ~ we are saying do this in descending order  0 1 2 3 4 5 ascending   5 4 3 2 1 0 descending.   ~ is a way that says go in the opposite direction. 

- build post form go to main edit page 
- create a view   controller name (blog) / view name  which will be post  blog/post should be your new view. 
- edit the blog/post view 
- changed the h1 header 
- edit the double curly brackets to show your form  remember  {{=form}} simple.  With this one line of code we will have an entire form with data validation. 
- See  the file  post.html if you need to view how the code should be.
- Go to your post page.    server/appName/blog/post  make sure appName matches the name you gave your application. 
- You should see a blog post paage as well as  a submit button all created for you. Pretty neat.  With advancements such as this in web development creating becomes less difficult so you can focus on the hard stuff. If you are getting ticket  urls  click them read the error understand the error and try to create the problem.  I received a few of them myself and tried to update the code as i got rid of errors. Errors i received was spelling  not using underscores  or using too many underscores. You know your fingers go a little faster than your brain at times. I apologize if you typed my code character for character and received an error message. I would double check though as I did update my code once I got it working. If not I apologize but no negative thoughts it will give you the chance to debug a little for those harder implemntations your going to build. 
- Try to hit the submit button without entering anything in.  Awesome right? Without having do all the coding you have validation. Now go to blog category and choose a category again really neat we have a drop down menu.  This has to be my favorite part about web2py I have done the same blog validation  I did in javascript in way less lines. Now I have yet to implement the styling and extra features my blog application had in javascript but saving this time can perhaps promote better features. I can either take that same time to produce something better or less time to make a clone. 
- Be sure to add a valid title and some details along with a url to an image and a url to a website. 
- In the learning phase it could be difficult to be creative so I will walk you through a blog post I created.  
- blog title   =  Web2py cheat sheet 
- Blog Details the web2py cheat sheet is pretty neat. 
- Blog Image -http://www.web2py.com/init/static/images/logo_lb.png
- Blog Url = http://www.web2py.com/examples/static/web2py_cheatsheet.pdf
- blog category = news 
- blog date posted = (probably the coolest out of the bunch  go head pic a date on the calender, this is acutally built using jquery whether you know jquery or not)
- once all of the fields are filled out click submit it should take you to a blank post form. 

**SQL Forms**

Object that allows you to update, insert, delete,  and automatially generate validation.  There is information on Forms and validationrs in Chapter 7 of the web2py.com book.    http://www.web2py.com/books/default/chapter/29/07/forms-and-validators#SQLFORM

We have already implemented the process method which you will see  where we performed .process(). We will now explore the accepted method. 

- go back to your blog.py file so we can edit it. 
- After clicking edit we will implement a function named display_form 
- it should have a form variable  try to remember what that should look like from previous code. 
- we also need to create some conditionals  if form.process().accepted 
- elif  form.errors  
- else 
- we will also return locals() at the bottom outside of the conditionals.
- Try to set your code up like this before I explain what is nested in each part of the conditionals. 
- Now you should have the conditionals implemented on your blog.py lets fill in the code with the following: 

        def display_form():
            form = SQLFORM(db.blog)
            if form.process().accepted:
                session.flash = 'form accepted'
                redirect(URL('thanks'))
            elif form.errors:
                response.flash = 'form has errors'
            else:
                response.flash = 'please fill out the form'
            return locals()

.accepted is our new method that if we are successful we are going to store the flash value because we need it available on the next page. We wil then redirect the user to a thank you page. 

else if (elif) we will return errors  else we will ask the form to be complted. 

returning the locals. 

- save and then go to the view server/applicationName/blog/display_form
- enter in some data into the fields and click submit 
- you should now see a Thank you page 

**Create thanks function**
- The thanks function can be very simple  have a variable equal a thank you message and then return the locals. 

        def thanks():
            msg = "Thank you for your submission"
            return locals() 

What you have to remember is this has to be inside of the blog.py file. 
The next step is create a view for thanks.   Remember blog/thanks should be your input when creating a new view.  

On the thanks page you just want to make sure your msg from the thanks function is seen and perhaps a header update. 


- lets add an update function to the blog.py 

        def update():
            record = db.blog(request.args(0)) or redirect(URL('post'))
            form = SQLFORM(db.blog, record)
            if form.process().accepted:
                response.flash = T('Record Updated')
            else:
                response.flash = T('Please complete the form.')
            return locals()

Okay all of this looks like previous code.  The only thing new here is using the or keyword in Python on a variable. What we are doing is lets go head and grab the argument if it doesn't exist instead of throwing an error go ahead and redirect the user to the post page. What this is doing is if the first parg db.blog(request.args(0)) is a thing  let record = this if not we will perform a redirect. args(0) is the #id  

Now we will have to create a view for update. blog/update wil be our title this should display our form and we can edit the header to indicate we are updating. 


Now to get to our update page we need to go to  servername/appName/blog/update/(id)  since you have at least submitted one post let's go to 1  so servername/appname/blog/update/1 

All of the information should be entered in. You may also see one additional part of the form Id this is not editable. 

**Build View Page**

- name the view page blog/view 
- Change the header 1 tag to the title of your choice. 
- add a  hr tag under your title 
- start a loop  {{ for x in rows will do the trick}} note you will have to use x.field_name to reference the fields now. 
- create a div that will hold the information for a single blog post 
- nested inside create a image tag that will refence the blog_image 
- create a new div nested inside the original div and under the image. 
- nested within the new dive  create a paragrah that will show the blog_title wrap the blog_title inside a a tag 
- create a new paragrah under the previous and show the blog_category 
- create a new paragraph dn show the blog_details 
- create a new paragraph and show the blog_date_posted 
- outside the divs   add {{ pass }} this is the end of the for loop. 

rows was a variable that was ordered in descending format.   Please note with web2py we can use bootStrap for our styling. I won't go over bootstrap implementation in this readme (perhaps a future readme) however the view.html will use classes referring to bootstrap grid/components. Just know that bootstrap is pretty much ready to use in web2py the files are already present you just have to know how to use it. 

Again {{pass }} tells python to stop running the for loop without this you will defintely continue looping. 

It is also important that you use x.blog_category x.blog_title and remember in order to refer to python you need double curly brackets. 

You should now be able to go to servername/appName/blog/view and see your posts aligned pretty evenly on the page with the latest result at the top. 

# **Database Administration** 

The plan is to import csv files 
Query the database
Inserts, Updates, Deletes 
Export CSV, Render JSON, XML 

