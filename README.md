Crypto001_Week1
===============

This is the solution to the Week 1 programming assignment for the “Cryptography I” course on Coursera.

Basically the solution is easy especially provided the hint as to XOR the encrypted `MSGS` together. Just pick up one `MSGS` per time and XOR with the `TARGET` message (which happens to be `MSGS[10]` in the code), i.e.:

```
  MSGS[0] XOR TARGET
  MSGS[1] XOR TARGET
  ...
  MSGS[9] XOR TARGET
```

What do we get by doing so? Consider the second half of the hint, if there is a space character in either side of the XOR operator and an alphabet character in the other one at the same position, after XOR operation the alphabet character will be flipped from lower to upper case or vice versa.

Assuming we get an upper case character "A" in certain position from the result of XOR operation, we know **probably** at this position either `MSG[i]` or `TARGET` contains a space character and the other one contains a lower case character "a" (in plain text). It is not absolute but still has a relatively high possibility.

So the only trick left in this assignment is how do we output the results of `MSGS[i] XOR TARGET` so that we can see the result clearly. Here is one possible solution:

I used python because the assignment already has a python source code paragraph attached to it and we can re-use some part of it, e.g. the `strxor()` function. After getting the result of `MSGS[i] XOR TARGET` I compare each byte of the results and see if it falls within "a"~"z" or "A"~"Z", if so I output it directly; if not, I simply output a "\*". Thus I get:

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

* Now look at position 0 of all the result strings. We got 9 "\*" characters and a lower case "t". Then **probably** the first character in `MSGS[9]` is a space and in `TARGET` is an upper case "T" (in plain text).
* Similarly position 1 could be a lower case "h".
* Position 2 would be a little bit confusion as we got 2 upper case "E" and an upper case "M". I would assume the correct answer could be lower case "e" since "E" appeared twice.
* Now position 3. It has 7 different characters, I would assume this time in turn the `TARGET` contains a space character at this position.
* ...

In this way we should be able to deduce the cracked target message `CRACK` to be something like:

```The secuet message is  Whtn usinw a stream cipher  never use the key more than once```

There is still some strange wording, it shouldn't be hard to tune it to:

```The secret message is  When using a stream cipher  never use the key more than once```

Again, I noticed there are extra space characters around "When using a stream cipher". I would assume the first extra space is actually a colon ":" and the second one a comma "," but I could not be sure. But it's still easy as we now have both the target message `TARGET` and its plain text `CRACK`, we can caculate the key and then decrypt the other `MSGS` to verify if the key's correct. Now if we use `CRACK` with 2 extra space characters directly we will get the crasked `MSGS` as below:

```
START---We can factor the numxer 15 with quantum computer. We can also factor the number 1---END
START---Euler would probably njoy that now his theorem bicomes a corner stone of crypto - ---END
START---The nice thing about Qeeyloq is now we cryptograpders can drive a lot of fancy cars---END
START---The ciphertext producd by a weak encryption algo~ithm looks as good as ciphertext ---END
START---You don't want to buy:a set of car keys from a guu who specializes in stealing cars---END
START---There are two types o| cryptography - that which {ill keep secrets safe from your l---END
START---There are two types o| cyptography: one that allo{s the Government to use brute for---END
START---We can see the point mhere the chip is unhappy if,a wrong bit is sent and consumes ---END
START---A (private-key)  encrcption scheme states 3 algorethms, namely a procedure for gene---END
START--- The Concise OxfordDiytionary (2006) deﬁnes cry|to as the art of  writing o r sol---END
```

Clearly all the plain texts has something strange words. Now again I just completed `CRACK` with the colon and comma I assumed:

```The secret message is: When using a stream cipher, never use the key more than once```

Again I verified the plain texts of `MSGS`, this time we got:

```
START---We can factor the number 15 with quantum computers. We can also factor the number 1---END
START---Euler would probably enjoy that now his theorem becomes a corner stone of crypto - ---END
START---The nice thing about Keeyloq is now we cryptographers can drive a lot of fancy cars---END
START---The ciphertext produced by a weak encryption algorithm looks as good as ciphertext ---END
START---You don't want to buy a set of car keys from a guy who specializes in stealing cars---END
START---There are two types of cryptography - that which will keep secrets safe from your l---END
START---There are two types of cyptography: one that allows the Government to use brute for---END
START---We can see the point where the chip is unhappy if a wrong bit is sent and consumes ---END
START---A (private-key)  encryption scheme states 3 algorithms, namely a procedure for gene---END
START--- The Concise OxfordDictionary (2006) deﬁnes crypto as the art of  writing o r sol---END
```

Now much better. So the problem is solved.
