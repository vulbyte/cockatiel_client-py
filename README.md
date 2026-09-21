# cockatiel_client-py

Python client SDK for connecting a module to the Cockatiel engine.

This repo is **standalone**: `lib_cockatiel.py` plus the `cockatiel_protobuf.proto`
it compiles at runtime. It does not reach into any other repository. The `.proto`
file is the same single source of truth as
[`cockatiel_proto`](https://github.com/vulbyte/cockatiel_proto) — keep them in sync
when the protocol changes.

## Using it in a module

Copy this folder (or submodule/pin it) into your module, then:

```python
from lib_cockatiel import CockatielClientBuilder, pb

client = (
    CockatielClientBuilder("tts-service")
    .endpoint("127.0.0.1", 9734)
    .pin(123456)
    .position("postprocess")
    .connect()
)
```

The client auto-compiles `cockatiel_protobuf.proto` into a cached `_pb2` module
next to it (`COCKATIEL_PROTO_PATH` overrides the proto location;
`COCKATIEL_PB2_CACHE` overrides the cache dir).

### Runtime requirements

- `websockets`
- `grpcio-tools` (to compile the `.proto` on first use)

## Protocol sync

`cockatiel_protobuf.proto` here is the compiled source of truth. When
`cockatiel_proto` changes, update this copy and bump whatever pins this repo by
commit.

## License

GPL-2.0