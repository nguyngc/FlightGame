# Software 2 Project
## FLIGHT GAME V2.0
FLIGHTGAME v2.0 continues to be based on the basic story where players take on the role of a pilot caught up in the quest for a precious gem that is the key to opening a treasure cave. Players will choose different airports based on the game's suggestions in this journey. At each airport that players choose, there will be a mandatory mission to gather information about the gem and increase the player's assets. Finding the gem depends on the information and assets the player collects at the airports.

The expanded FLIGHTGAME v2.0 will allow players to experience more realistic role-playing and have a user interface for players to interact within the browser. The game will use actual data about the location of airports worldwide, a world map, and an online weather service.

In addition, the missions will be classified by difficulty level according to the real weather at the airport.

### Database
This game uses the airport and country table from the database course.

1. Create a new database 'flightgame':  
`CREATE DATABASE flightgame_v2`;
2. Switch to that database:  
`USE flightgame_v2`;
3. Import the same lp.sql as you did earlier in the database course:  
`source path/to/lp.sql`
4. Keep airport and country tables, remove others:  
`SET FOREIGN_KEY_CHECKS = 0;`  
`DROP TABLE game;`  
`DROP TABLE goal;`  
`DROP TABLE goal_reached;`  
`SET FOREIGN_KEY_CHECKS = 1;`
5. Create the following tables:  
```sql
CREATE TABLE IF NOT EXISTS `flightgame_v2`.`team` (
  `id` INT(11) NOT NULL AUTO_INCREMENT,
  `name` VARCHAR(45) NOT NULL,
  PRIMARY KEY (`id`))
ENGINE = InnoDB
AUTO_INCREMENT = 6
DEFAULT CHARACTER SET = latin1;
```

```sql
CREATE TABLE IF NOT EXISTS `flightgame_v2`.`player` (
  `id` INT(11) NOT NULL AUTO_INCREMENT,
  `username` VARCHAR(40) NOT NULL,
  `password` VARCHAR(40) NULL DEFAULT NULL,
  `continent` VARCHAR(40) NULL DEFAULT NULL,
  `country` VARCHAR(40) NULL DEFAULT NULL,
  `start_location` VARCHAR(40) NULL DEFAULT NULL,
  `plane` VARCHAR(40) NULL DEFAULT NULL,
  `current_location` VARCHAR(40) NULL DEFAULT NULL,
  `total_adventure` INT(11) NULL DEFAULT NULL,
  `total_score` INT(11) NULL DEFAULT NULL,
  `team_id` INT(11) NULL DEFAULT NULL,
  PRIMARY KEY (`id`),
  UNIQUE INDEX `id_UNIQUE` (`id` ASC),
  UNIQUE INDEX `user_name_UNIQUE` (`username` ASC),
  INDEX `fk_player_team_idx` (`team_id` ASC),
  CONSTRAINT `fk_player_team`
    FOREIGN KEY (`team_id`)
    REFERENCES `flightgame_v2`.`team` (`id`)
    ON UPDATE CASCADE)
ENGINE = InnoDB
AUTO_INCREMENT = 17
DEFAULT CHARACTER SET = latin1;
```

```sql
CREATE TABLE IF NOT EXISTS `flightgame_v2`.`player_progress` (
  `player_id` INT(11) NOT NULL,
  `location` VARCHAR(40) NOT NULL,
  `score` INT(11) NOT NULL,
  `status` INT(11) NOT NULL,
  INDEX `f_player` (`player_id` ASC),
  INDEX `f_player_airport_idx` (`location` ASC),
  CONSTRAINT `f_player`
    FOREIGN KEY (`player_id`)
    REFERENCES `flightgame_v2`.`player` (`id`)
    ON UPDATE CASCADE,
  CONSTRAINT `f_player_airport`
    FOREIGN KEY (`location`)
    REFERENCES `flightgame_v2`.`airport` (`ident`)
    ON UPDATE CASCADE)
ENGINE = InnoDB
DEFAULT CHARACTER SET = latin1;
```

![db.png](documents%2Fdb.png)

