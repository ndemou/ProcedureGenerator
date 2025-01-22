# ProcedureGenerator

A program that generates simple procedures in an a webpage from text

An example of a process 

    # Part 1
     
    Please answer the following questions:
     
    Q: What is the city: [city]
     
    Q: How many servers in city: [server_nr]
     
    Q: What model is the laptop: [model](One of: Dell, Lenovo)
       (You can have the properties just after the variable if you prefer)     
     
    Q: Password: [password]
     
    {
          // all code in {...} like this is prefixed with this line: 
          //    error_message=""; warning_message=""; end_process =false
          // and run with an eval()
          // If the code above sets error_message it is shown, and validation fails
          // If it only sets warning_message it is shown but it is not failing validation 
          // If it sets end_process then the process ends 
     
          let country=""
          if (city == "Athens") {country="Greece"}
          if (city == "Sofia") {country="Bulgaria"}
     
          if (city == "Athens" && server_nr<5) {
                error_message = "No way you have less than 5 server at Athens"
          }
          if (city != "Athens" && server_nr>5) {
                warning_message = "Warning: you have unexpectadely many servers"
          }     
          
          min_nr_of_servers_to_check = Math.max(1, Math.floor(server_nr / 3))
    }
     
    --- 
     
    Visit the offices at {city}.
    
    *** 
    Note: Avoid weekends because most offices are closed
     
    --- 
     
    # Part 2
    
      
    Ask to show you at least {min_nr_of_servers_to_check} servers
     
    ---
     
    Q: Enter the name of one user: [user]
     
    ---
    
    (Numbered lists are always rendered as separate steps; no need to put --- between)
    
    Perform these steps:
     
    1.	Open the box
    2.	Remove the contents
    3.	Replace them with sand
    4.	Close the box
     
    ---
    
    (but unordered lists like this are kept together in one step)
    
    Perform any of the following:
     
      * Ask for help
      * Do everything by yourself
      * A mix of the two
    
    (a separator --- is implied here because a # header follows) 
    
    ## Part 2.2
     
    {showif model=="Dell"  
    Call Quest and ask them to service the laptop
    (Dell is the official service point for Dell)
     
    {end}  (this signals the end of the process)  
    }
    
    ---
     
    {showif model=="Lenovo"  
    
    Call Oktabit and ask them to service the laptop  
        {showif server_nr>5 (single = are replaced with == before expression is fed to eval)
    and to raise priority because it affects a lot of servers
    (notice that we can have nested ShowIfs)
        }  
    (Oktabit is the official service point for Lenovo)
     
    ---
    
        {Repeat Until last_server="Yes"
    Check if server has up-to-date firmware
    
    Q: Was this the last server? [last_server]
        }
        Any single = in the expression is replaced with == before it is eval()ed
        You can also have these similar commands: 
           {Repeat while expression 
           {Repeat var times
        The special variable iteration is available within Repeat var times loops 
        and is set to 1 for the first iteration, 2 for the second, e.t.c.
    
    }
     
    ---
     
    Ask {user} to open an excel sheet.
