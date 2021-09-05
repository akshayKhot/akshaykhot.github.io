---
layout: post
title: "Unix: A History and a Memoir"
date: 2021-7-6
img: unix_memoir.jpg
---

Bell Labs, where Unix began, was a remarkable institution that produced many good ideas and capitalized on them. 

<div class="book">
<a target="_blank" href="{{ site.bookshelf }}/{{ page.img }}">
  <img src="{{ site.bookshelf }}/{{ page.img }}" alt="{{page.title}}">
</a>
</div>
An **operating system** is just a big and complicated program built from the same instructions as ordinary programs like Word or a browser. Its task is to control all the other programs trying to run and manage interactions with the rest of the computer.  

### History of Unix

**CTSS** was the most innovative OP of the time, allowing users to type on terminals connected to a big IBM machine (7094) instead of punch cards. It was more pleasant and productive than batch processing.

It was such a productive programming environment that MIT researchers decided to create an even better version called **Multics,** which stood for Multiplexed Information and Computing Service.

Multics was complicated, and needed new software and hardware than IBM 7094, so MIT enlisted GE (for hardware) and Bell Labs (for software).

Because it was so ambitious, Multics soon ran into problems. It was a victim of the **second system effect**. It was over-engineered, and was described as "an attempt to climb too many trees at once." Coordinating two companies and a university spread across the country was difficult. 

> Second system effect: After a success, it's tempting to try to creates a new system that fixes all the remaining problems with the original while adding everybody's favorite new features. The result is often a system that's too complicated, a consequence of taking on too many different things at the same time. 

Bell Labs worked on Multics from 1966 through 1969. By 1968, it realized that it was not going to achieve its goal of providing computing services at a reasonable cost. It was too expensive. Bell Labs dropped out of the project in April 1969. MIT and GE worked on it, and Multics was eventually completed and used until 2000, though not widely.

Multics was the source of many good ideas, but its biggest contribution was its influence on a tiny operating system called Unix.

### Unix

Unix was created in part as a reaction to the complexity of Multics. When Bell Labs pulled out of Multics, Ken Thompson and Dennis Ritchie, who were working on it, had to find something else to do. They spent time exploring ideas and doing paper designs. 

Around this time, Ken found DEC PDP-7, a dated computer with 16K bytes of memory. 

> “At some point I realized that I was three weeks from an operating system.” - Ken Thompson

He needed to write three programs, one per week.

1. An editor, so he could create code.
2. An assembler, to turn the code into machine language that could run on the PDP-7
3. A kernel - an operating system

At that time, Ken’s wife went on a three-week vacation to take their one-year-old son to visit Ken’s parents in California, and Ken had three weeks to work undisturbed.

As he (Ken) said during a 2019 interview, 

> One week, one week, one week, and we had Unix.

The first version of a recognizable Unix system was running in mid to late 1969. 

> In retrospect, I think that Bell Labs did a good job with space. Though they cost more than open areas, private offices give people peace and quiet, a place to focus without constant noise in the background, storage for books and papers, and a door to close for intense thought or private conversations.  
>
> By now, I've spent enough time in open-plan work areas to know that, for me at least, they are utterly destructive of concentration. The Bell Labs mixture of one’s own private office and a shared space for the community worked very well. 
>
> \- Brian Kernighan on open offices

### Features of Unix

It may be hard for today's readers to appreciate just how much of a simplification all Unix was. It hid all the irrelevant nonsense that earlier operating systems enforced on their users. 

**File system**

- A Unix file is simply a sequence of bytes. 
- Any structure or organization of the contents is determined only by the programs that process it. 
- Files are organized in directories containing file information e.g., name, access, size, date & time of creation/modification, etc. 
- Any directory can contain subdirectories, so the file system is hierarchical. 

**System calls**

- Provide a way to access the services that an OS provides, such as starting/stopping programs, reading/writing files, and accessing storage/network. 
- The Unix File system interface is very simple, with only five system calls to open or create a file, read or write its bytes, and close it. 

**Shell**

- The primary interface between the users and the operating system. 
- A program that runs other programs, lets users run commands. You can have multiple shells, as it's simply a user program. 
- A shell script is a sequence of commands stored in a file. Running the script runs the commands in a sequence. 

**Pipes**

- Perhaps the single most striking invention in Unix, providing a new way of thinking about how to design and use programs. 
- A pipe connects the output of one program to the input of another. 
- Doug McIlroy came up with the initial idea of screwing programs together like a 'garden hose' in 1964. However, it was not obvious how to make it work. He continued to nag, and Ken continued to think. 

It's a programming instance of an old strategy: **divide and conquer**. By breaking bigger tasks into smaller ones, each becomes more manageable, and you can combine the pieces in unexpected ways. 

> As Ken says, “One day I got this idea: pipes, essentially as they are today.” He added a pipe system call to the operating system in an hour; he describes it as “super trivial” given that the mechanisms for I/O redirection were already there. He then added the pipe mechanism to the shell, tried it out, and called the result “mind-blowing.”

**Grep**

- A pattern-searching program originally written by Ken Thompson. 
- The name grep comes from a command in the ***ed\*** text editor, ***g/re/p,\*** that prints all lines that match the regex pattern ***re\***; it's even in the Oxford English Dictionary. 

**Regular Expressions**

- A notation for specifying a pattern of text. It's a small language for describing text patterns. 
- A regex also allows you to specify more complicated patterns by giving special meaning to some characters, e.g. '.' matches a single character. 

> A common Unix story: a real problem from a real user, deep knowledge of relevant theory, effective engineering to make the theory work well in practice, and continuous improvement. It all came together because of broad expertise in the group, an open environment, and culture of experimenting with new ideas. 

### The C Programming Language 

Programming is the process of creating the sequences of operations that perform some desired task using some programming language. Compilers translate from higher-level languages (closer to human language) ultimately to the individual instructions of a specific kind of computer.  

C has been very successful, one of the most widely used languages of all time. As Dennis said in a paper for the second History of Programming Languages conference in 1993,

> C is quirky, flawed, and an enormous success. While accidents of history surely helped, it evidently satisfied a need for a system implementation language efficient enough to displace assembly language, yet sufficiently abstract and fluent to describe algorithms and interactions in a wide variety of environments.

### Seventh Edition (1976-1979)

The 7th edition was the source of much of the heritage shared by all Unix systems. It was a portable OS that ran on at least four different kinds of processors.

**Bourne Shell**
In 1976, Steve Bourne wrote a new shell whose goal was to make it a fully programmable scripting language. It provided programming constructs such as if-then-else, while, for, and case. It also included variables, both shell-defined and user-defined. 

You could use the shell to write pretty much anything that could be formulated as a sequence of commands. It could often do this well enough that there was no need to write a C program. 

Over the years, more features have been added, especially in Bash (Bourne Again Shell), which is the standard for most Linux and macOS users. 

**Yacc, Lex, Make**
Languages are used for communication. Better languages help us communicate more effectively. Good language lowers the barrier between **what we want to say** and **what we have to say to get some job done.**

Various Unix tools such as Yacc, Lex facilitated the creation of new languages and thus led to better ways to communicate with computers. 

Two main aspects characterize computer languages: 

1. **Syntax**: Describes the grammar, what the language looks like, what's allowed and what's not, rules for programming constructs, etc. 
2. **Semantics**: Meaning ascribed to the legal syntax, what does a legal construction mean or do. 

A compiler translates something written in one language into something semantically equivalent in another language, e.g. the C compiler translates the C code to assembly language. 

To compile the program, we first have to parse it, i.e. recognize names, constants, functions, etc., allowing us to assign these constructs later suitable semantics. 

**Yacc** is a program that generates a parser for a compiler. Steve Johnson wrote it in 1973. It consists of grammar rules for a language's syntax and the semantic meaning attached to the rules. Its name was inspired by a comment from Jeff Ullman, which stands for "yet another compiler-compiler".

**Lex** is a program that generates a lexical analyzer. Michael Lesk created it in 1975. A Lex program consists of regular expressions that define the lexical tokens to be identified for a programming language. 

> **Fun Note:** Mike's first version of Lex was quickly revised by an intern in the summer of 1976. That intern was Eric Schmidt, who went on to become the CEO of Google. 

Yacc and Lex work together. Each time Yaa needs the next token while parsing, it calls on Lex, which reads enough input to identify a complete token and passes that back to Yacc.

<a target="_blank" href="{{ site.images }}/yacc-lex.png">
  <img src="{{ site.images }}/yacc-lex.png" alt="Yacc and Lex">
</a>

> If a program writes your code for you, the code will be more correct and reliable than if you write it yourself by hand. If the program is improved, everyone benefits, whereas improvements to one hand-written program do not improve others. 

**Make** compiles and links together multiple source files to create a single executable program. Stu Feldman came up with the specification language describing how the pieces of a program depend on each other. He wrote a program (Make) that analyzed the specification and used the times that files had been changed to do the minimum amount of recompilation necessary to bring everything up to date. 

Make was an instant success, as it obviated a whole class of silly errors while making compilation as efficient as possible. One makefile could capture all the processing steps necessary to compile a new version of a program. It could also describe how to do related tasks like running lint, making a backup, and printing documentation. 

Though makefile had some of the same properties as a shell script, it used declarative language to specify the dependencies. 

> Rather than writing code or doing sequences of operations by hand, create a notation or specification that declares what has to be done, and write a program to interpret the specification. This approach replaces code with data, and that's almost always a win. (Ruby on Rails)

He (Hamming) felt that programming should be taught as writing was taught. There should be a notion of style that separated poor code from good code, and programmers should be taught how to write well and appreciate good style.  

### Beyond Research: Descendents of UNIX

After a few years in the lab in Center 1127, Unix began to spread, both inside Bell Labs and outside, the latter primarily through universities. 

In 1973, AT&T began licensing Unix to universities for a nominal fee. One of the most active license recipients was the University of California at Berkeley (UCB). Several graduate students made major contributions to the system that eventually became the Berkeley Software Distribution (BSD), one of two main branches that evolved from the original Unix.

The 7th edition was the last research version of Unix released. Though three more versions were developed, by the 10th version in 1989, it was clear that the center of gravity of Unix development had moved elsewhere.  

**BSD,** which stands for Berkeley Software Distribution) was developed by Bill Joy and his colleagues at UCB. BSD descendants, such as FreeBSD, OpenBSD, and NetBSD are still active.

**NextSTEP** was another spinoff of BSD, created for NeXT, founded by Steve Jobs in 1985. Though it was not a commercial success, Apple bought the company in 1997, and Jobs became the CEO within a year. The current **macOS** used in Apple computers derives from NextSTEP.

**Andy Tanenbaum created Minix** at the Free University in Amsterdam in 1987. It was a Unix lookalike compatible at the system call level but written entirely from scratch with a different kernel organization.

**Plan 9** was developed by a small group at Bell Labs - Ken Thompson, Rob Pike, Dave Presotto, and Howard Trickey. Ken and Rob also created Golang. It was an attempt to take the good ideas from Unix and push them further. However, due to the momentum of Linux, Plan 9 didn't catch on. It did contribute one thing of surpassing importance to the world, the UTF-8 encoding of Unicode. 

**Linux:** On August 25, 1991, a 21-year old Finnish college student named Linus Torvalds released Linux, by posting an email on comp.os.minix, a Usenet news group. What started as a few thousand lines of code now stands at well over 20 million lines, with Torvalds as the principal developer and coordinator of a worldwide developer community maintaining and enhancing it. 

At this point, Linux is a commodity operating system that can run on any computer. It's on literally billions of devices and runs a substantial part of Internet infrastructure, including servers for companies like Google and Amazon. 

### Legacy and Lessons

Unix has been tremendously successful. As Unix or Linux or macOS, it runs on billions of computers, serves billions of people, and has made billions of dollars for some (though not for its creators). It has also shaped later operating systems.

What accounts for the success of Unix? What can we learn from it? Primarily on two fronts: technical and organizational. 

**Technical**

Part of the genius of Ken Thompson and Dennis Ritchie was their tasteful selection of existing good ideas, and their ability to see a general concept or a unifying theme that simplified software systems. 

Here are some of the important technical ideas from Unix: 

- **Hierarchical File System**: Starting from the root directory, each directory either contains files, or other directories containing files or directories. Files are uninterpreted bytes; the system doesn't care what the bytes are, or know anything about their meaning. 
- **A high-level implementation language (C)**: Not only for user programs but also for the operating system. C led to the portability of the operating system. Instead of getting locked to specific proprietary hardware from hardware manufacturers with their proprietary languages, you simply used Unix, an open and widely understood standard, as a commodity.  
- **User-level programmable shell:** Made it possible to program by using programs as building blocks. It became another high-level language in the programmer's toolbox. 
- **Pipes**: Provide an elegant and efficient way to use temporary connections of programs. The notion of streaming data is intuitive, and the syntax is simple. 
- **Programs writing programs**: Writing programs by hand is hard, so if you can write a program that writes them for you, it's a big win. It's easier, and the generated programs are more likely to be correct, e.g. compilers, lexers, parsers, etc.  

> Unix Philosophy: Writing small programs that each do one thing well, rather than large and monolithic programs that try to do many things. 

**Organization**

A large component of Unix's success was due to non-technical factors, i.e. the managerial and organizational structure of Bell Labs, and the flow of ideas across a group of talented people working on diverse problems in a collegial environment. 

- **A stable environment:** Consistent and predictable - money, resources, mission, structure, management, culture. Researchers could explore ideas that they thought were important, for long periods, even years, without having to justify their efforts every few months.
- **Problem-rich environment**: Computer Science was a new field, with plenty of ideas to explore both theoretical and practical fronts. The interplay between theory and practice produced many good results, e.g. language tools and regular expressions.
- **Hire the Best**: Hiring was very carefully managed. My (Kernighan) preference has been for people who are really good at what they do, without worrying too much about specifically what it is. Bell Labs worked hard to try to attract good people. We used our own researchers as recruiters, not professional career recruiters. 
- **Technical Management**: Managers have to understand the work they manage. Management was technical all the way to the top and had a solid understanding of the work both within their own organizations and across others. Management supported their people, often collaborated, and never competed. 
- **Cooperative Environment**: For any technical area, there were multiple experts, often world leaders in their field. The culture was strongly cooperative and helpful. A superb technical library was open 24 hours a day, with subscriptions to a large collection of journals and remote access to other libraries. 
- **Fun:** It's important to enjoy your work and the colleagues that you work with. 1127 was almost always a fun place to be, not just for the work but also for being part of a remarkable group. At the same time, there was zero, or even negative, enthusiasm for the kinds of team-building exercises that one often sees today. Most of us saw them as artificial, pointless, and a waste of time. 

I (Kernighan) was a department head for over 15 years, was probably at best an average manager, and was definitely happy to step down. Others successfully resisted promotion for long periods; Dennis Ritchie became a department head well after I did, and Ken Thompson never did. 

> It takes effort to build and maintain an organization whose members like and respect each other, and who enjoy each other’s company. This can’t be created by management fiat, nor by external consultants; it grows organically from the enjoyment of working together, sometimes playing together, and appreciating what others do well.  

The big secret to doing good research is hiring good people, making sure there are interesting things for them to work on, taking a long view, and then getting out of the way. It certainly wasn’t perfect, but Bell Labs research generally did this well.

### Short Biographies of Key Unix People

**Ken Thompson**

- Born in 1943 
- Went to UCB to study electrical engineering 
- Electronics was his hobby for 10 years before college
- Arrived at Bell Labs in 1966 and started work on Multics
- Interest in games, especially Chess; and flying 
- Retired from Bell Labs in 2000
- Moved to Google in 2006
- Created Go programming language with Rob Pike and Robert Griesemer

> I consumed computers, I loved them. At that time, there was no computer science curriculum at Berkeley; it was being invented.  

> I was just going to stay in the university because... I owned it. My fingers were in absolutely everything. The main monster computer at university shut down at midnight and I’d come in with my key and I’d open it up and it would be my personal computer until 8 AM.

**Dennis Ritchie**

- Born in 1941
- Went to Harvard for undergrad in physics and grad in applied Maths.
- ACM Turing Award in 1983 for C and Unix
- Retired officially in 2007 but continued to come down to Bell Labs every day until his death in October 2011.

> Dennis was modest and generous, always giving credit to others while downplaying his own contributions. 

Dennis was a superb technical writer, with a spare elegant style, deft turns of phrase, and often with flashes of dry wit that accurately reflected his personality. He and I (Kernighan) wrote The C Programming Language together; it was published in 1978, with a second edition in 1988, and has since been translated into more than two dozen languages.

Dennis’s original C reference manual formed the basis of the ANSI/ISO standard for C that was first produced in 1988 and was a major part of the book. Without a doubt, some of the successes of C and Unix can be attributed to Dennis’s writing.

**Doug McIlroy**

- Received his undergraduate degree in Physics from Cornell in 1954 and Ph.D. in Applied Mathematics from MIT in 1959. 
- Worked for a summer at Bell Labs, joining permanently in 1958, and became head of the Computing Techniques Research dept. in 1965. 
- Once Unix was underway, he wrote a wide variety of fundamental software, e.g. storage allocator ***malloc, spell, diff, sort, join, graph, speak, tr, tsort, calendar, echo,\*** and ***tee.\*** Pipes were his idea, too (though the final version used Ken's syntax).
- Doug was a superb technical critic, often the first to try out some new program or idea. He would experiment at the earliest possible time and, since he had excellent taste, his opinions on what was good and what needed to be fixed were invaluable. 
- Stepped down from management role in 1986 and retired from the Labs in 1997, to teach at Dartmouth.    

Rob Pike has called Doug McIlroy "*the unsung hero of Unix*". Unix might not have existed, and certainly would not have been as successful, without Doug's good taste and sound judgment of both technical matters and people.  

> He’s (Doug) one of the finest technical writers that I know of. He has a flair for language, and a flair for economy of expression that is remarkable. - Al Aho

**Bill Joy**

Ken Thompson spent a sabbatical year at Berkeley in 1975 and 1976, where he taught courses on operating systems. Bill Joy, a grad student at the time, modified the local version of Unix, adding some programs of his own. It included the vi text editor, which is still one of the most popular Unix editors, and the C shell csh.

Bill later designed the TCP/IP networking interface for Unix that is still used today. His socket interface made it possible to read and write network connections with the same read and write system calls as were used for file and device I/O, so it was easy to add networking functionality.

**John Lions**

John Lions, a professor of computer science at the University of New South Wales in Sydney, was an enthusiastic early adopter of Unix and used it extensively in courses on operating systems and general educational and research support at UNSW.  

In 1977, John wrote a line-by-line “commentary” on the 6th edition source code. He explained every part of the source code in detail, so one could see how it worked, why it was the way it was, and how you could do it differently.

**Conclusion:** The Unix story certainly offers many insights into how to design and build software, and how to use computers effectively, which the book tries to highlight. The Unix philosophy of software tools made it possible to combine existing programs to accomplish a wide variety of tasks without writing new software. 