````md
# Day 4 – CLI Basics & Configuration (CCNA 200-301)

---

## 1. Console Port and CLI Access

Network devices such as **routers and switches** are managed using a **Command Line Interface (CLI)**.

- The CLI allows administrators to:
  - Configure the device
  - Monitor its status
  - Troubleshoot issues
- The CLI is accessed through the **console port**, especially during:
  - Initial setup
  - Password recovery
  - When the network is down (out-of-band management)

![Console Port or CLI](./images/Console%20Port%20or%20CLI.png)

---

## 2. Rollover Cable

A **rollover cable** is used to connect a PC to a network device’s **console port**.

- Also called a **console cable**
- Pin layout is reversed (pin 1 ↔ pin 8)
- Not used for data traffic
- Used only for device management

![Rollover cable](./images/Rollover%20cable.png)

---

## 3. CLI Modes Overview

Cisco IOS uses different **modes** to separate user access and configuration levels.

| Prompt | Mode | Description |
|------|------|------------|
| `Router>` | User EXEC | Limited monitoring |
| `Router#` | Privileged EXEC | Full monitoring, access to config |
| `Router(config)#` | Global Configuration | Device configuration |

---

## 4. User EXEC Mode

- Default mode when you first access the device
- Very limited commands
- Used mainly to:
  - Test connectivity
  - View basic status

Prompt:
```text
Router>
````

---

## 5. Privileged EXEC Mode

Entered from User EXEC mode using:

```text
Router> enable
```

Prompt changes to:

```text
Router#
```

### Capabilities

* View full configuration
* Reload the device
* Save configuration
* Enter configuration modes

This mode is usually **password protected**.

---

## 6. Global Configuration Mode

Entered from Privileged EXEC mode using:

```text
Router# configure terminal
```

or

```text
Router# conf t
```

Prompt:

```text
Router(config)#
```

### Purpose

* Configure system-wide settings
* Configure passwords, interfaces, routing, etc.

---

## 7. Enable Password

Used to protect access to **Privileged EXEC mode**.

```text
Router(config)# enable password CCNA
```

### Characteristics

* Stored in **clear text** by default
* Case-sensitive
* Weak security
* Can be encrypted using `service password-encryption`

---

## 8. Enable Secret (Recommended)

```text
Router(config)# enable secret Cisco
```

### Key Points

* Always encrypted
* Uses **Type 5 (MD5) hashing**
* More secure than enable password
* If both are configured, **enable secret is used**

---

## 9. Service Password Encryption

```text
Router(config)# service password-encryption
```

### Effects

* Encrypts:

  * Existing passwords
  * Future passwords
* Uses **Type 7 encryption**
* Does **NOT** affect enable secret

⚠️ Type 7 encryption is **reversible** and should not be considered secure.

---

## 10. Disabling Service Password Encryption

```text
Router(config)# no service password-encryption
```

* Already encrypted passwords remain encrypted
* New passwords are stored in clear text
* Enable secret is unaffected

---

## 11. Canceling (Removing) Commands

Cisco IOS uses the `no` keyword to remove configurations.

```text
Router(config)# no service password-encryption
```

General format:

```text
Router(config)# no <command>
```

---

## 12. Running vs Startup Configuration

### Running Configuration

* Active configuration
* Stored in **RAM**
* Lost on reboot

```text
Router# show running-config
```

---

### Startup Configuration

* Saved configuration
* Stored in **NVRAM**
* Loaded when the device restarts

```text
Router# show startup-config
```

---

## 13. Saving the Configuration

To prevent configuration loss after reboot:

```text
Router# write
```

or

```text
Router# write memory
```

or

```text
Router# copy running-config startup-config
```

All commands perform the **same function**.

---

## 14. Executing EXEC Commands from Config Mode

```text
Router(config)# do show running-config
```

* Allows EXEC-level commands without exiting configuration mode

---

## 15. Modes Review

| Prompt            | Mode                 |
| ----------------- | -------------------- |
| `Router>`         | User EXEC            |
| `Router#`         | Privileged EXEC      |
| `Router(config)#` | Global Configuration |

---

## 16. Command Review

```text
enable
```

→ Enter Privileged EXEC mode

```text
configure terminal
```

→ Enter Global Configuration mode

```text
enable password <password>
```

→ Set basic enable password

```text
enable secret <password>
```

→ Set secure enable password

```text
service password-encryption
```

→ Encrypt passwords (Type 7)

```text
no <command>
```

→ Remove a configuration

```text
show running-config
```

→ View active configuration

```text
show startup-config
```

→ View saved configuration

```text
write / copy running-config startup-config
```

→ Save configuration

---

## 17. Final Review

* Console port provides **out-of-band access**
* Rollover cable is required for console access
* CLI modes control access and permissions
* Always prefer **enable secret** over enable password
* Configurations must be saved to survive reboot

---

✅ **End of Day 4 – CLI Basics**

```
```
