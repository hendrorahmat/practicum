React App
---
Q: Do the components render correctly? If not, what's wrong in the code?

A: components will be rendered but not correctly, the problem is in the `src/components/Main.js` 
`Attempted import error: 'currentUser' is not exported from '../contexts/CurrentUserContext'.` there is no object with 
name `currentUser`, but you try to import object with name `currentUser` in `Main.js`, so it caused the ui crashed
-----------------------

Q:Is it possible to simplify the project infrastructure? How would you recommend reorganizing it? 

A: actually infrastructure of the project is already good, but there is concern in the `api.js` in the future the file will 
be bigger and bigger, so there will so many function in the file, I would recommend creating folder called service
in the folder services there are files that handle getting data, but it will be nice also if we replace react context with 
redux tool kit (RTK), RTK has powerful libraries to handle data such as manipulating state, react context will be harder
to manage, if our applications bigger

-----------------------

Q: Are all routes configured correctly (including protected routes)?

A: routes not configured correctly, because to determine user is logged in or not just check from the state `props.loggedIn`
imagine if the user visit to the website which have protected routes and suddenly the token removed from backend because 
there are some reason, and there is no props from child element to manipulate `props.loggedIn` to log out user, so the apps
will treat user as logged-in user, and there is no protected routes for EditProfilePopup, that component should be accessed
by user has token if there is no token has been set, the user should redirect to login page

-----------------------

Q: Are the necessary manipulations with the JWT implemented correctly in App.js?

A: I think we should update for handling 400 - 500 status code, because currently in app.js will only handle success status code,
we should handle also if error, get the messages, and redirect to login page if there is error 401 or user has no access

-----------------------
Node APP
---

Q: Do all requests get the correct responses?

A: Yes, it will return response, but there is no proper error response, the error response just only show what the 
error response is, there is no call to action from user approach, so I will recommend implementing 
[Problem Detail](https://www.rfc-editor.org/rfc/rfc7807), and better to split between business logic, database logic
currently all the logic put in the controller, so it will be harder to create unit testing, better to implement repository
pattern, and create services to handle business logic, so it will be easier to create unit testing and mock it, 
and for delete card there is wrong statement, the function called delete the data of the card, but the function does 
update the data of the card
-----------------------
Q: Do these requests correspond to REST API principles?

A: Yes, currently the request url implement semantic rest, but currently there is no api documentation about it
so if we would like to know what is the request body, we should read to the code first, it will be nice if we write api docs
such as swagger
-----------------------
Q: Is the incoming data correctly validated? The Validator.js library is used for validation. What can be removed or 
changed in validation if reviewers only require the URL validation for the image link?

A: we should change models/card.js if reviewers only require image link, we can set name as optional which is when name is exists
the name will be validated, if not exists name will be ignored, we can modify required object such as `required: function() {
return this.name != "" && this.name != null;
}`
-----------------------
Q: Is it possible to add or remove unintended data to database?

A: yes, since image validation just validate url valid or not, we can put data like this http://domain.com/run.php, 
it will be dangerous, so better not just validate the url, but we should validate file extension also
-----------------------

HTML & CSS
---

Q: Is this markup semantically correct? Are there tags that are used incorrectly?

A: there is incorrect for using `<div class="menu">` instead use `<nav>`, The `<nav>` is element defines a set of navigation links

-------------------------
Q: Are there mistakes in the names, in the usage of the blocks, elements, and modifiers?

A: there is inconsistent naming convention, some tag using separate `"__"` and `"-"`, better all class name using same convention
but recommend way is using `""__"`

--------------------------
Q: Are there mistakes in the BEM file structure? Explain in detail.

A: mostly the file structure consist of 1 folder 1 file, we can refactor that using this architecture
`blocks -> {block_name}, {elements_folder -> element_file}` so we don't need to jump into the folder to see the file

---------------------------
Q: Analyze the adaptive design and comment on the decisions that were made in this code.

A: the architecture is good, implementing `BEM` make us easy to make our code scalable, reusable, maintainable, 
easy to understand and
make another engineer fast to learn, 
