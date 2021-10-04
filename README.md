# f8-inter-vue
F8-th Technical Interview Task Details:  Your task is to write a web client using Vue JS that makes a request every second to an API. This API will return six usernames and a number associated to each one. Within the API, pull the six usernames from a database then randomize numbers for each of them between 0 and 100. When the data is returned to the web client, it should then be parsed and displayed in a panel that features pictures for each user, their username, and the number. You should also somehow highlight the user with the highest score. 


# Instructions For Running the code.
- Make sure you are in the master branch within github, then pull the repo onto your local environment.
- open a terminal in the project folder and run commands: 
  - npm install json server -g
  - json-server db.json
 -open a second terminal and run command 
  - npm run serve
 - within the browser open the links
    - http://localhost:3000/users   --> this link contains the the list of users in JSON format
    - http://localhost:8080/        --> You can see the lauched site on the local environment
