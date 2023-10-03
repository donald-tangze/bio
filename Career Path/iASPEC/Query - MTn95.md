Create an outward MTn95 Query message. There are two scenario as below:

## 1.Based on an incoming Payment message 

Incoming payment   ->   MT Query MTn95

instructing agent     ->     To

instructed agent     ->      From     (we)

Incoming payment   ->   Original Message

create datatime of iw     ->    create datatime in field (79) 

## 2.Based on an outgoing Payment message 

outgoing transaction   ->   MT Query MTn95

instructing agent          ->     From  (we)

instructed agent           ->     To

outward transaction     ->     Original Message (79)

create datatime of ow     ->    create datatime in field (79) 