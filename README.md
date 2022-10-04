# SafeChat - a social platform with secure chat & share

- Project name: SafeChat
- Time: 9/26/2022 - 10/227/2022
- Purposes:
  - demonstrate ability to use fastAPI in microservices
  - demonstrate ability to use MongoDB to ...
  - demonstrate ability to work with others in a team setting
- Team members & responsibilities:
  - Austin Miller: ???
  - Chris Tsoi: ???
  - Echo Yang: ???
  - Qingying Meng: ???

---

## Overview:

- Wire-frame diagram:
  ![Wire-frame diagrams](/images/wireframe.png)

- App preview:
  ![App preview](/images/LsJazlDzWa.gif)

---

## Getting started:

1. Fork the repository at
2. Add teammate to the project: GitLab > Project Information > Members > Invite members (as Maintainer)
3. All member clone the same repo to their computer:
   ```
   git clone https://gitlab.com/chatapp12/chat-app.git
   ```
4. Run docker-compose up

---

## Working in development branches:

1. Creates a dev-branch:

   ```python
   (main) $ git checkout -b my-branch  # create and change to a new branch
   (my-branch) $  # <-- hey look, I'm in my new branch
   ```

2. Now each team member can mangle all they want without affecting the main branch or anyone else's dev-branch
3. When a team member's branch is at a stable state and ready to be pushed to the main branch, follow these steps:

   ```python
   (my-branch) $ git checkout main    # switch to main branch
   (main) $ git pull                  # get latest from remote
   (main) $ git checkout my-branch    # switch to dev branch
   (my-branch) $ git merge main       # merge latest into dev branch
   ... handle any merging here
   ... test out your code
   (my-branch) $ git checkout main    # switch to main branch
   (main) $ git pull                  # test for changes on remote
   ... if no changes proceed,
   ... if changes go back to line 3
   (main) $ git merge my-branch       # merge dev branch into main
   (main) $ git push                  # push changes to the remote
   (main) $ git checkout my-branch    # change back to dev branch
   ```

4. Merge conflicts

---

## Virtual environment & FastAPI installation:

- FastAPI
  - fastapienv
    - bin
    - lib
  - chats.py

1. change shell from zsh to bash:

   ```python
   chsh -s /bin/bash
   ```

2. create virtual environment with project directory:

   ```python
   cd desktop
   mkdir FastAPI
   cd FastAPI
   pip list  # check if virtualenv is already install
   pip install virtualenv  # if not, install virtualenv
   python -m venv .fastapienv  # create virtualEnv for fastapienv
   # activate virtualEnv:
   source .fastapienv/bin/activate
   # [OPTIONAL] deactivate virtualEnv:
   source .fastapienv/bin/deactivate
   ```

3. install all of the dependencies for FastAPI:

   ```python
   cd FastAPI
   pip install fastapi[all]
   ```

4. create chats.py and edit:

```python
from fastapi import FastAPI  # import FastAPI into chats.py
my_app = FastAPI()  # create fastAPI application, chat_app
# decorator: all GET requests to the "<<...>>" path should be handled by the upcoming function
@my_app.post("/api/test")
async def first_api():
    return {"message": "Hello FastAPI"}

# start application: run uvicorn & start relooader and server process
uvicorn chats:my_app --reload
# uvicorn running on http://127.0.0.1:8000 & shows {"message": "Hello FastAPI"}
```

---

## Deploy:

1. Setup and deploy group project template
2. Create Heroku account. Only one needed for the project, but all should create one and play with it.
3. Get Heroku API Key: Heroku avatar > Settings > API Key > Reveal
4. Create a Heroku application: upper right corner "New" > Create new app > App name: my-safe-chat
5. Set 2 env vars in `.gitlab-ci.yml`:
   - `PUBLIC_URL`: "https://USERNAME(qmeng222).gitlab.io/PROJECTNAME(safe-app)"
   - `REACT_APP_API_HOST`: "https://HEROKU-APP-NAME(my-safe-chat).herokuapp.com"
6. Set Heroku Config Variables:
   Heroku app name > Settings > Config Vars > Reveal Config Vars > Add
   - CORS_HOST (as key): "https://USERNAME.gitlab.io" (as value)
7. Set GitLab CI/CD Variables (Settings > CI/CD > Variables > Expand > Add variables, one by one):
   1. HEROKU_API_KEY: value from step #2 above. This must be "masked" and "protected".
   2. HEROKU_FASTAPI_APP: HEROKU_APP_NAME
   3. REACT_APP_API_HOST: "https://APP-NAME.herokuapp.com"

7) Push to main, go watch the CI/CD pipeline in gitlab
8) When that succeeds, go see if your site is up: Settings > Pages > click the link
