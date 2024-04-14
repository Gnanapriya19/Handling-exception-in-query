IMPLEMENTATION OF HANDLING EXCEPTION IN QUERY 
 
AIM: 
To handle exceptions in PL/SQL Program 
 
PROCEDURE: 
An error occurs during the program execution is called Exception in PL/SQL. 
PL/SQL facilitates programmers to catch such conditions using exception block in the program and an appropriate action is taken against the error condition. 
There are two type of exceptions: 
o 	System-defined Exceptions o 	User-defined Exceptions 
SYNTAX: 
DECLARE  
   <declarations section>  
BEGIN  
   <executable command(s)>  
EXCEPTION  
   <exception handling goes here >     WHEN exception1 THEN         exception1-handling-statements      WHEN exception2  THEN         exception2-handling-statements      WHEN exception3 THEN         exception3-handling-statements  
   ........  
   WHEN others THEN  
      exception3-handling-statements  
END; 
 
10. IMPLEMENTATION OF HANDLING EXCEPTION IN QUERY 
 
COMMANDS: 
SET SERVEROUTPUT ON; DECLARE  
   c_id customers.id%type := 8;     c_name customerS.Name%type;     c_addr customers.address%type;  
BEGIN  
   SELECT  name, address INTO  c_name, c_addr  
   FROM customers  
   WHERE id = c_id;   
   DBMS_OUTPUT.PUT_LINE ('Name: '||  c_name);  
   DBMS_OUTPUT.PUT_LINE ('Address: ' || c_addr);  
EXCEPTION  
   WHEN no_data_found THEN  
      dbms_output.put_line('No such customer!');     WHEN others THEN  
      dbms_output.put_line('Error!');  
END;  
/ 
OUTPUT: 
No such customer!   
PL/SQL procedure successfully completed.  
 
User-defined Exceptions DECLARE  
   c_id customers.id%type := &cc_id;     c_name customerS.Name%type;     c_addr customers.address%type;      -- user defined exception     ex_invalid_id  EXCEPTION;  BEGIN  
   IF c_id <= 0 THEN  
      RAISE ex_invalid_id;  
   ELSE  
      SELECT  name, address INTO  c_name, c_addr  
      FROM customers  
      WHERE id = c_id; 
      DBMS_OUTPUT.PUT_LINE ('Name: '||  c_name);   
      DBMS_OUTPUT.PUT_LINE ('Address: ' || c_addr);  
   END IF;  
EXCEPTION  
   WHEN ex_invalid_id THEN  
      dbms_output.put_line('ID must be greater than zero!');     WHEN no_data_found THEN  
      dbms_output.put_line('No such customer!');     WHEN others THEN  
      dbms_output.put_line('Error!');   
END;  
/ 
OUTPUT: 
Enter value for cc_id: -6 (let's enter a value -6)  old  2: c_id customers.id%type := &cc_id;  new  2: c_id customers.id%type := -6;  ID must be greater than zero!   
PL/SQL procedure successfully completed.  
