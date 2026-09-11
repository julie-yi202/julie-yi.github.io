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
0x7fffffffe78




