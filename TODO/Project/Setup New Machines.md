#setup

### Assign FIX ip.

- Have a lists of used ip´s (maybe separate deployments into another subnet 192.172.x.XX)
- Allow certificate auth in the new machine. (Be already set up on clone)

```
PubkeyAuthentication yes
AuthorizedKeysFile .ssh/authorized_keys
PasswordAuthentication yes  # (or no, only after keys work)
```



	- Restart if it was configured
  
- 