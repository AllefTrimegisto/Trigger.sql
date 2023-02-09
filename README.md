# Trigger.sql
CREATE TABLE command_info (
  command_id INT PRIMARY KEY AUTO_INCREMENT,
  command_name VARCHAR(50) NOT NULL,
  command_type VARCHAR(20) NOT NULL
);

CREATE TRIGGER command_trigger BEFORE INSERT ON command_info 
FOR EACH ROW 
BEGIN
  IF NEW.command_name NOT IN ('INSERT', 'SELECT', 'UPDATE', 'DELETE') THEN
    SIGNAL SQLSTATE '45000' 
    SET MESSAGE_TEXT = 'Invalid command name';
  END IF;
END;
