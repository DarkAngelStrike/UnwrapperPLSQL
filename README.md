### UnwrapperPLSQL

----

This repository contains a python script capable of unwrapping *Oracle 10g/11g PL/SQL* procedures.
A general introduction to *PL/SQL Source Text Wrapping* can be found within the
[official oracle documentation](https://docs.oracle.com/cd/E24693_01/appdev.11203/e17126/wrap.htm).
This documentation also contains some samples for wrapped procedures and the following procedure will
be used for demonstration purposes:

```
CREATE OR REPLACE FUNCTION fibonacci wrapped 
a000000
b2
abcd
abcd
abcd
abcd
abcd
abcd
abcd
abcd
abcd
abcd
abcd
abcd
abcd
abcd
abcd
8
14a fb
e1Yq3QQJoEoNKIeJlbgLoLdSgogwgxDcf8vWfHSKbuowFOXFKoj9MqYGqWyRxeeCUVqNVIO1
ICqJa3yPr6e7z8GZpMH3J0Cx0uQ0B1JuysymdNDlzfTvb7QWsrLU4jGs3h8Mm49/L9nyO4Xh
Ae06nawFpOJIAYpBf9wBVC+ZrjU/nuEtokBqCce6HWIoF6rYgz0V0W/47x5KpOnQ2i7X3kFe
FR8K7jT7X58k8xK9uYlZv5LhV71a7A==
```


### Usage

----

When launching the script without any arguments, it expects the wrapped procedure to be passed via stdin
and outputs the unwrapped procedure to stdout:

```console
[user@host ~]$ cat wrapped.pld | python3 unwrap.py 
FUNCTION fibonacci (
  N PLS_INTEGER
) RETURN PLS_INTEGER
AUTHID DEFINER
IS
  FIB_1 PLS_INTEGER := 0;
  FIB_2 PLS_INTEGER := 1;
BEGIN
  IF N = 1 THEN                              
    RETURN FIB_1;
  ELSIF N = 2 THEN
    RETURN FIB_2;                           
  ELSE
    RETURN FIBONACCI(N-2) + FIBONACCI(N-1);  
  END IF;
END;
```

You can also specify a file that contains a wrapped procedure as argument:

```console
[user@host ~]$ python3 unwrap.py wrapped.pld 
FUNCTION fibonacci (
  N PLS_INTEGER
) RETURN PLS_INTEGER
AUTHID DEFINER
IS
  FIB_1 PLS_INTEGER := 0;
  FIB_2 PLS_INTEGER := 1;
BEGIN
  IF N = 1 THEN                              
    RETURN FIB_1;
  ELSIF N = 2 THEN
    RETURN FIB_2;                           
  ELSE
    RETURN FIBONACCI(N-2) + FIBONACCI(N-1);  
  END IF;
END;
```

### Resources

----

* [Official Oracle Documentation](https://docs.oracle.com/cd/E24693_01/appdev.11203/e17126/wrap.htm).
* [Unwrapping Oracle PLSQL - Blog Post](http://blog.teusink.net/2010/04/unwrapping-oracle-plsql-with-unwrappy.html)
