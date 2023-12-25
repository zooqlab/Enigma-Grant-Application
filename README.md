Enigma Grant Application
===

**Project website** - https://eniapp.quest/

**Labs Grant Page** - https://labs.wax.io/proposals/164

**Project Development Stages:**
- Quests Functionality (Backend, API, Smart-contract, Frontend)
- Passport Functionality (Backend, API, Smart-contract, Frontend)
- Analytics Functionality (Backend, API, Smart-contract, Frontend)

**Current work in progress on:**
- Design System (Research `completed`, Design `completed`, Frontend `in progress`)
- UX optimization for users - flow of quest creation, community and subscription management (Research `completed`, Frontend `in progress`)
- Passport and project scoring metrics (Reasearch `in progress`)

# Quests Functionality

Quests are the main direction of Enigma, the system of quests allows you to organize a convenient system of work with your community and bring interactivity, using all the possibilities of the Enigma protocol. The creation of communities, quests and tasks is implemented using smart contracts and our backend to validate some data that goes beyond the blockchain.

**The quests are categorized as follows:**
- Backend (work with social networks, profiles, quizzes, analytics of onchain quests fulfillment) - `completed`
- Smart-contract (data storage, record keeping and confirmation of actions) - `completed`
- API (obtaining any data that is related to community, quests, quests and wallets) - `completed`
- Frontend (Community building, quest creation, quest completion, personal accounts and subscriptions) - `in progress`

### Deliverable #1 - Quests stage 2 Development backend, smart-contract, API

**Backend** - [backend source](https://github.com/zooqlab/enigma-backend)

1. We've implemented a full range of validation and data storage through an internal API when creating communities, quests, and tasks. Developed validation by our backend of all important actions in our smart contract that require validation of data outside the blockchain to verify.
2. Structured data handling and split into 3 independent mysql databases, configured security and interaction with them.
3. We developed the mechanics of working with Discord, Twitter data - authorizations, storage of sessions, receiving and validation of all necessary data (subscriptions, retweets, likes, comments, roles), we also developed a Telegram bot to expand the capabilities of the system (the ability to track any available data, both in the group and in the connected group chat).
4. Developed a system for validating Quiz-type tasks.

We have published the source code that is responsible for all data manipulation in the project. Some algorithms contain private data, such as the logic of calculating and validating score, accessing api with our private key.

**Smart-contract** - [smart-contract source](https://github.com/zooqlab/enigma-quests-contract)

We have organized the structure of the quests as follows - 

The community table is the main table that allows users to create "groups" that contain all active quests and to which users can subscribe. Data in the table - community name, avatar, number of subscribers, quest id (+ status). 

Quest table (a quest is time limited event that includes frontend sections with specific tasks), which contains the quest name, description, banner, rewards, number of participants (successful is a participant who completed 1 task) and a list of task ids (+ point rewards and type)

Task table contains information on specific tasks, tasks are divided into different types (onchain, discord-social, twitter-social, tg-social, any, quiz, referral). Depending on the type of task, the cells may contain different content, but it is standardized. The table also contains task name, rewards in points, boolean values, description, the number of those who have completed the task.

The scoring table displays the actual scoring data in the user's scope, it takes into account each individual quest for scoring calculation.

**Action table:**

| Action  | Description |
| ------------- | ------------- |
| **createсommun**  | Creating a community, one user can have an unlimited number.  |
| **editcommun**  | Update some information on the community, such as avatar or name.  |
| **subscribe**  | Subscription by user selected community.  |
| **createquest**  | Creating a quest within the created community.  |
| **editquest**  | Editing some quest information that does not affect the functionality of the quest.  |
| **createtask**  | Creating a single task within a quest.  |
| **deletetask**  | Deleting a task.  |
| **edittask**  | Editing a task, without the ability to change the type and rewards.  |
| **submittask**  | Passing a task and receiving an award.  |

**API** - [api source](https://github.com/zooqlab/enigma-api)

We have developed a feature-rich graphQL api for all users to get the most detailed information on all community and quests on the platform.

Current endpoints of our API:

| Endpoint  | Description |
| ------------- | ------------- |
| **wallets**  | A list of all existing addresses (wallets) in the system that participated in community creation/execution.  |
| **communities**  | A list of all existing communities on the platform by ID.  |
| **communities[id]**  | The data for a specific community, including the owner's wallet, avatar, banner, verification status (retrieved from AtomicHub, Nefty), a list of members and the total count, and a list of quests with their statuses.  |
| **quests**  | A list of all existing quests on the platform by ID.  |
| **quests[id]**  | The data for a specific quest, including the title, owner's wallet, banner, leaderboard (ID - points), a list of sections with tasks (IDs of the tasks themselves).  |
| **quests[wallet]**  | The data for a specific wallet within a quest, including a list of tasks and their status (ID - "success", "fail", "none"), position in the leaderboard, total points in the quest, and a boolean for rewards.  |
| **tasks[id]**  | The data for a specific task, including the title, task type (social, quiz, online, etc.), description, point rewards, participation restrictions, frequency of completion, number of participants, and a list of participants who completed the task.  |
| **tasks[id+wallet]**  | The data for a specific wallet within a task, including the task completion status and the sequential number of task completions.  |

The work within the API will continue as we develop the next stages of the project. We plan to expand functionality and add additional data that can be obtained from the passport and analytics for convenient tracking of all projects and wallets on our platform.
