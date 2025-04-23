# ROMs I have used

- mon3-15-32k.bin
- mon3-16-32k.bin

# Programming the EEPROM using minipro

## Hardware check
```
minipro --hardware_check
```

## Read EEPROM
```
minipro -p AT28C256 -r c.bin
```

### List contents EEPROM
```
hexdump -C c.bin
```

## Write EEPROM
```
minipro -p AT28C256 -w mon3-16-32k.bin
```

### Write protected error
Verification failed at address 0x0000: File=0xC3, Device=0xFF
This chip may be write-protected. Use -u and try again.

### Write EEPROM remove write protect
To remove the write protect:
-u,  --unprotect
Disable protection before programming.

```
minipro -p AT28C256 -u -w mon3-16-32k.bin
```

## Commands
https://www.mankier.com/1/minipro
