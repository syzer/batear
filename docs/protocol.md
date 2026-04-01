# LoRa Packet Protocol

AES-128-GCM encrypted, 28 bytes on the wire:

```
[4B nonce] [8B ciphertext] [16B GCM auth tag]
```

## Plaintext format (8 bytes)

```
[2B seq] [1B device_id] [1B event_type] [1B f0_bin] [1B rms_db] [2B reserved]
```

## Security features

- **Sequence counter** prevents replay attacks
- **GCM auth tag** ensures data integrity and authenticity
- **Sync word** provides channel isolation at the RF level
