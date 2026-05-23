# IBM-i-AS400-Documentation-Case-Study

I set this up over a single evening to get real hands-on experience with IBM i before applying to a Command Center infrastructure role. No virtual machine, no hardware · just a free public IBM i 7.5 server called pub400.com and a 5250 terminal emulator (tn5250j).

Everything below is from that session. The screenshots are real, the commands are ones that operators use day to day.

1. Connecting to a live IBM i system

  Configured tn5250j to connect to pub400.com over SSL (port 992). The system runs IBM i 7.5 and is used by hundreds of people around the world to learn and practice. Getting the SSL certificate accepted and the session established was the first real hurdle.

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/4b44efbd-666d-4596-8f02-2ece510e3e2e" /> Login screen on PUB400 · IBM i 7.5, Server: PUB400, Subsystem: QINTER2

2. First login and password change

   On first sign-in, IBM i forces a mandatory password change · standard security policy. You fill in the current password, set a new one, and verify it. Navigating this with Tab through the 5250 form fields was a good early lesson in how the terminal model works.

   <img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/d84b38cd-9a5f-492d-8001-d2d12488407d" /> Change Password screen · profile ZELPR, forced update on first access

3. IBM i Main Menu

   After the password change, the system drops you into the IBM i Main Menu. This is the central navigation point for everything · system tasks, file management, programming, communications. A Command Center operator would typically bypass this and run CL commands directly, but understanding the menu structure matters.

   <img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/fa44a814-9409-4d7d-ae79-f586eea17645" /> GO MAIN · the IBM i top-level navigation menu, System: PUB400

4. Checking the message queue with WRKMSG

  WRKMSG displays messages in your user message queue · this is how the system communicates events, errors, and alerts to operators. In a production environment, this is one of the first places you check when something goes wrong. In this session the queue was clean, which is also useful to know.

  <img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/88f21d11-665b-4e03-8bdb-5dcc738357d1" /> WRKMSG · Display Messages for ZELPR, Queue: QUSRSYS, Delivery: *BREAK

5. Monitoring active jobs with WRKACTJOB

  WRKACTJOB is the core command for live system monitoring. It shows every active job on the system, their CPU usage, type, and status. This is what a Command Center operator watches during an incident to spot jobs that are hung, consuming too much CPU, or behaving unexpectedly. Here the system had 1064 active jobs at the time of the screenshot.

  <img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/504882c9-d3ac-4ca0-9085-ca643a971500" /> WRKACTJOB · 1064 active jobs, CPU 0.0%, subsystems QSYS and DONGENAV visible

6. Reading system load in real time

Running WRKACTJOB a second time showed a spike to 31.9% CPU with 1059 jobs active. Watching how the numbers shift between refreshes gives you a feel for what normal load looks like · and by extension, what abnormal looks like. This pattern recognition is core to incident triage.






  



