# Configuration

All network and role settings live in two small files — no `menuconfig` needed.

## Detector config

**`sdkconfig.detector`**

```ini
# Board
CONFIG_BATEAR_BOARD_HELTEC_V3=y
CONFIG_ESPTOOLPY_FLASHSIZE_8MB=y

# Role
CONFIG_BATEAR_ROLE_DETECTOR=y
CONFIG_BATEAR_DEVICE_ID=1

# Network
CONFIG_BATEAR_NET_KEY="DEADBEEFCAFEBABE13374200F00DAA55"
CONFIG_BATEAR_LORA_FREQ=915000
CONFIG_BATEAR_LORA_SYNC_WORD=0x12
```

## Gateway config

**`sdkconfig.gateway`**

```ini
# Board
CONFIG_BATEAR_BOARD_HELTEC_V3=y
CONFIG_ESPTOOLPY_FLASHSIZE_8MB=y

# Role
CONFIG_BATEAR_ROLE_GATEWAY=y

# Network
CONFIG_BATEAR_NET_KEY="DEADBEEFCAFEBABE13374200F00DAA55"
CONFIG_BATEAR_LORA_FREQ=915000
CONFIG_BATEAR_LORA_SYNC_WORD=0x12
```

## Parameter Reference

| Parameter | Description |
|:---|:---|
| `CONFIG_BATEAR_BOARD_*` | Board selection — determines GPIO mapping and `set-target` chip. |
| `CONFIG_ESPTOOLPY_FLASHSIZE_*` | Flash size — must match your board's flash chip. |
| `CONFIG_BATEAR_NET_KEY` | 128-bit AES-GCM key (32 hex chars). **Must match** between all devices. |
| `CONFIG_BATEAR_LORA_FREQ` | Centre frequency in kHz: `915000` (US/TW), `868000` (EU), `923000` (AS). |
| `CONFIG_BATEAR_LORA_SYNC_WORD` | Network isolation byte. Different values = invisible to each other. |
| `CONFIG_BATEAR_DEVICE_ID` | Detector only. Unique ID (0–255) shown on gateway display. |

## Generate a new encryption key

```bash
python3 -c "import os; print(os.urandom(16).hex().upper())"
```

!!! warning
    The `CONFIG_BATEAR_NET_KEY` must be identical on **all** detectors and gateways in your network. If they don't match, packets will fail decryption silently.
