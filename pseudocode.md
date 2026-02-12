//TASK ONE: USERNAME CHECK
FUNCTION Username_check()
    BEGIN FUNCTION
   
    SET User TO ""
    WHILE User is "" DO
        SEND "please enter your User:" TO DISPLAY
        RECIEVE User FROM (string) KEYBOARD
    ENDWHILE

    SET user_len TO User.LENGTH()

    WHILE user_len is < 4 OR user_len > 12 DO
        send "Username should be between 4 and 12 characters:" TO DISPLAY
        RECIEVE User FROM (string) KEYBOARD
    ENDWHILE
    RETURN User & 'is valid'
ENDFUNCTION

//ALTERNATIVE APPROACH

FUNCTION username_checker()
    BEGIN FUNCTION
    SET flag TO True
    WHILE flag = True DO
        SET username = RECIEVE username FROM(STRING) KEYBOARD
        IF 3 < LEN(username) < 13 DO
            RETURN "Username accepted " TO DISPLAY
            SET flag TO False
            ENDWHILE
        ELSE:
            SEND "The length of username should be between 4-12 characters" TO DISPLAY
ENDFUNCTION

//TASK TWO: STOCK LEVEL ALERT
FUNCTION stock_level()
    BEGIN FUNCTION
    SET stock_level TO -1

    WHILE stock_level < 0 DO
        RECEIVE stock_level FROM (INTEGER) KEYBOARD
        IF stock > 20 THEN
            SEND 'High stock' TO DISPLAY
        ELSE IF stock > 5 THEN
            SEND 'Stock OK' TO DISPLAY
        ELISE IF stock > 0 THEN
            SEND 'Low stock' TO DISPLAY
        ELSE IF stock = 0 THEN
            SEND 'Out of stock' TO DISPLAY
        ELSE
            SEND 'Invalid response'
        ENDIF
    RETURN 'Stock level checked'
    ENDWHILE

ENDFUNCTION

//TASK THREE: MAINTENANCE CHECKER
FUNCTION maintenance()
    BEGIN FUNCTION
    SET daysSinceLastService TO RECIEVE days FROM(INTEGER)KEYBOARD

    WHILE daysSinceLastService NOT number DO
        SEND "Please enter a number"
        SET daysSinceLastService TO RECIEVE days FROM(INTEGER)KEYBOARD
    ENDWHILE

    WHILE daysSinceLastService < 0 DO
        SEND "The number must be 0 or more!"
        SET daysSinceLastService TO RECIEVE days FROM(INTEGER)KEYBOARD
    ENDWHILE

    SET serviceFrequency TO ""
    SEND "Please choose an option for you service frequency: 1.Weekly  2.Monthly" TO DISPLAY
    SET frequency TO RECIEVE frequency FROM(INTEGER) FROM KEYBOARD

    IF frequency = 1 THEN
        SET serviceFrequency TO 7
    ELSE IF frequency = 2 THEN
        SET serviceFrequency TO 30
    ELSE 
        SEND "Sorry you did not enter a valid option " TO DISPLAY
    ENDIF

    SET daysleft TO serviceFrequency - daysSinceLastService
    IF daysleft IN [1,2] THEN
        SEND "Due soon" TO DISPLAY
    ELSE IF daysleft > 2 THEN
        SEND "Not due yet" TO DISPLAY
    ELSE IF daysleft = 0 THEN
        SEND "Due now" TO DISPLAY
    ELSE IF daysleft<1 DO
        SEND "You are late for the service"
    ELSE 
        SEND "There was a problem"
    
    RETURN "Service day function complete"
ENDFUNCTION

//TASK FOUR: PRIORITY CLASSIFER

FUNCTION priority_checker()
    BEGIN FUNCTION
    SET Array_conditions TO ['Good', 'Worn', 'Critical']
    SET Array_in_use TO ['Yes', 'No']

    SET condition TO ''
    WHILE condition NOT IN Array_conditions
        SEND 'Enter condition from list' TO DISPLAY
        RECEIVE condition FROM (STRING) KEYBOARD
    ENDWHILE

    SET days_last_service TO -1
    WHILE days_last_service < 0 DO 
        SEND 'Enter days since last service' TO DISPLAY
        RECEIVE days_last_service FROM (INTEGER) KEYBOARD
    ENDWHILE

    SET priority TO ''
    IF condition = 'critical' AND days_last_service > 61 THEN
        SET priority TO 'High'
    ELSE IF condition = 'worn' AND days_last_service > 29 THEN
        SET priority TO 'Medium'
    ELSE IF condition = 'good' AND days_last_service <= 29 THEN
        SET priority TO 'Low'
    ENDIF
    RETURN priority
ENDFUNCTION

