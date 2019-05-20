# Types

## Timedate
The only supported format is specified, using python formatting,
as this `%Y-%m-%dT%H:%M:%S.%fZ`. You can find out more about this definition
[at python's documentation](https://docs.python.org/2/library/datetime.html#strftime-and-strptime-behavior). Briefly explained we used only the ISO timedate format using only
the UTC offset.<br>
Example: `2019-05-13T22:00:13.703856Z` (the writing time of this article).

## IDs
All of the IDs presented in the documentation are storable as unsigned 64-bit
longs and they are unique for in every place (two sensors from two different
sites will never have the same id).
