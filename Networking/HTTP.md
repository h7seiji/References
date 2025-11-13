# Hypertext Transfer Protocol (HTTP)

## HTTP/2

### Request and Response Multiplexing

The ability to break down an HTTP message into independent frames, interleave them, and then reassemble them on the other end is the single most important enhancement of HTTP/2, enabling us to:

- Interleave multiple requests in parallel without blocking on any one
- Interleave multiple responses in parallel without blocking on any one
- Use a single connection to deliver multiple requests and responses in parallel
- Remove unnecessary HTTP/1.x workarounds
- Deliver lower page load times by eliminating unnecessary latency and improving utilization of available network capacity

### Header Compression

HTTP/2 compresses request and response header metadata using the HPACK compression format:

- It allows the transmitted header fields to be encoded via a static Huffman code, which reduces their individual transfer size.
- It requires that both the client and server maintain and update an indexed list of previously seen header fields, which is then used as a reference to efficiently encode previously transmitted values.
