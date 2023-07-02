## Introduction
- All the major brute forcers, create a **TCP handshake** for a single request and send the request to the server, thereby the server waits and shares the response back, as soon as the tool gets the response, it then reads out and the same happens again.
	- However, the handshake consumes a lot of time and the sending & reading phases contain a much latency too, thereby giving a high load on the CPU and consuming a lot of memory reducing the speed to fuzz that.
- the **turbo intruder** is different and as its speed is. It works on an old technology i.e., **HTTP pipelining** which establishes the connection first and shares as many possible requests in one go without worrying about the received responses in order to minimize the latency and server processing time.

**Note** - You can find brute-forcing password wordlists _[10-million-password-list](https://github.com/danielmiessler/SecLists/tree/master/Passwords/Common-Credentials)_ here.

### Brute Forcing the application’s Passwords
1. we’ll capture the login portal’s HTTP Request by setting the username to **bee** and a random password as **12345.**
![[turbo_intruder1.png]]

2. Back into the intercept tab, we’ll **select the payload position** and will then hit right-click in order to share the request to the Turbo Intruder.
By right click on intercept > Extensions > turbo intruder

3. Interface of **turbo intruder**:
![[turbo_intruder2.png]]
- upper part where our **“shared request”** is embedded, other part we got a **“snippet of python code”** aligned.
- However, over into the **Request section**, we can see that our injection point was converted into **“%s”,** representing where the payload will be going to hit.
- at the other section, there is a **drop-down list** with a **python code** displayed, which thus could be modified as per the attack scenario.

3. Overview to drop-down list in turbo intruder:
![[turbo_intruder3.png]]
- The drop-down list contains a number of attacking python scripts, that we could use accordingly whenever we need.
- **examples/basic.py** --> This is the most common script.

## Turbo intruder script:
1. The script within the **first highlighted box** is responsible for the **fuzzing speed** and the **number of connections made** by the turbo intruder. However, it even carries up the **requests made per connection.**
- Over in the **second box** we need to **add the dictionary** manually by specifying its location.
- The **third code snippet** is the most highlighted section as it defines **which request should be displayed** in the output table. Here the code **“if req.status != 404:”** defines that all the requests will get added to the table leaving the once that are having **status code = 404**
![[turbo_intruder4.png]]

2. Now, let’s **inject our dictionary** by defining its path while manipulating the code.
![[turbo_intruder5.png]]
Further, we’ll hit the **Attack button** in order to initiate our fuzzer.

3. Burp turbo intruder analysis:
![[turbo_intruder6.png]]
- You might be wondering like, this needs to be faster than the basic intruder, however, the RPS rate for the Burp Intruder was 23, and it’s just 14.
- This is all due to the default configuration in the python script as the **concurrentConnections** was just **5** and the **Request per Connection** was **100**. 

4. Let’s modify it all and start the attack again, in order to do so hit the **halt** button and configure the same with
        concurrentConnections=20,
        requestperConnetction=200,
![[turbo_intruder7.png]]
- However, during the attack, you could find that the **retries value is going up**, as the fuzzer was initiating. So, is the requests are not hitting?
- No, it is an indication that the connection per request value might be too high for the server to handle, making the attack is less optimal, thus we need to cut it down and reduce it to half.

### Customizing the Python Scripts
We want the table to dump only the **302 Redirection**, we don’t want any **200 OK**, neither **404 Error**
![[turbo_intruder8.png]]

### Fuzz for Multiple Parameters
1. Back into the **Proxy tab** let’s select any parameter and hit a right-click in order to navigate to **turbo intruder**
![[turbo_intruder9.png]]

2. There, over in the request portion, let’s set **“%s”** in order to select the injection points.
![[turbo_intruder10.png]]

3. Time to choose the script, click on the bar to check the drop-down menu, and then select **examples/multipleParameters.py**
![[turbo_intruder11.png]]

4. The python script:
![[turbo_intruder11.png]]

5. Let’s boot the speed by manipulating the **concurrentConnections=20** and **requestperConnetction=200**, we’ll set the dictionaries for the first word and the second word.
![[turbo_intruder13.png]]

6. we hit the **Attack** button:
![[turbo_intruder14.png]]