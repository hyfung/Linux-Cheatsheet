# Regex Cheatsheet

## Look Up Table

### Characters
|Pattern|Explanation            |
|-------|-----------------------|
|\d     |Digit                  |
|\D     |Not digit              |
|\w     |Alphanumeric, _        |
|\W     |Not alphanumeric, _    |
|\s     |Space, Tab, CR, LF     |
|\S     |Not Space, Tab, CR, LF |
|.      |Any char except break  |

### Quantifier Suffixes
|Pattern|Explanation                |
|-------|---------------------------|
|*      |0 or more                  |
|+      |1 or more                  |
|?      |Once only, shortest match  |
|{N}    |N times                    |
|{M,N}  |M to N times               |
|{N,}   |N or more                  |

### Logical Operation
|Pattern|Explanation    |
|-------|---------------|
|\|     |OR             |
|(...)  |Group          |
|\N     |Group N content|
|(?:...)|               |

### Char Classes
|Pattern|Explanation    |
|-------|---------------|
|[]     |One char in set|
|[ - ]  |Range          |
|[^...] |Not in         |
|[\xNN] |ASCII Hex      |

### Anchor Boundary
|Pattern|Explanation        |
|-------|-------------------|
|^      |Line start         |
|$      |Line end           |
|\A     |Start of string    |
|\Z     |End of string      |
|\b     |Word boundary      |
|\B     |Not word boundary  |

# List Of Useful Regex Pattern

#### SSH Login Log for /var/log/auth.log
`(\w{3} \d{2} \d{2}:\d{2}:\d{2}) \w+ sshd\[\d+\]: Accepted publickey for (\w+) from (\d+.\d+.\d+.\d+) port (\d+) ssh2: RSA SHA256:\/([A-Za-z0-9+]+)`
