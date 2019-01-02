---
layout: post
title: "Erlang learning (7) - Concurrent Programming (3)"
subtitle: "Message Passing System Example"
author: "Bing Yan"
header-img: "img/erlang-7/post-bg-java.jpg"
header-mask: 0.2
catalog: true
tags:
  - Erlang
  - Concurrent Programming
  - Learning
---

## Preface

&ensp;&ensp;&ensp;&ensp;Through the last two learning Blog of Erlang concurrent programming, I master the basic ideas and principles of concurrent programming. <br/>
&ensp;&ensp;&ensp;&ensp;This time learning, by reading and analyzing an example - Message Passing System, I want to expand and consolidate the knowledge of concurrent programming.

## Text

### Message Passing System

**Compile and Use:**

To use this program:
*   Configure the server_node() function with Erlang system of server, I use messenger@Icy.
*   Copy the compiled code (messenger.beam) to the directory on each computer where you start Erlang.

```
%%% Message passing utility.  
%%% User interface:
%%% logon(Name)
%%%     One user at a time can log in from each Erlang node in the
%%%     system messenger: and choose a suitable Name. If the Name
%%%     is already logged in at another node or if someone else is
%%%     already logged in at the same node, login will be rejected
%%%     with a suitable error message.
%%% logoff()
%%%     Logs off anybody at that node
%%% message(ToName, Message)
%%%     sends Message to ToName. Error messages if the user of this 
%%%     function is not logged on or if ToName is not logged on at
%%%     any node.
%%%
%%% One node in the network of Erlang nodes runs a server which maintains
%%% data about the logged on users. The server is registered as "messenger"
%%% Each node where there is a user logged on runs a client process registered
%%% as "mess_client" 
%%%
%%% Protocol between the client processes and the server
%%% ----------------------------------------------------
%%% 
%%% To server: {ClientPid, logon, UserName}
%%% Reply {messenger, stop, user_exists_at_other_node} stops the client
%%% Reply {messenger, logged_on} logon was successful
%%%
%%% To server: {ClientPid, logoff}
%%% Reply: {messenger, logged_off}
%%%
%%% To server: {ClientPid, logoff}
%%% Reply: no reply
%%%
%%% To server: {ClientPid, message_to, ToName, Message} send a message
%%% Reply: {messenger, stop, you_are_not_logged_on} stops the client
%%% Reply: {messenger, receiver_not_found} no user with this name logged on
%%% Reply: {messenger, sent} Message has been sent (but no guarantee)
%%%
%%% To client: {message_from, Name, Message},
%%%
%%% Protocol between the "commands" and the client
%%% ----------------------------------------------
%%%
%%% Started: messenger:client(Server_Node, Name)
%%% To client: logoff
%%% To client: {message_to, ToName, Message}
%%%
%%% Configuration: change the server_node() function to return the
%%% name of the node where the messenger server runs

-module(messenger).
-export([start_server/0, server/1, logon/1, logoff/0, message/2, client/2]).

%%% Change the function below to return the name of the node where the
%%% messenger server runs
server_node() ->
    messenger@Icy.

%%% This is the server process for the "messenger"
%%% the user list has the format [{ClientPid1, Name1},{ClientPid22, Name2},...]
server(User_List) ->
    receive
        {From, logon, Name} ->
            New_User_List = server_logon(From, Name, User_List),
            server(New_User_List);
        {From, logoff} ->
            New_User_List = server_logoff(From, User_List),
            server(New_User_List);
        {From, message_to, To, Message} ->
            server_transfer(From, To, Message, User_List),
            io:format("list is now: ~p~n", [User_List]),
            server(User_List)
    end.

%%% Start the server
start_server() ->
    register(messenger, spawn(messenger, server, [[]])).


%%% Server adds a new user to the user list
server_logon(From, Name, User_List) ->
    %% check if logged on anywhere else
    case lists:keymember(Name, 2, User_List) of
        true ->
            From ! {messenger, stop, user_exists_at_other_node},  %reject logon
            User_List;
        false ->
            From ! {messenger, logged_on},
            [{From, Name} | User_List]        %add user to the list
    end.

%%% Server deletes a user from the user list
server_logoff(From, User_List) ->
    lists:keydelete(From, 1, User_List).


%%% Server transfers a message between user
server_transfer(From, To, Message, User_List) ->
    %% check that the user is logged on and who he is
    case lists:keysearch(From, 1, User_List) of
        false ->
            From ! {messenger, stop, you_are_not_logged_on};
        {value, {From, Name}} ->
            server_transfer(From, Name, To, Message, User_List)
    end.
%%% If the user exists, send the message
server_transfer(From, Name, To, Message, User_List) ->
    %% Find the receiver and send the message
    case lists:keysearch(To, 2, User_List) of
        false ->
            From ! {messenger, receiver_not_found};
        {value, {ToPid, To}} ->
            ToPid ! {message_from, Name, Message}, 
            From ! {messenger, sent} 
    end.


%%% User Commands
logon(Name) ->
    case whereis(mess_client) of 
        undefined ->
            register(mess_client, 
                     spawn(messenger, client, [server_node(), Name]));
        _ -> already_logged_on
    end.

logoff() ->
    mess_client ! logoff.

message(ToName, Message) ->
    case whereis(mess_client) of % Test if the client is running
        undefined ->
            not_logged_on;
        _ -> mess_client ! {message_to, ToName, Message},
             ok
end.


%%% The client process which runs on each server node
client(Server_Node, Name) ->
    {messenger, Server_Node} ! {self(), logon, Name},
    await_result(),
    client(Server_Node).

client(Server_Node) ->
    receive
        logoff ->
            {messenger, Server_Node} ! {self(), logoff},
            exit(normal);
        {message_to, ToName, Message} ->
            {messenger, Server_Node} ! {self(), message_to, ToName, Message},
            await_result();
        {message_from, FromName, Message} ->
            io:format("Message from ~p: ~p~n", [FromName, Message])
    end,
    client(Server_Node).

%%% wait for a response from the server
await_result() ->
    receive
        {messenger, stop, Why} -> % Stop the client 
            io:format("~p~n", [Why]),
            exit(normal);
        {messenger, What} ->  % Normal response
            io:format("~p~n", [What])
    end.
```
Using this program, nodes are started on four different Erlang nodes.  
Four Erlang nodes are started up: messenger@Icy, c1@Icy, c2@Icy, c3@Icy. <br/>

**Test steps:**

1. First the server at messenger@Icy is started up:
2. Peter logs on at c1@Icy; James logs on at c2@Icy; Fred logs on at c3@Icy:
3. Peter sends Fred a message; Fred receives the message and sends a message to Peter and logs off.
4. James now tries to send a message to Fred, But this fails as Fred has already logged off.

**Test results:**

![](/img/erlang-7/messenger.png)

![](/img/erlang-7/c1.png)

![](/img/erlang-7/c2.png)

![](/img/erlang-7/c3.png)


**Knowledge points:**

*   There are two versions of the server_transfer function: one with four arguments (server_transfer/4) and one with five (server_transfer/5). These are regarded by Erlang as two separate functions. <br/>
**Learning notes:as my understanding, this situation as method overload in Java. But I am not sure if Erlang have overload concept?
But anyway, in earlier Erlang practice examples, different match conditions in the same function name and same number arguments are in different clause of same function.**

*   Notice how to write the server function so that it calls itself, through server(User_List), and thus creates a loop. The Erlang compiler is "clever" and optimizes the code so that this really is a sort of loop and not a proper function call. But this only works if there is no code after the call. Otherwise, the compiler expects the call to return and make a proper function call. This would result in the process getting bigger and bigger for every loop.
**Learning notes: the server function call itself, and this should be a recursive call. If it's a recursive call, that means this function has to have a boundary conditions. Without boundary conditions, the recursive call will cause memory problem. But in this function, there is no other code after recursive call, and Erlang compiler can know it's a loop, not proper function call. It's good, but question is besides this way to realize loop, is there more 'official' way for loop?**

*   lists Module: in example, some functions of module list are used. Such as lists:keymember(Key,Position,Lists), lists:keydelete, lists:keysearch. Know the arguments and return type can help decide write the matching condition of clause.

*   exit/1: An Erlang process (conceptually) runs until it does a receive and there is no message which it wants to receive in the message queue. "conceptually" is used here because the Erlang system shares the CPU time between the active processes in the system.<br/>A process terminates when there is nothing more for it to do, that is, the last function it calls simply returns and does not call another function. Another way for a process to terminate is for it to call exit/1. The argument to exit/1 has a special meaning, which is discussed later. In this example, exit(normal) is done, which has the same effect as a process running out of functions to call.

*   whereis/1: The BIF whereis(RegisteredName) checks if a registered process of name RegisteredName exists. If it exists, the pid of that process is returned. If it does not exist, the atom undefined is returned.



## Summary

&ensp;&ensp;&ensp;&ensp; This study is mainly to read and practise this larger example. <br/>
&ensp;&ensp;&ensp;&ensp; During reading this example, I start to have more feelings about the  


## Reference
http://www.erlang.org <br/>
http://erlang.org/doc/getting_started/conc_prog.html <br/>
