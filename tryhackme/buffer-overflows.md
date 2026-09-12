#Task 8

<img width="922" height="710" alt="Screenshot 2026-09-09 234627" src="https://github.com/user-attachments/assets/e33d67a3-436c-48c5-bdba-d50f9c969d58" />

You can see there are source c code and compiled binary in the overflow-3 directory


<img width="933" height="283" alt="Screenshot 2026-09-09 234733" src="https://github.com/user-attachments/assets/5a6509b3-43ba-4c5f-b9de-36d91c96c75d" />







<img width="926" height="548" alt="Screenshot 2026-09-09 234812" src="https://github.com/user-attachments/assets/fe1191e0-1bf9-40c2-9310-2790dcc5bfab" />

Looking at the c code with r2 (radare2); Similar to Immunity Debugger but more like CLI interactive than GUI interactive Immunity Debugger.




<img width="921" height="421" alt="Screenshot 2026-09-09 234837" src="https://github.com/user-attachments/assets/b05fb802-a727-4043-968b-6f8f286c2525" />


<img width="934" height="425" alt="Screenshot 2026-09-09 234903" src="https://github.com/user-attachments/assets/781a4074-3a50-4a55-a952-a6835f3ffa93" />




Tested the memory with shellcode and extra charaters
<img width="936" height="211" alt="Screenshot 2026-09-09 235015" src="https://github.com/user-attachments/assets/de3aec2c-a6d0-4b6e-a76b-ca1abd9a5e92" />


Tested memory in r2 
<img width="930" height="435" alt="Screenshot 2026-09-09 235040" src="https://github.com/user-attachments/assets/437f8b2a-0a73-4f1e-9e22-fcbd63bcb166" />

<img width="937" height="375" alt="Screenshot 2026-09-09 235103" src="https://github.com/user-attachments/assets/e36580ca-c1a0-481c-8f4d-67347aedcc90" />

<img width="929" height="462" alt="Screenshot 2026-09-09 235120" src="https://github.com/user-attachments/assets/5dd6e65c-2ab0-432d-b2ad-546058c655f3" />


Testing random string in r2
<img width="928" height="627" alt="Screenshot 2026-09-10 001400" src="https://github.com/user-attachments/assets/65a4bb6b-7e95-4ba9-b3e6-e0d4d03ede8d" />


<img width="936" height="374" alt="Screenshot 2026-09-10 001733" src="https://github.com/user-attachments/assets/d758366c-3073-40bb-8b73-bdbf9c6987f6" />



<img width="932" height="500" alt="Screenshot 2026-09-10 003008" src="https://github.com/user-attachments/assets/1621c973-178f-48b1-a6de-a6f5e300a1b2" />



Checking registers..especially the rip value
<img width="930" height="323" alt="Screenshot 2026-09-10 003026" src="https://github.com/user-attachments/assets/abc6892d-9765-4ab7-a247-6ce96e5d62ce" />


Checking memory at rsp

<img width="935" height="330" alt="Screenshot 2026-09-10 004506" src="https://github.com/user-attachments/assets/17803a23-5fec-4850-91cd-d7569a3bc8bc" />

<img width="927" height="67" alt="Screenshot 2026-09-10 005408" src="https://github.com/user-attachments/assets/1b6a5c81-e4fe-401a-a746-e2280464464c" />

Shellcode to open basic shell
<img width="1006" height="28" alt="Screenshot 2026-09-10 233100" src="https://github.com/user-attachments/assets/e610d681-a435-44a3-a40b-36d7e4d05fda" />

Disassembled shellcode
<img width="728" height="334" alt="Screenshot 2026-09-10 233646" src="https://github.com/user-attachments/assets/a8ce4601-97dc-49df-860a-91b74f278c09" />

Running Command in r2
<img width="931" height="381" alt="Screenshot 2026-09-11 002002" src="https://github.com/user-attachments/assets/5351ee38-4bb4-4bd5-b62b-9b643d0798e4" />

<img width="929" height="453" alt="Screenshot 2026-09-11 002312" src="https://github.com/user-attachments/assets/7bd15a22-f531-4ce3-b370-9e577429a121" />

You can see the shellcode was executed in the memory.
<img width="937" height="304" alt="Screenshot 2026-09-11 003040" src="https://github.com/user-attachments/assets/d2efa403-2c7a-4bde-a255-f6e3c7deb80a" />

The Bs popped from stack into rip. You can see 0x42424242 in rip 
<img width="943" height="373" alt="Screenshot 2026-09-11 003524" src="https://github.com/user-attachments/assets/f5c5c4bb-1e07-49d3-a3c3-16d1b9edd95c" />



We select address in the middle of the NOPS.
0x7fffffffe278
<img width="933" height="466" alt="Screenshot 2026-09-11 012241" src="https://github.com/user-attachments/assets/b5bed61b-1017-42a6-98f0-8b45b688318f" />

<img width="944" height="335" alt="Screenshot 2026-09-11 012310" src="https://github.com/user-attachments/assets/e293208a-7b5d-48b2-b6b1-9cdef88b350a" />

<img width="941" height="320" alt="Screenshot 2026-09-11 012342" src="https://github.com/user-attachments/assets/2cc8c608-fdd9-46fb-a4d1-310227ddc9d7" />

Trying different shellcode
<img width="936" height="454" alt="Screenshot 2026-09-11 013540" src="https://github.com/user-attachments/assets/4ed62099-b10a-40c2-9fb0-9e04c1003389" />

Signal 11 is your indicator that:

You hit an invalid address

You overwrote something important

You’re close to hijacking control flow

It’s a normal part of exploit dev.

<img width="936" height="674" alt="Screenshot 2026-09-11 013609" src="https://github.com/user-attachments/assets/f7332fb5-0273-4b8f-b970-de93e83719ae" />

All chars for bad char check
<img width="880" height="641" alt="Screenshot 2026-09-11 213852" src="https://github.com/user-attachments/assets/3d57b8f4-c5e7-4299-8288-8f42df9feea6" />

<img width="859" height="399" alt="Screenshot 2026-09-11 214849" src="https://github.com/user-attachments/assets/7c68e7d5-481c-404a-99f2-ab90a3d83d00" />

<img width="883" height="640" alt="Screenshot 2026-09-11 214914" src="https://github.com/user-attachments/assets/a015376e-92bd-4320-97b1-ebb13f45f5af" />


For debugging I used easy to see input to find address where buffer variable is stored
AAAAAAAABBBBBBBCCCCCCCCBDDDDDDDD

<img width="888" height="229" alt="Screenshot 2026-09-11 215435" src="https://github.com/user-attachments/assets/ee920715-b9ea-4d9a-aaa6-0fd668903d36" />

<img width="898" height="355" alt="Screenshot 2026-09-11 215504" src="https://github.com/user-attachments/assets/5adc8bfa-743b-449d-82ee-97b6bd1deddd" />


###Trying to find bad characters

common bad characters

\x00    null byte      strcpy, strcat, scanf, sprintf: terminates most string ops

\x0a    newline        fgets, line-based protocols (HTTP, SMTP, telnet)

\x0d    carriage ret   HTTP parsers, some terminal protocols

\x20    space          whitespace-delimited parsers

\x26    &              URL-encoded fields

\x3d    =              key=value parsers

\xff    DEL            some terminal emulators

<img width="932" height="632" alt="Screenshot 2026-09-11 221725" src="https://github.com/user-attachments/assets/99a43994-1deb-4085-bc13-b8fd3aff8926" />


<img width="934" height="464" alt="Screenshot 2026-09-11 222632" src="https://github.com/user-attachments/assets/925c6c96-b01a-418c-8d11-28995ddbdc96" />

<img width="927" height="358" alt="Screenshot 2026-09-11 222704" src="https://github.com/user-attachments/assets/bc645b6c-e5b3-474c-8bce-70c15827a172" />

<img width="936" height="615" alt="Screenshot 2026-09-11 223638" src="https://github.com/user-attachments/assets/3b8ba95b-732e-4341-b2f2-c5ebb0bf23e8" />

Put the break point at 0x400552

<img width="930" height="422" alt="Screenshot 2026-09-11 225814" src="https://github.com/user-attachments/assets/59595047-cc51-414a-b0d7-532ad64ab018" />


<img width="926" height="360" alt="Screenshot 2026-09-11 231526" src="https://github.com/user-attachments/assets/d1c6f57e-c159-4bca-a598-d38d9934a443" />


Removed \x09 from the All chars
<img width="936" height="468" alt="Screenshot 2026-09-11 232625" src="https://github.com/user-attachments/assets/c19b5ac2-891a-4398-ba56-3f2587a7705f" />

Set the Break Point
<img width="933" height="391" alt="Screenshot 2026-09-11 232658" src="https://github.com/user-attachments/assets/814bce55-ee7e-42d8-8949-1f4e85671bc0" />

Removed \x0a from the All chars 
<img width="933" height="469" alt="Screenshot 2026-09-11 232735" src="https://github.com/user-attachments/assets/a280d8c3-68bb-4d1a-ac17-0caabb030fe9" />

Set the Break Point and continue
<img width="924" height="459" alt="Screenshot 2026-09-11 232807" src="https://github.com/user-attachments/assets/79d2bd33-7e72-4882-b23c-8a10edb91831" />

There is 0000 0000 after 1f, removing \x20
<img width="928" height="491" alt="Screenshot 2026-09-11 235308" src="https://github.com/user-attachments/assets/953f9f12-b7da-4e42-8c3e-1d2befba03e8" />

<img width="938" height="369" alt="Screenshot 2026-09-11 235551" src="https://github.com/user-attachments/assets/e5aefff9-e553-41be-8d6c-e9f443fb83a4" />

All chars are in order.

Bad chars: \x00\x09\x0a\x20

Using new shell code

<img width="942" height="419" alt="Screenshot 2026-09-12 002225" src="https://github.com/user-attachments/assets/f9ed1544-b8ee-4e6a-a8b8-40e83cce6ea3" />

<img width="942" height="358" alt="Screenshot 2026-09-12 002245" src="https://github.com/user-attachments/assets/aad565c7-f2f8-42ea-9f30-49fc90543c0a" />

<img width="953" height="378" alt="Screenshot 2026-09-12 002414" src="https://github.com/user-attachments/assets/c59d7b13-2a7a-4556-af24-907b32a8ac53" />

Set the break point to 0x400563
The address is on top of rsp to be read by ret instruction

<img width="935" height="646" alt="Screenshot 2026-09-12 002920" src="https://github.com/user-attachments/assets/380ca257-86a1-4e16-b4ac-f66691b77f34" />

<img width="941" height="388" alt="Screenshot 2026-09-12 003322" src="https://github.com/user-attachments/assets/bc1c4d91-28c1-4f11-a303-f8867873b188" />

The ds command hops to the right address.

<img width="934" height="359" alt="Screenshot 2026-09-12 003354" src="https://github.com/user-attachments/assets/f7b378ad-759e-4678-9bae-03fdf5dff612" />

When you’re walking toward the crash:

ds helps you see exactly when RIP gets overwritten.  

You can step instruction-by-instruction until the function returns and jumps to your corrupted saved RIP.

You can watch the stack pointer move as the vulnerable function copies your payload.

You can confirm shellcode placement by stepping until the crash and then inspecting memory (pxr @ rsp).

You can verify control flow hijack: once the function hits ret, ds will step into the jump to your overwritten RIP (usually 0x4141414141414141 during offset discovery).

<img width="945" height="369" alt="Screenshot 2026-09-12 004741" src="https://github.com/user-attachments/assets/1a9c1716-d9fe-4bb4-8502-050db1a7ee1a" />

Set the break point at 0x7fffffffe2a4

<img width="933" height="403" alt="Screenshot 2026-09-12 005417" src="https://github.com/user-attachments/assets/99dd17a0-fc44-40aa-823b-ff02cf73329f" />

Going step thru the NOPs

you can see the position of the shell code moved twice

<img width="937" height="385" alt="Screenshot 2026-09-12 005716" src="https://github.com/user-attachments/assets/70d3b21a-5e43-4ed2-b959-6167581ba7d0" />

<img width="926" height="661" alt="Screenshot 2026-09-12 171033" src="https://github.com/user-attachments/assets/595fa073-b5dd-4f7e-bc7a-6ecf96b28ede" />
After changing shellcode, removing bad chars, and changing return address, got the shell. But the user1 doesn't have permission to get the secret.txt file.

<img width="928" height="121" alt="Screenshot 2026-09-12 173131" src="https://github.com/user-attachments/assets/4abd65e1-efd9-4af7-8315-c86753afacac" />

Got one more shellcode for suid

<img width="937" height="212" alt="Screenshot 2026-09-12 173200" src="https://github.com/user-attachments/assets/e6a9dbeb-1e51-46ee-8afb-d0b46382299c" />

And got the shell with user2 permission and flag
### Alternative way

<img width="928" height="316" alt="Screenshot 2026-09-12 175729" src="https://github.com/user-attachments/assets/7ba6186f-6ead-4c29-8c15-768207539fdd" />

Used msfvenom to craft shell code for payload.

<img width="942" height="498" alt="Screenshot 2026-09-12 175813" src="https://github.com/user-attachments/assets/6e700756-086d-44b2-bb28-53ba718a0b1f" />

After inspecting the memory, set the break point db 0x7fffffffe240.

<img width="923" height="424" alt="Screenshot 2026-09-12 180017" src="https://github.com/user-attachments/assets/30572122-0a90-4468-bb7b-ace80a1590be" />





























