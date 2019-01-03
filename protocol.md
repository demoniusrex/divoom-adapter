# Divoom Aurabox Bluetooth serial protocol documentation #

## Command Message Format ##
| Message Prefix | Message length | Command | Command Data | Checksum | Message Suffix |
| -------------- | -------------- |-------- | ------------ | -------- | -------------- |
| 0x01           | 0x?? 0x00      | 0x??    | 0x??*        | 0x?? 0x??| 0x02           |

## Commands ##
| Command Name   | Length    | Command | Command Data 
| -------------- | ---------:| -------:|--------------------
| Show View      | 0x04 0x00 | 0x45    | [{View}](#views)
| Show Image     | 0x39 0x00 | 0x44    | 0x00 0x0a 0x0a 0x04 {ImageData} 
| Show Animation | 0x3b 0x00 | 0x49    | 0x00 0x0a 0x0a 0x04 {Position} {Time to display} {ImageData} 
| Play Music     | 0x05 0x00 | 0x41    | [{Music Type}](#musictypes) 0xff 
| Stop Music     | 0x05 0x00 | 0x41    | [{Music Type}](#musictypes) 0x00 
| Sleep          | 0x05 0x00 | 0x40    | [{Sleep Duration}](#sleep) [{Music Type}](#musictypes) 0xff 
| Stop Sleep     | 0x05 0x00 | 0x40    | 0x00 0x00 0x00 
| Alarm          | 0x06 0x00 | 0x43    | {Hour} {Minute} [{Music Type}](#musictypes) 0xff 
| Stop Alarm     | 0x06 0x00 | 0x43    | 0x00 0x00 0x00 0x00 
| Brightness     | 0x04 0x00 | 0x32    | [{Brightness}](#brightness) 
| Set Color      | 0x04 0x00 | 0x47    | [{Color}](#colors) 
| Set Time       | 0x0b 0x00 | 0x18    | {YY(last two digits)} {YY(first two digits)} {MM} {DD} <br/> {HH} {MM} {SS} {Fraction of second}
| Set Temp Unit  | 0x04 0x00 | 0x4c    | [{Temp Unit}](#tempunits) 

## Escaped Bytes ##
| Original Byte | Escaped Value |
| ------------- | ------------- |
| 0x01          | 0x03 0x04     |
| 0x02          | 0x03 0x05     |
| 0x03          | 0x03 0x06     |

## Message Data Types ##

### <a name="views">**Views**</a> ###

| View      | Value     |
|-----------|-----------|
|Clock      | 0x00      |
|Temp       | 0x01      |
|Color      | 0x02      |
|Spectrum   | 0x03      |
|Random     | 0x04      |
|Arrows     | 0x05      |
|Spinner    | 0x06      |
|Countdown  | 0x07      |
|Blank      | 0x08      |
|Image      | 0x09      |

### <a name="colors">**Colors**</a> ###

| Color     | Value     |
|-----------|-----------|
|Black      | 0x00      |
|Green      | 0x01      |
|Red        | 0x02      |
|Yellow     | 0x03      |
|Blue       | 0x04      |
|Purple     | 0x05      |
|Teal       | 0x06      |
|White      | 0x07      |

### <a name="musictypes">**Music Types**</a> ###

| Music Type| Value     |
|-----------|-----------|
|Bluetooth  | 0x00      |
|Forrest    | 0x01      |
|Rain       | 0x02      |
|Ocean Harp | 0x03      |

### <a name="tempunits">**Temperature Units**</a> ###

| Temp Unit | Value     |
|-----------|-----------|
| C         | 0x00      |
| F         | 0x01      |

### <a name="sleep">**Sleep Duration**</a> ###

| Duration  | Value     |
|-----------|-----------|
| 10 Minutes| 0x0a      |
| 20 Minutes| 0x14      |
| 30 Minutes| 0x1e      |
| 40 Minutes| 0x28      |
| 50 Minutes| 0x32      |
| 60 Minutes| 0x3c      |

### <a name="brightness">**Brightness**</a> ###

| Brightness| Value     |
|-----------|-----------|
| Full      | 0xd2      |
| Dimmer    | 0x3f      |
| Off       | 0x00      |
