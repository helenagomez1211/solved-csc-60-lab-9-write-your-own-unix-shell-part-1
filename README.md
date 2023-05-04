Download Link: https://assignmentchef.com/product/solved-csc-60-lab-9-write-your-own-unix-shell-part-1
<br>
<strong><u>PURPOSE</u></strong>:  The purpose of this lab is to allow students to learn a user interface aspect of a UNIX shell.  Student will work with some basic system calls.

<strong>Important note:  please use sp1, sp2, sp3, or atoz servers for this lab.</strong>

<strong><u>UNIX Shell</u></strong>

We will start with 3 built-in commands:

<ul>

 <li><strong>exit</strong> (exit shell)</li>

 <li><strong>pwd </strong>(print working directory)</li>

 <li><strong>cd</strong> (change directory)</li>

</ul>

The built-in functions are <strong>not</strong> executed by forking and executing an executable. Instead, the shell process executes them itself.

Your shell is basically an interactive loop:

<ul>

 <li>it repeatedly prints a prompt “<strong>csc60msh &gt;</strong> “,</li>

 <li>parses the input, executes the command specified on that line of input,  and waits for the command to finish.</li>

</ul>

<strong><u>FILES TO COPY</u></strong>:

To get the file you need, first move to your class folder by typing:  <strong>cd csc60 </strong>Type: <strong>cp  -R  /gaia/home/faculty/bielr/files_csc60/lab9  .</strong>

Spaces needed:  (1) After the <strong>cp </strong>and after the <strong>-R               ↑ </strong>Don’t miss the space &amp; dot.

(2) After the directory name at the end &amp; before the dot.

After the files are in your account and you are still in <strong>csc60</strong>, you need to type:  <strong>chmod 755 lab9 </strong>This will give permissions to the directory.

Next move into lab9 directory by typing:  <strong>cd lab9</strong>

<h1>Type: chmod  644  lab9.c</h1>

This will give permissions to the file.

Your new lab9 directory should now contain:  lab9.c

<strong><u>Please follow these steps:</u></strong>

<ul>

 <li>Review the source codes, compile, and execute the programs. Examine the output texts to understand the behavior of each program.</li>

 <li>I have provided you with a shell template (<strong>c</strong>) that you can work from. You build your program into it. <strong><u>Read </u></strong>the existing code closely to identify the key components and understand its execution flow. You can compile the shell using the following command:     <strong>gcc</strong> <strong><em>lab9.c</em></strong></li>

 <li><strong>Function main.</strong> Handling <strong>built-in Commands</strong>: There are three special cases where your shell should execute a command directly itself instead of running a separate process.

  <ul>

   <li><em>First</em>, Additionally, we must deal with the fact that a user might just type an Enter Key with no command.</li>

   <li><em>Second</em>, if the user enters <strong>“exit”</strong> as a command, the shell should terminate.</li>

   <li><em>Third</em>, if the user enters <strong>“pwd”</strong>, print the current working directory. This can be obtained with <em>getcwd()</em></li>

   <li><em>Fourth,</em> if the user enters <strong>“cd dir”</strong>, you should change the current directory to “dir” 0by using the <em>chdir</em> system call. If the user simply types <strong>“cd”</strong> (no dir specified), change to the user’s home directory. The $HOME environment stores the desired path; use <em>getenv(“HOME”)</em> to obtain this.</li>

  </ul></li>

</ul>

<strong>Pseudo Code</strong>  (Highlight indicates provided code.)

/*———————————————————-*/ int main (void)

{

while (TRUE)

{

//         int childPid; char *cmdLine;

print the prompt();      /* <em>i.e. <strong>csc60msh </strong></em><strong>&gt;</strong> , Use printf*/

fgets(cmdline, MAXLINE, stdin);




/* You have to write the call. The function itself is <em>provided: </em>function parseline */ Call the function <strong>parseline</strong>, sending in <strong>cmdline</strong> &amp; <strong>argv</strong>, getting back <strong>argc</strong>

/* code to print out the argc and the agrv list to make sure it all came in. <strong>Required</strong>.*/

Print a line. Ex: “Argc = %i” loop starting at zero, thru less than agrc, increment by one.{       print each argv[loop counter]   [ (“Argv %i = %s 
”, i, argv[i]); ] }

/* Start processing the built-in commands */ if ( argc  compare-equal-to  zero){

/* a command was not entered, might have been just Enter or a space&amp;Enter */        <em>continue</em> to end of while(TRUE)-loop

}

// next deal with the built-in commands

//   Use <em>strcmp</em> to do the test

// <em>if(strcmp(argv[0], “exit”) == 0)  </em>     // <strong><em>Sample of complete line.</em></strong>

//   after <strong>each</strong> command except for “exit’, do a <em>continue</em> to end of while(TRUE)-loop      if (“exit”)

{       issue an exit call

}

 <em>the continued Else-IF is on next page</em>….

else if (“pwd”)

{

declare a char variable array of size MAX_PATH_LENGTH to hold the path  (MAX_PATH_LENGTH is in a #define…. look for it)       do a getcwd     (May skip error checking here)       print the path       continue

}

else if (“cd”)

{

declare a char variable <em>dir </em>as a pointer (with an *)       if the argc is 1

{

use the getenv call with “HOME” and

return the value from the call to variable <em>dir</em>

}       else

{

variable <em>dir</em> gets assigned the value of argv[1]

}

execute a call to chdir(dir) with error checking. Message = “error changing directory”       continue

//…end of the IGNORE above…………………….

}                 /* end of the while(TRUE) */

}                       /* end of main */

<h1>Partnership</h1>

Students may form a group of 2 students (maximum) to work on this lab.  As usual, please always contact your instructor for questions or clarification.  Your partner does not have to attend the same section.

All code files should include both names.

Using <strong>vim</strong>, create a small name file with both of your names in it. When you start your script file, <em>cat</em> that name file so both names show up in the script file.

You <strong>must BOTH</strong> submit your effort.  As both of your names occur on everything, when I or another grader find the first submission, we will then give the same grade to the second student.

<strong>Useful Unix System Calls </strong>(Also see PowerPoint Slides named<strong> Lab9 Slides</strong>):

<table width="623">

 <tbody>

  <tr>

   <td width="623"><strong>getenv</strong>: get the value of an environment variable</td>

  </tr>

  <tr>

   <td width="623">     path = <strong>getenv</strong>(“PATH”);</td>

  </tr>

  <tr>

   <td width="623">     cwd = <strong>getenv</strong>(“PWD”);</td>

  </tr>

  <tr>

   <td width="623"><strong>getcwd</strong>: get current working directory.</td>

  </tr>

  <tr>

   <td width="623"><strong>chdir</strong>: change the current working directory (use this to implement <strong>cd</strong>)</td>

  </tr>

 </tbody>

</table>

<h1>Compilation &amp; Building your program</h1>

The use of <em>gcc</em> is just fine.  If you want to have the executable have a different name from  a.out, type: gcc <em>–o  name-of-executable</em>  name-of-source-code

<h1>Marks Distribution</h1>

Lab 9 with the built-in commands is worth 38 points.

<h1>Hints</h1>

Writing your shell in a simple manner is a matter of finding the relevant library routines and calling them properly. Please see the resources section below.

Keep versions of your code. This is in case you need to go back to your older version due to an unforeseen bug/issue.

A lot of code to be used in Lab10 is currently commented out.  Leave it there.  At the start of Lab10, you will receive instructions about which comment marks you should remove.

<strong>C Library functions:</strong>

<table width="623">

 <tbody>

  <tr>

   <td width="623">#include &lt;string.h&gt; <em>String compare:</em>int strcmp(const char *s1, const char *s2);<em>This line is in #include &lt;string.h&gt; &amp; does <strong>not</strong> need to be duplicated in your code.</em>if(strcmp(argv[0], “exit”) == 0)       // <strong>Sample of complete line. </strong>     strcmp(argv[0], “cd”)      strcmp(argv[0], “pwd”)      strcmp(….,”&gt;”)      strcmp(….,”&lt;“)<em>Print a <strong>system</strong> error message:</em>perror(“Shell Program error
”);<em>Input of characters and strings:</em>fgets(cmdline, MAXLINE, stdin);</td>

  </tr>

 </tbody>

</table>

<strong>Preparing your script file:    </strong>

When all is well and correct, type:

<h1>        1.   script StudentName_lab9.txt</h1>

<ol start="2">

 <li><em>If you are on a team, cat your name file here. </em></li>

</ol>

At the prompt, type:

<table width="297">

 <tbody>

  <tr>

   <td width="24"><strong>3.</strong></td>

   <td width="144"><strong>gcc lab9.c -Wall</strong></td>

   <td width="129">to compile the code</td>

  </tr>

  <tr>

   <td width="24"><strong>4.</strong></td>

   <td width="144"><strong>a.out</strong></td>

   <td width="129">to run the program</td>

  </tr>

 </tbody>

</table>

Enter in sequence:

<ol start="5">

 <li>the Enter Key,</li>

 <li>a Space, and then the Enter Key,</li>

 <li>pwd</li>

 <li>cd <strong>..</strong></li>

 <li>pwd</li>

 <li>cd lab9</li>

 <li>pwd</li>

</ol>

<h1>12. cd</h1>

<ol start="13">

 <li>pwd</li>

 <li>exit (exit from the script)</li>

 <li>exit (exit from the shell)</li>

</ol>

If all worked, submit your two files to Canvas.

<h1>Deliverables</h1>

Submit <strong>two</strong> files to Canvas. No zip files please.

<ol>

 <li>c</li>

 <li>txt</li>

</ol>