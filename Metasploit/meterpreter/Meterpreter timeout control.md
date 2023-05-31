## Displaying the current timeout configuration:
```python
meterpreter > get_timeouts
Session Expiry  : @ 2023-03-24 11:53:15
Comm Timeout    : 300 seconds
Retry Total Time: 3600 seconds
Retry Wait Time : 10 seconds
```
#### 1.)Session Expiry:
- This refers to the time when a session will expire.
- In this case, the session will expire on November 19, 2017, at 5:59:46 AM. After this time, the user will need to log in again to continue using the service.
- Let's say you log into an online banking website at 2:00 PM and the session expiry is set to 1 hour. This means that you have until 3:00 PM to complete any transactions or view any information on the website. If you try to access the website after 3:00 PM, you will be prompted to log in again.

#### 2.)Comm Timeout:
- This is the amount of time the system will wait for a response from a communication partner before timing out. 
- In this case, the timeout is set to 300 seconds, which means that if the system does not receive a response within 300 seconds, it will consider the communication to have failed.
- Imagine you are using a chat application and you send a message to a friend. The comm timeout is set to 30 seconds, but your friend's internet connection is slow, so it takes them 45 seconds to respond. Since the response took longer time than the conn timeout, the chat application will consider the communication to have failed and may prompt you to try sending the message again.

#### 3.)Retry Total time:
- This is the total amount of time the system will attempt to retry a communication before giving up. 
- In this case, the total retry time is set to 3600 seconds or 1 hour.
- Suppose you are trying to download a large file from a website, but the download keeps failing due to poor internet connection. The website is set to retry the download for up to 1 hour, so it will continue to try to download the file for up to 1 hour before giving up.

#### 4.)Retry Wait Time:
- This is the amount of time the system will wait before attempting to retry a failed communication. 
- In this case, the wait time is set to 10 seconds, which means that the system will wait 10 seconds before attempting to retry the communication after a failure.

## Changing the current timeout configurations:
```python
meterpreter > set_timeouts -c 600
Session Expiry  : @ 2023-03-24 11:53:14
Comm Timeout    : 600 seconds
Retry Total Time: 3600 seconds
Retry Wait Time : 10 seconds
```
- To change the `Conn Timeout`, we can use the -c flag followed by the time in seconds.