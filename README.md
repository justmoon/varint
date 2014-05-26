# varint

encode whole numbers to an array of [protobuf-style varint bytes](https://developers.google.com/protocol-buffers/docs/encoding#varints) and also decode them.

```javascript
var varint = require('varint')

var bytes = varint.encode(300) // === [0xAC, 0x02]
varint.decode(bytes) // 300
varint.decode.bytesRead // 2 (the last decode() call required 2 bytes)
```

## api

### varint = require('varint')

### varint.encode(num[, output=[], offset=0]) -> array

encodes `num` into either the array given by `offset` or a new array at `offset`
and returns that array filled with integers.

### varint.decode(data[, offset=0]) -> number

decodes `data`, which can be either a buffer or array of integers, from position `offset` or default 0 and returns the decoded original integer.

### varint.decode.bytesRead

if you also require the length (number of bytes) that were required to decode the integer you can access it via `varint.decode.bytesRead`. this is an integer property that will tell you the number of bytes that the last .decode() call had to use to decode.

### varint.encode.bytesWritten

similar to `bytesRead` when encoding a number it can be useful to know how many bytes where written (especially if you pass an output array). you can access this via `varint.encode.bytesWritten` which holds the number of bytes written in the last encode.


### varint.encodingLength(num)

returns the number of bytes this number will be encoded as, up to a maximum of 8.

## usage notes

If varint is passed a buffer that does not contain a valid end
byte, then `decode` will return undefined, and `decode.bytesRead`
will be set to 0. If you are reading from a streaming source,
it's okay to pass an incomplete buffer into `decode`, detect this
case, and then concatenate the next buffer.

# License

MIT
