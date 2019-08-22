# rsocket-rust
learn rust && implement rsocket. 😭

## Example

> Here's a prototype of RSocket API. Yes, It works! 

```rust
extern crate bytes;
extern crate futures;
extern crate rsocket;
extern crate tokio;

use bytes::Bytes;
use futures::Future;
use rsocket::prelude::*;

#[test]
fn test_socket_request() {
  // You can run a mock server by rsocket-cli in golang. (see: https://github.com/rsocket/rsocket-go)
  // rsocket-cli --request -i 'Hello World!' -m 'text/plain'  -s --debug tcp://127.0.0.1:7878

  // create a socket.
  let socket = DuplexSocket::connect("127.0.0.1:7878");
  // request and block future for result.
  let sending = Payload::builder()
    .set_data(Bytes::from("Hello Rust!"))
    .set_metadata(Bytes::from("text/plain"))
    .build();
  let result = socket.request_response(sending).wait().unwrap();
  println!("********** YES: {:?}", result);
}

```

## TODO
 - Codec
   - [x] Setup
   - [x] Keepalive
   - [x] Payload
   - [x] RequestResponse
   - [x] RequestStream
   - [x] RequestChannel
   - [x] RequestFireAndForget
   - [x] MetadataPush
   - [x] RequestN
   - [ ] Resume
   - [x] ResumeOK
   - [x] Cancel
   - [x] Error
   - [x] Lease
 - Transport
   - [ ] TCP
   - [ ] Websocket
 - Rx
   - [ ] ...
 - High Level APIs
   - [ ] Client
   - [ ] Server
