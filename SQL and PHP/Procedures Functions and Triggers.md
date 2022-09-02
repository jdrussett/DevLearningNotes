	• Routines: program modules that execute on demand
		○ Procedures: routines that do not return values & can take input or output parameters; must be explicitly called
		○ Functions: routines that return values & take input parameters
		○ Triggers: routines that execute in response to a database event
	• Structure of routine language:
DELIMITER delimiter_symbol
CREATE routine_name
BEGIN
     [DECLARE variable declaration]
     ….
END delimiter_symbol
DELIMITER;
		○ DELIMITER: changes delimiter to a symbol specified, often '$$'; delimiters distinguish one line of code from another
		○ CREATE routine_name: handles the actual creation of the procedure/function/trigger
		○ DECLARE: provides ability to specify variables, constants, & cursors
		○ BEGIN: executes the program logic such as IF & LOOP
		○ END: finishes the routine
		○ DELIMITER is used again at the end of the code to set the delimiter back to normal
	• Declaring a variable will specify the value of certain variables that can be used by the code later on in the processing logic
		○ Example:
DECLARE variable_name <data_type>;
		○ Then you can test a variable with:
SELECT column_name INTO variable_name FROM table_name …. ;
	• IF/THEN logic: evaluates criteria & returns certain results when criteria are met
		○ Example:
IF (condition) THEN 
     logic if condition is true;
ELSE
     logic if condition is false;
END IF;
	• PROCEDURE: a routine that doesn't return values & can take input or output parameters; must be explicitly called
		○ Example:
DELIMITER delimiter_symbol
CREATE PROCEDURE procedure_name (IN/or/OUT/or/INOUT variable_name data_type(), other data definitions …. [as many variables as necessary])
BEGIN
     DECLARE variables/cursors/constants;
     select statement ….
END delimiter_symbol
DELIMITER;
		○ To call a procedure:
CALL procedure_name (variable1_name, variable2_name, ….);
		○ IN: passes argument to stored procedure which will not change even if it is changed in the procedure
		○ OUT: variable can change & be used outside procedure but initial value cannot be used
		○ INOUT: passes argument to stored procedure which can change & be used outside the procedure
	• FUNCTION: a routine that returns values & may take input parameters; must be explicitly called
		○ Example:
DELIMITER delimiter_symbol
CREATE FUNCTION function_name (variable_name data_type(), other data definitions …. [as many variables as necessary; can also leave entirely blank])
RETURNS data_type
BEGIN
     DECLARE variables/cursors/constants;
     select statement ….
     RETURN (variable_name);
END delimiter_symbol
DELIMITER;
		○ What is contained within the DECLARE/RETURN lines is what the user wants to see as a result of the function
		○ It is critical to provide an INTO statement which identifies what field in the selection is being passed into the declared variable
		○ To call a function:
SELECT function_name (variable_name) FROM DUAL;
	• Various ways to handle missing data:
		○ Substitute estimate of missing values
			§ Based on calculation of other values/default value if not specified
		○ Construct report listing missing values
			§ In the form of report table
		○ Ignore missing data unless value is significant
			§ Check for significant values before inserting/updating data in database
	• TRIGGER: a routine that is invoked automatically when a change is made to the data on the associated table; driven by events, not called independently
		○ Example:
DELIMITER delimiter_symbol
CREATE TRIGGER trigger_name [BEFORE/or/AFTER INSERT/or/UPDATE/or/DELETE] ON table_name
FOR EACH ROW [FOLLOWS/or/PRECEDES] existing_trigger_name
BEGIN
     select statement ….
END delimiter_symbol
DELIMITER;
		○ BEFORE/AFTER INSERT/UPDATE/DELETE will determine when the trigger execute
		○ FOR EACH ROW will execute the trigger for each row of the table
FOLLOWS/PRECEDES determines whether trigger will execute before/after other existing triggers