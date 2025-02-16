

**Scanning and Enumeration**

Starting with port scanning and service enumeration using Nmap

![](https://cyber247record.wordpress.com/wp-content/uploads/2024/07/image-1.png?w=670)

_Nmap scan_

The next step is to further investigate the front and back end of the website. For that we will begin with using a simple add-in (Wappalyzer) to detect any web technologies being used on the web server’s back-end.

![](https://cyber247record.wordpress.com/wp-content/uploads/2024/07/image-2.png?w=1024)

_Wappalyzer_

In this case, we were unable to detect any further technologies besides the fact that we know Golang is being used as the back-end programming language.

Next, we would require to perform web directory busting, in order to identify all possible web domain directories and their further nested sub-directories using two tools, Gobuster and Feroxbuster and analyse the results.

![](https://cyber247record.wordpress.com/wp-content/uploads/2024/07/image-3.png?w=673)

_Gobuster_

![](https://cyber247record.wordpress.com/wp-content/uploads/2024/07/image-4.png?w=879)

_Feroxbuster_

You will notice that we’ve obtained two different varying results between using both Gobuster and Feroxbuster. The reason I prefer using more than one tool to do the exact same task is to obtain as much results as possible from two different sources. That way we are not relying on simply one source of information as one tool could overlook something the other tool would not.

Currently we notice a pattern of sub-directories, naming the “Host/r/a/b/” which most likely would be spelling the word “rabbit”, hence the photo shown on the website. Therefore, we attempt to browse into each individual sub-directory of each character in that word.

![](https://cyber247record.wordpress.com/wp-content/uploads/2024/07/image-6.png?w=1024)

_Source code_

Browsing through the source code of every web directory, I have noticed a hidden html style tag with what appears to be a username and a password.

**Exploitation and Gaining Access**

Now knowing the fact that there are no login pages on the website, we can confidently jump to the only possible conclusion that the credentials are meant for remotely logging into the machine using the SSH service.

![](https://cyber247record.wordpress.com/wp-content/uploads/2024/07/image-7.png?w=653)

_SSH_

![](https://cyber247record.wordpress.com/wp-content/uploads/2024/07/image-8.png?w=945)

_Checking for sudo permissions_

After checking our permissions using “sudo -l” to check whether we can use the sudo command, we notice that our user Alice is only able to run a python script stored on our home directory as the user rabbit.

![](https://cyber247record.wordpress.com/wp-content/uploads/2024/07/image-9.png?w=474)

_Contents of Python script_

We also notice that it is no special Python script, only seems to import a “random” library and prints out some text on the screen. In order to abuse this script we would first need to understand a crucial concept that Python has a hierarchy by which libraries are imported.

![](https://cyber247record.wordpress.com/wp-content/uploads/2024/07/image-10.png?w=829)

_Stack Overflow_

Looking into Stack Overflow, the “import” function in Python will typically look for the module or library to be imported from within the same folder.

**Escalating Privileges**

Equipped with this knowledge we can proceed with creating our very own “random” module containing malicious commands to escalate our access.

![](https://cyber247record.wordpress.com/wp-content/uploads/2024/07/image-11.png?w=1024)

_GTFOBins_

After checking GTFOBins, under the Python section there was a command to obtain a shell, we then proceed with creating a malicious “random.py”. However, we need to remove the “python -c” because there is no need for it as it is not possible to call on Python within a Python script that is being executed by Python itself.

![](https://cyber247record.wordpress.com/wp-content/uploads/2024/07/image-14.png?w=293)

_Malicious random.py_

Now, in order to trigger our payload, we would need to execute the Python script in the context of the rabbit user along with the sudo command.

![](https://cyber247record.wordpress.com/wp-content/uploads/2024/07/image-15.png?w=754)

_Triggering the malicious payload_

In this instance we were successful in gaining access to the “rabbit” user. Let’s have a look at the home directory for a sub-directory for rabbit.

![](https://cyber247record.wordpress.com/wp-content/uploads/2024/07/image-17.png?w=584)

_Contents of /home/rabbit_

Taking a look into the contents, we notice what appears to be an executable file with the SUID bit set, which is quite interesting since executing SUID binaries would enable us to gain access to root.

![](https://cyber247record.wordpress.com/wp-content/uploads/2024/07/image-18.png?w=552)

_Executing teaParty_

Executing the binary does not seem to be that beneficial, but we can use the “strings” command to take a look at any potential variables or modules to be abused for our own advantage.

![](https://cyber247record.wordpress.com/wp-content/uploads/2024/07/image-19.png?w=275)

_Strings_

It appears that the target machine does not have the strings binary installed. We would require to move the file and inspect it on our own Kali in this instance using the SCP tool and then further investigate locally.

![](https://cyber247record.wordpress.com/wp-content/uploads/2024/07/image-20.png?w=840)

_SCP_

```
┌──(kali㉿kali)-[~/Desktop]
└─$ strings teaParty                                
/lib64/ld-linux-x86-64.so.2
2U~4
libc.so.6
setuid
puts
getchar
system
__cxa_finalize
setgid
__libc_start_main
GLIBC_2.2.5
_ITM_deregisterTMCloneTable
__gmon_start__
_ITM_registerTMCloneTable
u/UH
[]A\A]A^A_
Welcome to the tea party!
The Mad Hatter will be here soon.
/bin/echo -n 'Probably by ' && date --date='next hour' -R
Ask very nicely, and I will give you some tea while you wait for him
Segmentation fault (core dumped)
;*3$"
GCC: (Debian 8.3.0-6) 8.3.0
crtstuff.c
deregister_tm_clones
__do_global_dtors_aux
completed.7325
__do_global_dtors_aux_fini_array_entry
frame_dummy
__frame_dummy_init_array_entry
teaParty.c
__FRAME_END__
__init_array_end
_DYNAMIC
__init_array_start
__GNU_EH_FRAME_HDR
_GLOBAL_OFFSET_TABLE_
__libc_csu_fini
_ITM_deregisterTMCloneTable
puts@@GLIBC_2.2.5
_edata
system@@GLIBC_2.2.5
__libc_start_main@@GLIBC_2.2.5
__data_start
getchar@@GLIBC_2.2.5
__gmon_start__
__dso_handle
_IO_stdin_used
__libc_csu_init
__bss_start
main
setgid@@GLIBC_2.2.5
__TMC_END__
_ITM_registerTMCloneTable
setuid@@GLIBC_2.2.5
__cxa_finalize@@GLIBC_2.2.5
.symtab
.strtab
.shstrtab
...
...
...
.data
.bss
.comment
```

After analysing the contents of the teaParty binary using the strings command, we notice that it is obtaining the date and time using the built-in system function since it is not importing any libraries or modules.

![](https://cyber247record.wordpress.com/wp-content/uploads/2024/07/image-22.png?w=477)

We begin by creating a malicious date file and host it on Kali to be downloaded on the target machine using the wget command and saved in a folder that we have write permissions to, usually this would be /tmp.

![](https://cyber247record.wordpress.com/wp-content/uploads/2024/07/image-23.png?w=814)

Now an important command we would need to run is to export the /tmp folder as a path in our global environment, to have it accessible globally on the target system, especially when executing the Python script.

![](https://cyber247record.wordpress.com/wp-content/uploads/2024/07/image-24.png?w=224)

We would also need to have date file exactable using the chmod command.

![](https://cyber247record.wordpress.com/wp-content/uploads/2024/07/image-25.png?w=187)

![](https://cyber247record.wordpress.com/wp-content/uploads/2024/07/image-26.png?w=440)

Next next

![](https://cyber247record.wordpress.com/wp-content/uploads/2024/07/image-27.png?w=401)

Now that we have access to the hatter user, we can see the contents of his home directory on the system. Using the above password we were able to SSH into the system as hatter.

Currently it seems like we are not progressing towards accessing the root user but rather accessing different users on the system, therefore, we resort to uploading and executing the automated script linpeas.sh.

![](https://cyber247record.wordpress.com/wp-content/uploads/2024/07/image-28.png?w=362)

After investigating the critical aspects within the output of linpas, I discovered the "Capabilities" vulnerability for privilege escalation to root.

![](https://cyber247record.wordpress.com/wp-content/uploads/2024/07/image-29.png?w=1024)

I then managed to escalate my privileges to root by exploiting the Perl Capability. 

![](https://cyber247record.wordpress.com/wp-content/uploads/2024/07/image-30.png?w=739)
