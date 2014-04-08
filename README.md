Crypto001_Week1
===============

This is the solution to the Week 1 programming assignment for the “Cryptography I” course on Coursera.

Basically the solution is easy especially provided the hint as to XOR the encrypted MSGS together. Just do it once a time using a selected MSGS and the target MSG, i.e.:

```
  MSGS[0] XOR TARGET
  MSGS[1] XOR TARGET
  ...
  MSGS[9] XOR TARGET
```

What do we get by doing so? Consider the second half of the hint, if there is a space in the MSGS, by XORing with the TARGET message, it will flip the character in the same position from lower case to upper or vice versa. So if we XOR the MSGS and TARGET together, and get an upper case char "A" in certain position of the TARGET message, we know most likely in the same position of MSGS it is a space. And the real character in this position in the TARGET message is a lower case "a". So that leaves us only one problem: how do we output the results of MSGS[...] XOR TARGET so that we can see the result clearly.

I used python because the assignment already has a python source code paragraph attached to it and we can re-use some part of it, e.g. the XOR function. After getting the result of MSGS[...] XOR TARGET I compare if each byte of the results is within "a"~"z" or "A"~"Z", and if so I output it directly. If not, I simply output a "*". Thus I get:

```
START--- * * E C * * C * * * T * * S * * * E N * * X E * H T * * * * * * G Q * A * * * * A * O * * * * * * * * N * * E * A * S * L * * E F * * * O * O * * E T * * * B * * C T ---END
START--- * * * E * E * * * * D M * * * * * * L * S * N * * * N T * * * N * O * * * * * E * * E * * * * E * I C * * * * R A U * * R * * * * * * * N * O * * * * * * * T * N N E ---END
START--- * * * * * * * * E * H * * * S * * * U * S q E * * * * Q U * * N * O * * * * R * * * P * * * * * * D E * * V * * N U * * I * * E A K * * T M * * E F * * * * * * * * * ---END
START--- * * * * * * * * * * T * * * S * * * D * * * D w * * N A U * * * * * * N * * * * * * O * I * * * * * I * * * E * O * * * * * * E G * * * * * * R * I * * * * T * * * E ---END
START--- * * * * * * * U * T W * * * S * * E B * * * A w * * * * * * I * * R A K * * * E * * O * I * H * * U * * * * E * P * * * A * * * E * E * N M * * * A * * * * * * * * * ---END
START--- * * * R * E * * * T T * * S * * * * S I * * * * * * * T * * * * * H * * * T * * * * * * * * * * R * I * * V * * E * S * E * * * T * E * A * * R * R * * A * O * * C * ---END
START--- * * * R * E * * * T T * * S * * * * S I * * * * * * * O * * * * * Y * * * * * E * * A * I * * * * * S N * * * R g * * * R * * * N * E * O M * * * * * * * * E O * * * ---END
START--- * * E C * * C * * * * * * * S * * * N * S M H * * * N T * * I * * I * * * * R * * * A * * * H * * * A N * * * * G U * * T T * * * * * * T M * * * * * * * * U * * * E ---END
START--- * H M P * * * * * * * * * * Z A G * N * * C P * * * * * * * * * * E A S * * * * * M * C * * * * * E T * * * I R N * * * L * H * * * * * C * * * * E T * * * * * * * * ---END
START--- t * * E S * * * * * S * E * * * * * D * * Y T * * * * R * S A * W * W * S * * * * * N * * P * * * * T * E * * R T * * E A * * E O * E Y W * * * * N * H * N R O * * * ---END
```

Paste the results in a text editor without wrapping and we will see it's easier to align all the positions of the results in this way.
