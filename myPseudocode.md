## PRETASK 1
FUNCTION new_customer()
    BEGIN FUNCTION
    SET name TO ''
    SET surname TO ''
    SET dob TO ''

    WHILE name = '' DO
        SEND 'Enter Name' TO DISPLAY
        RECEIVE name FROM (STRING) KEYBOARD
    ENDWHILE

    WHILE surname = '' DO
        SEND 'Enter Surname' TO DISPLAY
        RECEIVE surname FROM (STRING) KEYBOARD
    ENDWHILE

    WHILE dob = '' OR dob >= today() DO
        SEND 'Enter date of birth' TO DISPLAY
        RECEIVE dob FROM (DATETIME) KEYBOARD
    ENDWHILE

    RETURN 'Customer Added'
ENDFUNCTION



## TASK 1: Username Checker
FUNCTION get_name()
    BEGIN FUNCTION
    SET name TO ''
    SET running TO FALSE
    WHILE running = FALSE DO
        SEND 'Enter username.' TO DISPLAY
        RECEIVE name FROM (STRING) KEYBOARD
        SET len_name TO LENGTH(name)
        IF len_name >= 4 AND len_name <= 12 THEN
            SEND 'Username accepted' TO DISPLAY
            SET running TO TRUE
        ELSE
            SEND 'Invalid username.'
        ENDIF
    ENDWHILE
ENDFUNCTION



## TASK 2: Stock Level Alert
FUNCTION stock_alert()
    BEGIN FUNCTION
    SET stock TO 0
    SEND "Enter stock level." TO DISPLAY
    RECEIVE stock FROM (INTEGER) KEYBOARD
    IF stock <= 0 THEN
        SEND "Out of stock" TO DISPLAY
        SET stock TO 0
    ELSE IF stock >= 1 AND stock <= 5 THEN
        SEND "Low stock" TO DISPLAY
    ELSE IF stock >= 6 AND stock <= 20 THEN
        SEND "Stock OK" TO DISPLAY
    ELSE IF stock > 20 THEN
        SEND "High stock" TO DISPLAY
    ELSE
        SEND "Error" TO DISPLAY
    ENDIF
ENDFUNCTION



## TASK 3: Maintenance Due Checker
FUNCTION maintenanceChecker()
    BEGIN FUNCTION
    SET lastService TO 0
    SET serviceFrequency TO ""
    SEND "Enter days since last service." TO DISPLAY
    RECEIVE lastService FROM (INTEGER) KEYBOARD
    SEND "Enter service frequency (Weekly / Monthly)." TO DISPLAY
    RECEIVE serviceFrequency FROM (STRING) KEYBOARD

    IF serviceFrequency = "Weekly" THEN
        IF lastService < 5 THEN
            SEND "Not due yet" TO DISPLAY
        ELSE IF lastService >= 5 AND lastService <= 6 THEN
            SEND "Due soon" TO DISPLAY
        ELSE IF lastService = 7 THEN
            SEND "Due now" TO DISPLAY
        ELSE
            SEND "Error" TO DISPLAY
        ENDIF

    ELSE IF serviceFrequency = "Monthly" THEN
        IF lastService < 28 THEN
            SEND "Not due yet" TO DISPLAY
        ELSE IF lastService >= 28 AND lastService <= 29 THEN
            SEND "Due soon" TO DISPLAY
        ELSE IF lastService = 30 THEN
            SEND "Due now" TO DISPLAY
        ELSE
            SEND "Error" TO DISPLAY
        ENDIF

    ELSE
        SEND "Error" TO DISPLAY
    ENDIF
ENDFUNCTION



## TASK 4: Priority Classifier
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
