- Now, in normal client-server communication, there are a series of requests followed by responses. The idea behind an SMB Relay attack is to position yourself between the client and the server in order to capture the data packets transmitted between the two entities.

## What is SMB relay attack?
A SMB relay attack is where an attacker captures a users NTLM hash and relays its to another machine on the network. Masquerading as the user and authenticating against SMB to gain shell or file access.

## Prerequisites
- SMB Signing disabled on target
- Must be on the local network
- User credentials must have remote login access for example; local admin to the target machine or member of the Domain Administrators group.

## SMB Signing
What it does?
SMB signing verifies the origin and authenticity of SMB packets. Effectively this stops MITM SMB relay attacks from happening. If this is enabled and required on a machine we will not be able to perform a SMB relay attack.

## For simple terms refer below info:
   ![[AD_in_SMB_relay1.png]]

## Pre-requisite --> [LLMNR poisoning]
- With LLMNR poisoning we are able to capture password hash

![[SMB_relay_attack7.png]]

