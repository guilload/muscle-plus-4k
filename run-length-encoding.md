# Run-length encoding (RLE)

#### Implementation

```python
def encode(string):

    def append(char, count):
        """
        Helper
        """
        if count > 1:
            builder.append("{}".format(count))  # that nasty closure ;)

        builder.append(char)


    if len(string) < 2:
        return string

    builder = []

    count = 1
    current = string[0]

    for char in string[1:]:
        if char == current:
            count += 1
        else:
            append(current, count)
            count = 1
            current = char

    append(current, count)
    return "".join(builder)


def decode(string):
    builder = []
    count = 0

    for char in string:
        if char.isdigit():
            count = count * 10 + int(char)
        else:
            n = max(1, count)
            builder.append(char * n)
            count = 0

    return "".join(builder)
```

#### Runtime complexity

*O(n)*

#### Resources

https://en.wikipedia.org/wiki/Run-length_encoding
