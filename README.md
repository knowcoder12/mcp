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
