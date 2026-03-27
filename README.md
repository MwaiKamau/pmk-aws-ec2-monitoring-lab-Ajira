<img width="2560" height="1440" alt="Launching-Your-Amazon-EC2-Instance" src="https://github.com/user-attachments/assets/bb23e00e-c0c1-4e0c-bc2c-ac0e7af1079e" />
<img width="1097" height="932" alt="ec2-instance-connect-endpoint-1" src="https://github.com/user-attachments/assets/df21d4e6-3f75-44e8-8611-a2225e6846b0" />
<img width="1000" height="469" alt="instance_storage" src="https://github.com/user-attachments/assets/46bf36c7-7503-4171-b765-a6af80653b04" />

![PMK-AWS-Ajira-Alarm](https://github.com/user-attachments/assets/e44d30ec-11ea-4042-ae17-7d84f71d23f2)



![PMK-AWS-Ajira-Alarm-03](https://github.com/user-attachments/assets/5df5a1a6-275b-4f10-a1f1-a29a312b178d)



**Here is a detailed, step-by-step guide on how I created my first EC2 instance.**- 
I designed this tutorial for absolute beginners, and it includes instructions for publishing on GitHub and Medium (see also notes on how to save the screenshots for later use).

+ You’re sitting across from me now, coffee in hand, ready to dive into EC2 like we’ve done a hundred times before. Picture this: I’m sketching things out on a napkin because whiteboards feel too stiff for what we’re about to do. We start slow - launch an instance, pick an AMI, nothing wild yet. 

+ Then security groups come up, and yeah, they matter more than most admit at first. You frown slightly, so I pause, let it sink in. Subnets pop up next; one wrong choice here and everything feels off later. Key pairs? Always trip someone up, but not you - not today. Each click builds something real under your fingers. The console blinks once, then confirms: running. Your face lights up. It’s alive - but better, because you built it.

**First Time Using EC2 As a Cloud Beginner**-
A fresh start on setting up your first online machine - simple steps, real mistakes, what actually works. Watch it run, catch problems early, and learn while doing. This path skips confusion, focuses on clarity, and builds confidence slowly. Mistakes happen. They teach more than success ever could.

**Why I Wrote This**-
Truth is, I’ll speak plainly.

+ Funny thing - my gut reaction to hearing “launch an EC2 instance” was nerves. Back then, cloud stuff seemed built for folks with stacks of diplomas, one after another.

+ Yet this truth hit me slowly - beauty lives right inside, how simple it is.

+ This guide came together just how I hoped to find one years ago. Not stuffed with terms tossed out randomly. Nothing pretending you’ve memorised networking basics already. More like a quiet chat, shoulder to shoulder, watching my earliest try at starting an EC2 instance - one wrong turn, then small win after small win.

+ Right now, I’m where I am - and still making it happen. That means you could too, just by moving forward. This next part? We’ll get there at the same pace.

**What We're Building**-
When we finish this guide, both of us will already know:

+ A fresh EC2 machine now runs inside Amazon's network. This one lives entirely online, no physical box needed. Built using AWS tools, it powers up remotely. A cloud-based setup means access from anywhere counts. Remote computing starts here, flexible by design.

+ Keep an eye on how hard the processor is working by turning on tracking tools. Watch what happens inside when tasks run, using built-in checks. 

+ Spot shifts in speed through steady observation over time. Notice changes quietly while systems stay active behind the scenes.

+ Got alerts by email that do what they promise. Works without fuss. Sends updates when things shift. No extra steps needed. Runs smoothly in the background. Catches changes fast. Stays quiet till there is something real. Shows up only when it matters.

+ A burst of fake traffic hit the server, then alarms flashed instantly. The system reacted without delay when stress climbed past limits

Imagine actually doing cloud tasks, not just reading. Hands-on work replaces theory every single time.

**The Big Picture in Simple Words**-
Here is how I see the structure - forget strict terms, this is simply what makes sense in my head.

+ Setting Up a Small Office in a Secure Business Park

+ A virtual private cloud works like a business park meant just for you. Think of it as land surrounded by walls, separate from everything else. Amazon sets up an initial area named the Default VPC right away. That means no need to lay down barriers yourself at the start.

+ Picture a subnet like one particular building in a business park. Its spot is marked by an address. That is exactly where your server takes up space.

+ A doorway stands where visitors arrive. Through it, folks step into your space from beyond. That opening? The internet gateway - your entry point.

+ A single desk setup in an open room - that is what an EC2 instance feels like. It runs just like a real machine would, only it exists in the cloud. Think of it as a space where tasks happen quietly, without fuss. Instead of wood and metal, you get processing power and memory assigned on demand. Work lives here while everything else supports from behind.

+ A single watcher keeps tabs on your servers, like someone noticing steam building behind closed doors. Heat spikes - say, CPU running hard - and that watcher signals trouble without delay. It sits there quietly until numbers climb, then speaks up fast.

+ A warning pops up when temperatures climb too high - like a watchful helper tapping you on the shoulder. It does not shout. Instead, it slips a note under the door. Heat builds inside, yet the alert arrives calm, clear. A signal moves out once thresholds shift. Think of it as someone leaning close, saying it is time to look. Not loud. Just firm. Attention follows

Funny how a single image made it all fall into place.

**1.0 launching my first EC2 instance**-
Finding my way took some tries. That mix-up? Right there - that one tripped me up - might slow you down too.

**1.1 Logged into AWS Console**-
One day, I opened my browser, put aws.amazon.com into the bar up top. Logging in came next - smooth, quick. In case you’re new there, just make an account first thing. True, they want credit card details early on. Even so, I stuck strictly to what’s free. Not once did money leave my wallet.

**1.2 Found EC2**-
At first glance, the screen looked messy after I typed EC2 into the search. Then came a click. That one orange button stood out once I stopped expecting simplicity. A voice inside said keep going

**1.3 Clicked "Launch Instance"**-
A sudden urge made me press that bright orange button. Each tap felt different - sometimes shaky, sometimes bold.

**1.4 Named My Instance**-
Something clicks when labels make sense - I put MyFirstEC2Instance under "Name and tags." Practice shapes up slowly, like naming resources right each time.

**1.5 Select an Operating System**-
Later on, under Application and OS Images, Amazon Linux was what I picked. A line appeared below it - green letters saying Free tier eligible. Those words, colored like fresh leaves, stayed close with each step after that.

**1.6 Selected Instance Type**-
Picking t2.micro made sense. This time around, the screen showed "Free tier eligible" once more. A small relief washed over me.

**1.7 Key Pair Created**-
This moment gave me pause. What even is a key pair?

+ _That thing? It works like a passcode for your machine online. Without it, you just can’t get in._

+ A window popped up after I hit Create new key pair. My-first-keypair appeared in the name box. Instead of defaults, I picked RSA along with the .pem format. The system reacted by showing a download prompt. At that moment, a file landed on my local drive.

+ Almost messed up big time. That file nearly vanished. Keep hold of it. Tuck it away where it won’t disappear. Replacing it isn’t an option. My copy lives inside a folder named AWS-KEYS. Made sure another version sits safely elsewhere.

**1.8 Configured Network Settings**-
This felt overwhelming at first, yet when I pressed Edit, there it was - AWS had quietly prepared both the Default VPC along with a Default subnet. A quiet nod went out to the person behind that move.

+ A public IP gets handed out automatically when you flip the switch on that setting. Your machine shows up online because of it.

+ A fresh firewall - named my-first-sg - was set up. Inside it, just a single rule found its place

+ __Type: SSH

+ Source: My IP__

My IP showed up right away on AWS. That setup keeps others out - just my machine gets through. Stays locked tight that way.

**1.9 Configured Storage**-
That one time, I noticed 8 GiB sitting there. Left it be. Since the Free Tier includes 30 GiB, no issue came up.

**1.10 Clicked "Launch Instance"**-
I waited, then pressed the button.

+ A green note popped up on the screen. Following it, I pressed the instance ID, then saw how the status shifted - first stuck at Pending, later flipping into Running.

+ I stared at the screen for a moment. "I just launched a server. In the cloud. From my laptop."

Magic shimmered in the air. Not quite magic, though - just me figuring things out.

**2.0 Create an Alert System with SNS**-
These days, giving my server a voice feels like the next step. It started making sense after thinking it through slowly. A quiet machine that answers back - that idea stuck around. Talking instead of typing began to seem natural. The silence between us needed breaking somehow. Words replacing clicks just made sense eventually.

**2.1 Opened SNS**-
Last time I checked the console, SNS came up in the results. That stands for Simple Notification Service.

**2.2 Created a Topic**-
A button labeled Create topic got pressed. The setting stayed on Standard without changes. HighCPUAlerts appeared as the chosen name.

A single topic holds many messages together. Picture it like an email group where notes collect.

**2.3 Created a Subscription**-
The screen showed a button marked Create subscription. After tapping it, the form appeared. Information had to go into each field. Every section was completed one after another

+ _Protocol: Email

+ My Email Address_

After that, I pressed the button labeled Create subscription

**2.4 Confirmed My Email**-
A message waited inside my inbox, sent by AWS Notifications. There it was - a prompt to confirm, so I pressed the button marked Confirm subscription

A screen lit up with words: my name was on a list. That moment brought quiet satisfaction. Messages from my machine could finally reach me by mail

**3.0 Create CloudWatch Alarm**-
Finding someone to keep an eye on my server now.

**3.1 Opened CloudWatch**-
Looking up CloudWatch happened inside the console.

**3.2 Created an Alarm**-
I Clicked All Alarms Then the Orange Create Alarm Button.

**3.3 Selected the Metric**-
One tap opened the menu - then I moved straight into settings. The next step showed up fast after that choice

+ Ec2 per instance metrics

There I spotted the running instance - MyFirstEC2Instance was what I looked up - and after that, CPUUtilization got a check beside it. Then came the click on "Select metric." The screen changed slightly

**3.4 Alarm condition set**-
That alert turns on once the CPU jumps past seventy per cent.

One single datapoint triggers the alert - set at 70%. A breach happens fast; just one spike past that line wakes up the system.

**3.5 Configured the Action**-
For the Alarm state trigger setting, it was set to In alarm.

I Chose HighCPUAlerts As My SNS Topic.

**3.6 Named the Alarm**-
A label popped into my head - High-CPU-Alarm - and I stuck with it

**3.7 Created the Alarm**-
A tap on Create alarm made it show up right away, sitting there in the list with a steady OK mark.

A shadow watches over my server these days. It stands silent, always on duty.

**4.0 Step Four: Testing All Parts**-
Here it was, time to see. Would the setup do what it needed to?

**4.1 Connected to My Instance**-
Back at EC2, I found the active instance. A click on Connect opened the link

+ Starting fresh meant skipping the usual setup. A browser window opened right into the server - no keys needed. For someone just learning, it felt like a quiet win.

+ A button labelled Connect got pressed. A terminal popped up inside the web page.

I Was Inside My Server.

**4.2 Generated CPU Load**-
In The Terminal (AWS Command Line Interface-AWS CLI) I Typed

+ _text
dd if=/dev/zero of=/dev/null &
This command makes endless zeros, then throws them away. In effect, it says to the machine: push yourself to the limit_

I pressed Enter.

**4.3 Watched the Alarm**-
Clicking a new tab, I pulled up CloudWatch. The alarms screen loaded again after a refresh.

+ Still nothing after sixty seconds had gone by.

+ Last check - two minutes gone. All clear so far. Not too late yet.

+ After that, near three minutes in, everything shifted.

+ A flash of red lit up the room. Panic followed close behind.

A shiver ran down my spine. This is really happening

**4.4 Checked My Email**-
I Opened My Inbox.

+ Out of nowhere, an email appeared. From AWS Notifications. The subject line read:

+ ALARM High CPU Usage Alert in US East N Virginia

+ Inside the message was info on my setup, along with what level the processor hit before triggering the notice. That happened just after three in the morning.

Back in my chair, a grin spread across my face. The message from my server arrived - running at full effort, it said.

**4.5 Stopped the Load**-
Back at the terminal, typing

_+ _text
killall dd_
+ Everything came to a halt. After some time had passed, the alert on CloudWatch shifted back to normal._

Fine job by the machine today - smooth run, no hiccups at all.

**What I Learned- The Emotional Truth**-
What surprised me most wasn’t the tools themselves. Something else stuck - how solving real problems changed my thinking

**Default VPC First**-
Afraid of connecting systems, I started slow. Yet AWS handed me a ready-made structure - simple, functional. That freedom meant my attention stayed on the machine, not tangled in gateways or routing details. Starting complex? Not necessary. The first steps thrive on simplicity.

**EC2 Instance Connect Makes Access Simpler**-
That moment I stumbled on SSH and keys? Total confusion. Suddenly, EC2 Instance Connect showed up - no more hurdles, just straight into the machine. Great when you're figuring things out. Give it a go.

**Monitoring Gives Life to the Cloud**-
That old server used to sit there, silent. Once CloudWatch was running, everything shifted. It started sending signals, almost like breathing. Warnings popped up in red - one blinked hard, urgent, as if shouting without sound

**The Free Tier Is Generous- But Stay Aware**-
Even on Free Tier, I picked up one key habit - shutting down machines after use. When the job ends, a killall dd call halts the workload. Letting it run nonstop adds charges over time. Every new task gets a closing routine without exception.

**You Don't Have to Know Everything Before Beginning**-
Out of confusion came a setup that watches systems as it should. A message popped up one morning - proof that something ran right. That moment made clouds feel less distant, more mine. At first, Amazon's tools seemed foreign, nearly impossible.

+ This sensation? It’s the one I aim for you to feel.

+ AWS Services Used: Simple Summary

+ The AWS service and what it did for me

Running on Amazon EC2. That machine powers everything here. Core piece right there. Inside Amazon's virtual walls, my machine had a home. There, by sticking to the preset setup, life stayed uncomplicated. When the server worked harder, I noticed its CPU heat rising. That spike triggered a warning right away. Whenever the alert goes off, Amazon SNS shoots over an email. That’s how my server speaks up.

**Screenshots I Captured**-
One snapshot came first, showing where I started. Another followed after, capturing what changed along the way. The last one arrived later, marking how things stood when I finished

+ A green light on the dashboard - my EC2 instance is up, humming along without a hitch. Status checks cleared, no warnings blinking. That quiet confidence when systems do what they should.

+ A flash of red on the screen - there it is, the CloudWatch alert lit up. That colour means business, showing the system caught something off. Instead of staying quiet, it spoke loudly. A sign things are running as they should, even when trouble shows. Not every signal brings panic; sometimes it's proof that the watch never blinked.

+ A message showed up, sent by the system itself. This wasn’t just any note - it meant the machine had reached out on its own.

A folder named /screenshots held the files I set aside. Into the project they went, tucked neatly where they belong.

**Publishing This Project**-
This path felt worth telling, which is why you can now find it across two spots

**On GitHub**-
AWS EC2 first instance monitoring repository created

+ This whole guide got turned into a README.md file

+ A small directory appeared - named screenshots. Inside sat three image files I had placed there earlier. One by one, they were added, each saved carefully. The setup stayed minimal, just enough to keep things clear

+ Marks in the document now connect pictures just right. How do the visuals attach? Through formatted text hints that guide each placement carefully

Committed and pushed

**On Medium**-
New Story Created

+ Paste Content Into Editor

+ Uploaded screenshots directly

+ Hit publish

Turns out, passing on lessons hit just right - same warmth as when they clicked for me.

**A Final Word to You**-
If You Are Unsure About Cloud Computing, This Is For You

+ Right there, I stood in your shoes.

+ Fear crept in before I even started. That voice inside said it wouldn’t work. Starting now feels wrong - like everyone else already knows the rules.

+ Still, I went ahead. The orange button was pressed by me. Errors happened along the way. Lessons came from those. Growth followed after.

+ This time, I’ve put thoughts into words - maybe they’ll smooth your path more than my own ever did.

+ Just keep going. Each move forward counts.

Funny how a beep can mean so much - tell me once that morning alert goes off. Sharing those quiet wins matters, even from afar.

**Peter Mwai Kamau**-
Cloud learner- always starting over- _NEGU- Never Ever Give Up!_
