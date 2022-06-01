# Debugging and Data Control

## General

---

`System.assertEquals()` will check if two passed parameters are equal in data type and value

- Fails a test method if evaluates to false
  - Takes three parameters:
    1. Expected result
    2. Actual result
    3. Error message in the event of failure

`System.assert()` will check if the boolean value of the parameter passed evaluates to true; will throw a fatal error if it evaluates to false

`System.debug()` will return whatever is passed to it in the logged output of an Apex class after it is run

> When debugging, can specify the level of logging desired:
>
> - `NONE`  
> - `ERROR`
> - `WARN`
> - `INFO`
> - `DEBUG`
> - `FINE`
> - `FINER`
> - `FINEST`
>
>> **Note:** levels are cumulative and run from lowest-to-highest in terms of how granular the information they give you is
>>
>> To use, set the `LoggingLevel` parameter in a system debug statement (first parameter) and use dot notation to append desired log level
