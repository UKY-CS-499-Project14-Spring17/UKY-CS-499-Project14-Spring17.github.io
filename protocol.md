---
title: HTPOW Protocol
---

# HTPOW Protocol

On this page, we give names and regular expressions to all known protocols for the HTPOW engraver. We also give brief descriptions and an example (some examples, by necessity, are rather long, so the examples are hidden by default. Hover over an example to view it.

## Known Commands

### Threshold (B&W) Engrave

The Threshold Engrave will only engrave black and white; it stops the laser, moves, then resumes engraving. The first byte is a counting byte, looping from 0x3d (61) to 0x78 (120), iterating on each command sent from the host computer. The second and third bytes define the X location to move to. The fourth and fifth bytes define the Y location to move to. The sixth byte is always 0x00 and is ignored. The seventh byte, as with all commands, is a 0xff and designates the end of the seven byte command from the host. The engraver responds when the host reaches 0x3d (61) and 0x5b (91) on the clock byte. This 60 instruction cycle should take around 1.6s at SuperCarver's default settings.

```ruby
# matches 0x3d through 0x78 for the first bit, then 4 bytes, then 0x00, then 0xff
/([4-6][\da-f]|3[d-f]|7[0-8])(:[\da-f][\da-f]){4}:00:ff/
```

```hide
# reverseEngineering/rawData/better/horizontal.parse
host	3d:01:26:02:14:00:ff
host	3e:01:27:02:14:00:ff
host	3f:01:28:02:14:00:ff
host	40:01:29:02:14:00:ff
...
host	70:01:59:02:14:00:ff
host	71:01:5a:02:14:00:ff
host	72:01:5b:02:14:00:ff
host	73:01:5c:02:14:00:ff
host	74:01:5d:02:14:00:ff
host	75:01:5e:02:14:00:ff
host	76:01:5f:02:14:00:ff
host	77:01:60:02:14:00:ff
host	78:01:61:02:14:00:ff
# restarts after 78, back to 3d
host	3d:01:62:02:14:00:ff
```

### Threshold (B&W) END Signal

The END signal for threshold engraving will repeat the last clock byte, along with 4 0x09 bytes, either a 0x00 or 0x09, and the standard 0xff seventh byte. This will terminate signal from the host computer. After enough time passes for another status interrupt from the engraver, it will end and send its final signal.

In tests so far, ending on a horizontal travel terminates in a 0x00, while ending on a vertical travel terminates in a 0x09. The significance of this is not known or guaranteed.

```ruby
/([4-6][\da-f]|3[d-f]|7[0-8])(:09){4}:0[09]:ff/
```

```hide
# reverseEngineering/rawData/better/vertical.parse
host	4c:09:09:09:09:09:ff
# reverseEngineering/rawData/better/vertical_again.parse
host	4c:09:09:09:09:09:ff
# reverseEngineering/rawData/better/vertical_break.parse
host	49:09:09:09:09:09:ff

# reverseEngineering/rawData/better/horizontal.parse
host	77:09:09:09:09:00:ff
# reverseEngineering/rawData/better/horizontal_break.parse
host	67:09:09:09:09:00:ff
```

### Greyscale Engrave

The Greyscale Engrave will engrave in any range from black (full burn) to white (no burn); it stops the laser, moves, then resumes engraving. The first byte is a counting byte, looping from 0x79 (121) to 0xb4 (180), iterating on each command sent from the host computer. The second and third bytes define the X location to move to. The fourth and fifth bytes define the Y location to move to. The sixth byte defines the laser wait time, from 0xff (full time) to 0x00 (no time). The seventh byte, as with all commands, is a 0xff and designates the end of the seven byte command from the host. The engraver responds when the host reaches 0x79 (121) and 0xb4 (180) on the clock byte. This 60 instruction cycle should take around 1.6s at SuperCarver's default settings.

```ruby
# matches 0x79 through 0xb4 for the first bit, then 5 bytes, then 0xff
/([89a][\da-f]|7[9a-f]|b[0-4])(:[\da-f][\da-f]){5}:ff/
```

```hide
# reverseEngineering/rawData/better/grayscale.parse
host	79:02:13:00:44:ff:ff
host	7a:02:14:00:44:ff:ff
host	7b:02:15:00:44:ff:ff
...
host	b1:02:13:00:4c:ff:ff
host	b2:02:3c:00:4c:ff:ff
host	b3:02:3c:00:4d:ff:ff
host	b4:02:13:00:4d:ff:ff
# restarts after b4, back to 79
host	79:02:13:00:4e:ff:ff
host	7a:02:3c:00:4e:ff:ff
host	7b:02:3c:00:4f:ff:ff
```

## Encountered (and not yet fully understood) Protocol

### Greyscale END Signal

The END signal for threshold engraving will repeat the last clock byte, along with a 0x09 bytes, four 0x00 bytes, and the standard 0xff seventh byte. This will terminate signal from the host computer. After enough time passes for another status interrupt from the engraver, it will end and send its final signal.

NOTE: we need more data points to verify this behavior.

```ruby
/([89a][\da-f]|7[9a-f]|b[0-4]):09(:00){4}:ff/
```

```hide
# reverseEngineering/rawData/better/grayscale.parse
host	82:09:00:00:00:00:ff
```

