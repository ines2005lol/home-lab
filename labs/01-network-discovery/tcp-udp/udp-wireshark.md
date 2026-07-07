# Netcat UDP Listener Test

## Objective

The purpose of this section is to create a simple UDP service using Netcat and analyze how UDP communication behaves during network scanning.

This lab demonstrates:

* Creating a UDP listener
* Sending UDP data between machines
* Scanning UDP ports using Nmap
* Understanding UDP open and open|filtered states

---

## Lab Environment

| Machine       | Operating System | Role             |
| ------------- | ---------------- | ---------------- |
| Kali Linux VM | Linux            | Scanner / Client |
| Windows VM    | Windows          | UDP Listener     |

Both machines were connected to the same internal network.

---

## What is Netcat?

Netcat (`nc`) is a networking utility used to create network connections and listeners using TCP or UDP.

It can be used for:

* Testing network connectivity
* Creating simple listeners
* Sending and receiving data
* Troubleshooting network services

---

# 1. Creating a UDP Listener

On the Windows machine, a Netcat UDP listener was started on port `9999`.

<img width="307" height="60" alt="image" src="https://github.com/user-attachments/assets/377c6730-a824-4ba9-9dec-540cea7ec38f" />

The terminal remains active because Netcat is waiting for incoming UDP packets.

# 2. Scanning the UDP Port with Nmap

A UDP scan was performed from Kali:

<img width="537" height="177" alt="image" src="https://github.com/user-attachments/assets/10e2035c-ea51-43dc-b033-36f1acda93f3" />

# 3. Wireshark analysis

<img width="1032" height="62" alt="image" src="https://github.com/user-attachments/assets/18bad1ef-14de-4182-9e00-ff8ea7966658" />

Because UDP does not confirm delivery:

* An open UDP port may not send a response.
* Nmap may report `open|filtered` when no reply is received.

<img width="781" height="410" alt="image" src="https://github.com/user-attachments/assets/042d2e60-a07f-4567-8b7d-c8304442ce4c" />

# 4. Sending UDP traffic

From Kali Linux, a UDP connection was created:
<img width="262" height="72" alt="image" src="https://github.com/user-attachments/assets/762086ba-87a6-4875-a6a1-ef3fc0fcb57b" />

Result in Windows:
<img width="657" height="120" alt="image" src="https://github.com/user-attachments/assets/1f32eeb3-fa78-410c-b609-b61ea8e74663" />

Wireshark observation:
<img width="992" height="12" alt="image" src="https://github.com/user-attachments/assets/c6d8b8e4-adfd-4cd5-894e-2dd6412f4799" />
<img width="1547" height="90" alt="image" src="https://github.com/user-attachments/assets/28333eb7-faa2-4bb6-a751-33b628596248" />
-> Netcat does not provide encryption by default. Any data transmitted through a Netcat connection is sent in plaintext.

# 5. Closing the Listener

Stop Netcat using:

```text
CTRL + C
```

After stopping the listener, the UDP service is no longer active.

---

# Observations

* Netcat can create a simple UDP service for testing.
* UDP does not establish a connection before sending data.

---

## Skills Learned

* Created a UDP listener using Netcat.
* Generated and captured UDP traffic.
* Performed UDP reconnaissance using Nmap.
* Analyzed UDP behavior with Wireshark.
