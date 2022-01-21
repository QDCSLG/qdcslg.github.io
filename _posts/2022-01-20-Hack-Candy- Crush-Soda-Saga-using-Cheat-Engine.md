---
layout: post
title: Hack Candy Crush Soda Saga using cheat engine
description: How to hack Candy Crush soda sage using cheat engine
tags: 
- Cheat engine
---

Candy Crush Soda Saga is a very popular relaxing game. It is a free game for windows 10 user.

It is getting more and more chllenging if you win many games. Some time it is almost imposibble to pass the game without losing games. That is frustrating. 

***I like to play games, I don't like to be played by the game***

So I started my `cheatengine`

- Launch `CheatEngine`
- find the process called `stritz.exe`
  - This is the acual process runs the Candy Crush Soda Saga
- Using the current number of moves allowed, for example 32
- first scan
- make one move, now the number of move is 31
- next scan 31
- after few time, you will be able to see 3~4 address show up
  - start with 1*
  - start with 2*
  - start with 2*
  - start with 2*
- Freeze the value of these addresses, the game will not reduce the number of moves when you make a move.

This way, there is unlimited number of moves for the game. You can crush more candies without worring about our of move.

Update:

The steps described above definitly works. But the address will change slightly for each new game. These steps need to be repeated for each new game. It is not convienient at all.

For each of the address discoved by the previous step, right click the address then select `Find out who writes to this address`, By doing so, cheat engine will attach a debugger to the application.
Then go back to the game and make 1 move. There should be an address of the instruction displayed in the debugger.
Here is a list of example addresses:
- 00B4BD5A
- 00DCB670
- 00E8AF96
- 00DC9F3B

Among all addresses, `00B4BD5A` seems the one which actually contains the instruction to reduce the number of moves after each move.

The original code at that address is 
```
mov [edi+38],esi
```
It seems like the code is trying to move the value in register to another value. 

- mov
 - The mov instruction copies the data item referred to by its second operand (i.e. register contents, memory contents, or a constant value) into the location referred to by its first operand (i.e. a register or memory). While register-to-register moves are possible, direct memory-to-memory moves are not. In cases where memory transfers are desired, the source memory contents must first be loaded into a register, then can be stored to the destination memory address.



Replace with `NOP` instruction, then any move will not reduce the number of move. and it is consistent game after game.

