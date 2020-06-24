# node.js

> **what is node.js?**


node.js takes out javascript from the browser and gives it to the users, so he can use it on his computer outside of the browser.

This means node.js = javascript outside of the browser.
(that is not related to the browser)

Through this we can do stuff in our filesystem, for example create server, create web scrapper to go to some page and get some information.


> **When should we use node.js?**

- When we build backend, server
- When we want to use javascript for both frontend and backend.
- If we want to start developing fast, customize almost everything.
- If you need to move lots of data, handle data (node.js performs very well on data)
- Saving data, showing data, creating data, deleting data, showing it as fast as we can like realtime, update location, scales server very well(like chat, uber)
- Static website, not interactive

---

# Server

> **What is a server?**

physical server: Computer connected to the internet, lots of hard drive, memory, board. Hardwareish computer.

Software server: piece of code connected to the internet, sort of network (public, private). Answers to URL, accepts connection. 

Answers connection request. Listening to some connection.

Servers do open connection, listen connection, handle some files, send some htmls, save some data, get data from form.

> **npm**

**npm = Node Package Manager**

if I’m sharing this proeject with my friends/ or this project is open source or something, you have to upload express together.
Centralized place that everybody in node.js world.
Dependencies -> this is what our project needs to survive. (in our case, it’s express)

## authentication

> **process**

user => github website (auth)

github website (auth) => /auth/github/callback

githubLoginCallback gets (profile) (we can do finding user by email, or by github ID)
=> cb(is there any error?, is there any user?) ((error)/(null, user))

If (null, user)
=> cookie = makeCookie(user)

savedCookie = saveCookie(cookie)

sendCookie(savedCookie)