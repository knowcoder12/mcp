# mcp


mcp-> context -> ye info jo ai ko dikhati jab vo jawab deta and jaise like history ya tumne summary ya documentation diya jisse dekh ke vo check karega ki kya   answer du acc. to user question

toh tumhe copy paste karke dena padega tumhe vo documentation ya vo info

NOW FUNCTION CALL AAYA OPEN AI KA
ab ai bata sakta ki kaunsa function call karna chaiye 
toh now sab amne tool banae lag gaye GitHub se integrate google drive se data lana toh uske liye tool har cheez ke liye tool bane if folder ko acess toh uske liye tools bane

Story explanation :
now u have the tools now u will use it for creating or automation
1. jira a ticket is raised on it to develop two factor authentication chagot fetch it and okay acc. to that it use GitHub tool to fetch the code base in which dev have to done after  that it fetch sql info how to build schema then tool to connect to two factor info from anything and then build it 

PROBLEM WITH TOOL:
our copany use more then 1 chatbot now for every chatbot we have to create a unique tool for every chatbot so if u use more tool then we need to code more 
2. security as tools are more so there code isin fragments there api key are also present in fragment so maintain them is also time consuming 


MCP HOW IT SOLVE THIS :
major idea here is that we want to develop a soln such if u want to use GitHub there should be one code that can be used with every chatbot 

mcp have two things in it server and client client can be chatbot 

so understacnd mcp is language so now u create server to get weatcher in mcp language so now heavy code is on server side whereas client side u just have to write simple code acess it 
2. its universal as u use any chabot server side code will be same through same client side code u can acess the server side  info eg weather info easily so no need to write sepratecode for it 

now example ur company use weathcer api ,GitHub so now u will write two code in mcp for this 
and with ur three chatbot using same mcp code all of them can get info from tool so no need to write tool code specifaclly for evry chatbot 

now more more server provider is wrting their server in mcp so if tomorrow if a new company chatbot come if its a support mcp client it can use all these server tools for them 





THE WHAT 

SIMPLE ARCH : this is rough dig or workflow how mcp work
1. client ask a question "does there any new commit on my GitHub " host will say i dont have this info so i should check my tool library if i have any tool related to it yes so now use it 


detail arch :
host have clients these client connect or talk to server and fetch and give info and convert back to host understable language and this relation should be one on one 
means -> if we want to use more then one tool we have to contact to more then one server for each server we need a client on host side so every sevrver have its client on host 

benefits :1. as every client is not depend on other if one fail not affect other 
2. parallelism so as each server have client parallel tak can be there as if two tool these can be used parallely as its independent 

3. scalable 



# what is prompt primitive 
so eg u wnat to raise a issue in github now for this u have to use /client-issue tool so u will call it 
and llm will wirte a issue now main problem is here that llm dont know how to write a code so u give something like this to llm 
<img width="357" height="275" alt="image" src="https://github.com/user-attachments/assets/84dfd407-c288-4d96-a4bd-d039a0f37125" />

so now llm will se this and write issue acc.to this 

## ONW THING I WANT TO CLEAR LIKE IN A SERVER GITHUB THERE CAN BE MULTIPLE TOOLS FOR VARIOUS TASKS LIKE ISSUE CREATE INFO FETCH ETC 

read this below thing it basically tells u what to use for spefic tasks 
<img width="747" height="370" alt="image" src="https://github.com/user-attachments/assets/84b34091-7537-4754-a1e2-9cdf36dad593" />



# How data transfer Langauge

Json -rpc is used 
rpc is a langauge or tool that allow us to run fucntion file present on different computer to run on ur comp server like its present locally so basically diff server their data evrything get connected and can be use 

<img width="464" height="542" alt="image" src="https://github.com/user-attachments/assets/cfaa6aae-0dbd-4f65-97fe-a07dda8a06a4" />

**request**
1. so here check like a json list format is used which have jsonrpc its speficy the ver of the json rpc 
2. id : its a unique id given to evry request so when response come it can identify wheich req it belong to
3. methods : it tell what tool to call in server
4. params : to send params like if u want to use calculator so params will have that variable no. on which u want this operation to done

**Respone**
1. its have id jsonrpc but
2. result in result it have given list of all tool as u called the tool/list so its like this 


## why json rpc not rest api 
1. so understand as rpc is lightweight as not imp to use http
2. bi directional -> server can also send info to client
3. its transport agnostic means u u can use any transprt layer protocol http or anything else

## Mcp types of server 
local and remote server
1. local : so in this type of server stdio is used what is it so stdin means input the program reads
how it work host launches server as suborocess on machine
host client write json rpc message int server as stdin
server read those message and give stdout
used for local work like related to ur machine super fast and all, nitish campusx had given a good example to understand this better if u want u can check it out his mcp arch 3rd video

2. remote : (http+sse)-: host send a post req with json rpc as payload, this also use all authentication used in http
sse: its an extention of http, used to stream msg so instead of sending big chunk in one go it send it in small chuncks


## the lifecycle of mcp
now we will try to understand how client and server connect to each other 
this is three way req res based  -: checkout video no. 4 for seeing the file and code used to develop connetion 
1. client send a req with some info to server
2. server send res
3. cleint again send a confimation

between all his server cleint cant send anything to each other 

**version negotiation**
its means like if server and client have different prtocol ver. so it will check its config if cleint have that server server with it if yes they can connect f no they wont connect 

**capability negotiation**
so this is the way trough which cleint and server exchange their feature with each other 
1. understand what feature client offer to server : cleint give root acess if want to fetch some files or read anything
2. sampling : server can also send to use some tool like ai server want to use cleint ai for some task eg. summarization
3. there can be case where eg. server want to acess github but it didnt have the key to acess so alert cleint to give it

1. Now what server offer to cleint : prompts u can give tools , resources and logging is also can be shared

**Subcapblity**
listchanged : so take a case where a new tool is added to server in between so now server will tell client okay so now i have this capablity too 

## tool discovering 
So understand this thing when connection is setupt client ask server tool/list so server gave back list of all tool
so now hub decide which tool it want to use and like if we take local server so in it server is the ur desktop file system and client ask for permission to read .. etc

## shutdown phase 
one side intiate shutdown 
no special json rpc shutdown msg is defined 
transport layer is responsible for signaling termination 

shutdown in stdio : cleint intiated shutdown : in this cleint close input stream and wait fro server to exit if it doesnt it send sigterm poilitly tell server to exit is still not sigkill force server to exit 

➡️ shutdown in http : cleint intiate shut down : in this client tell to stop sending msg and it stop 
server intiate shutdown : server remove its connection with client so it can be becuse server is down so cleint try to reconnect or etc 

⭐ **Ping** : it is used to check if the other side is still active it also sended b/w long running task if server and cleint didnt intract for long time in b/w 

⭐ **Error handling**: so there can be case where some error occur common error are:
1. mismatch version
2. calling tools method tht didnt exist
3. internal server failure
4. timeout exceeded  client cancel request
5. malfored hson rpc msg

⭐**Timeout**: There can be a chance like in which some process or resource is running and capturing memory so we cant let this happen for long time so that time timeout cancel or free that resource 

⭐**Progress notifaction**: it give notification abt the progress like if 400 files is scnning so it will give u progress update 








# THE HOW 

## how to use server  with claude 
**connectors**: these are the connector that is present in claude directly used like u can click dot button and connec to ur github etc but main problem we cannot make connector for every mcp



 fastmcp vc mcp:
 pip install mcp[cli] and fastmcp both are same only diff is that before they both are together but after some time they seprated and made their own version 

 mcp old ver is traditional way and hard way 
 fastmcp is written in mcp old but its more easy then it 

 ## Imp sun local server claude se kaise connect ye video se dekh le badiya main likh ni raha jab use aay tab use karna  
Aur ek aur cheez ki fastapi ki app ko directly fastmcp mein convert kar sakte hai 

## remote mcp server

this server is deployed on some heavy server that is running continously
