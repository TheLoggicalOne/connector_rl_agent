# Reinforcement Learning Agent To Learn and Make Optimal Choices To Connect To VPN
## Why and How to Use connector_rl_agent
- This is for you if:
    -  you struggle connecting to a VPN server or(other servers)
    - you have to try many times
    - you have to try with many different servers 
    - you have to try with many differentsettings
    - you have to type your user and pass and other info many times
- Even If you have fine connections to servers, but still you prefer making the best choices(in term of speed, connection quality or even your made up quality that only you care) when choosing your servers and their configurations, this will be for you
- This Project is done on my machine, Ubuntu 20.04. I have no idea weather it is compatible with other systems
- I am using openconnect commandline interface, for any other connection type related script/fucntions should be added to appropriate location
   - This appropriate location is to be determined 
## Project Description and its components
This project has three main component:
### auto_connect_agent:
an executable program that tries to connect to VPN servers by trying all possible configurations fed to it by the RL Agent  
This program should be able to:
- create a connection based on type of connection and its configurations passed to it as parameter
    - ideally type of connection should be a parameter two
    - we start with openconnect command line interface as our first type of connection
    - ideally we want provide the possibility of adding different type of connections and their type without breaking previous code
- Our first idea for high level design that satifsfies these requirment: 
    - we use a high level function to get type of connection and its configurations as parameters and for each given type of connection call corresponding actuall script/function and pass the parameters to it  

### rl_agent 
The Reinforcement Learning Agent will learn and do optimal choices(actions) for some subset configuration options based on hitorical data of all previous attempted connections which are saved on a data base  
   - the rl_agent at start could just rank different choices based on frequency of success and choose from ranked list one after another
   - could be modeled and solved as a multi armed bandit problem  
        - arms are different configuration choices
   - dynamical multi armed bandit seems to be a better choice!
     - if an specific arm(specific config choice, let say server address) has really high reward compare to others and we have tried it twice in this second and failed both times, traditinal multi armed bandit will still prefer this choice to others, we could (hopefully) lighten these problem by considering effect of time and maybe weighting newest data higher
   - even better, contexual bandit, that can use other  
    parameters like time of day, week or even year, type of failed connections or even type of successfull connections 

   - The Best: General Reinforcment Learning Model: by considering logs and exit codes as information that will shape different nodes and considering many of config optins as actions


### historical_data 
a database(could be a file at start) for:
 - recoding hitorical data of all previous attempte connections
 - auto_agent_connect should be able to write data generated from its actions to this database
 - rl_agent should be able read the data from this database
    - we also want rl_agent to get only updates (new data) to this database

 - note that rl_agent might have its own database for ranking and scoring different choices and how to execute different connecting strategies

## Plan and Roadmap
### Stage One: Create A reasonable working 
#### Create Project Structure
#### Create auto_connect_agent 
- auto connect script/fucntion compatible with openconnect command line interface in Ubunto

#### Design the historical data db
#### create a fucntion/script that interact with auto_connect_agent and saves generated data to db
#### create simple rl_agent just based on success frequency
### Stage Two
#### more advanced rl_agents
#### generalize components API to provide opportunity of working with different connection types and rl_agents

