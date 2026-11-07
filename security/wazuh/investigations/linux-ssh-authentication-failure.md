# Lab 02: Linux SSH Authentication Failure Detection with Wazuh

## Objective

Demonstrate how Wazuh SIEM detects and analyzes failed SSH authentication attempts against a Linux server.

This lab was performed in my personal cybersecurity homelab using an Ubuntu Server endpoint monitored by a containerized Wazuh deployment.

## Lab Environment

| Component | Configuration |
|---|---|
| SIEM | Wazuh 4.14.8 |
| SIEM Host | Ubuntu Server 24.04 |
| Deployment | Docker Compose |
| Endpoint | Ubuntu Server |
| Wazuh Agent | ubuntu-homelab |
| Event Source | OpenSSH authentication logs |
| Target Service | SSH (TCP/22) |
| Test Source IP | 192.168.4.33 |

## Step 1: Verify SSH Log Collection

Confirmed that the Ubuntu Server was recording SSH authentication events.

Using the Ubuntu terminal, I executed:

```bash
sudo journalctl -u ssh --since "10 minutes ago" --no-pager
```

The command displayed SSH service activity, including authentication failures and successful connections.

The SSH service was listening on port 22.

## Step 2: Generate Controlled Authentication Failures

During the controlled test, SSH login attempts were made using a nonexistent Linux username.

The server recorded failed password attempts associated with the invalid account.

The authentication logs also showed that the connection was closed after the failed attempts.

A successful authentication to a valid Linux account was subsequently recorded from the same source IP address.

## Step 3: Verify the Linux Authentication Events

Reviewed the SSH service logs using:

```bash
sudo journalctl -u ssh --no-pager
```

The logs contained entries similar to:

```text
Invalid user [test-user] from 192.168.4.33
pam_unix(sshd:auth): authentication failure
Failed password for invalid user [test-user]
Connection reset by invalid user [test-user]
Accepted password for [valid-user]
```

The output confirmed that Ubuntu recorded the authentication attempts.

Two failed password entries were visible in the reviewed log excerpt.

## Step 4: Locate the Alert in Wazuh

Opened the Wazuh Dashboard and navigated to:

**Threat Hunting → Events**

Filtered the results by:

- Agent: `ubuntu-homelab`
- Event source: `sshd`
- Time range: November 7, 2026

Wazuh successfully displayed an SSH authentication alert associated with the invalid login attempt.

## Step 5: Analyze the Security Alert

The following information was collected from the Wazuh alert:

| Field | Observed Value | Interpretation |
|---|---|---|
| Rule ID | 5710 | SSH invalid-user detection |
| Rule Description | sshd: Attempt to login using a non-existent user | Invalid username authentication attempt |
| Rule Level | 5 | Low-severity alert |
| Source IP | 192.168.4.33 | Origin of the authentication attempt |
| Service | sshd | OpenSSH server |
| Rule Groups | syslog, sshd, authentication_failed, invalid_login | Authentication-related detection |
| MITRE ATT&CK | T1110.001 | Password Guessing |
| MITRE ATT&CK | T1021.004 | Remote Services: SSH |
| Agent | ubuntu-homelab | Monitored Ubuntu endpoint |

### Key Findings

**Invalid Username:** The authentication attempt targeted a Linux account that did not exist.

**Source IP Correlation:** The IP address `192.168.4.33` appeared in both the Ubuntu SSH logs and the Wazuh alert.

**Rule 5710:** Wazuh identified the authentication event as an attempt to log in using a nonexistent user.

**Rule Level 5:** Wazuh classified the event as a low-severity security alert.

**MITRE ATT&CK T1110.001:** The alert was mapped to password guessing. This mapping does not independently establish a sustained brute-force attack.

## Step 6: Security Assessment

The authentication failures occurred during a controlled homelab test.

The observed activity was expected and did not independently indicate malicious behavior.

In a real security investigation, additional context would be necessary, including:

- Number and frequency of failed SSH attempts
- Source IP reputation and network location
- Usernames targeted during authentication
- Successful logins following failed attempts
- Authentication attempts across multiple accounts
- Other suspicious activity on the endpoint

The successful login recorded from the same IP address was part of the observed authentication sequence. It does not, by itself, establish unauthorized access.

## Results

**Detection successful.**

- Ubuntu recorded the failed SSH authentication attempts.
- The Wazuh SIEM generated a level 5 alert.
- Wazuh rule 5710 identified the invalid-user attempt.
- The source IP matched the original Ubuntu authentication logs.
- The alert was searchable in the Wazuh Dashboard.
- The alert included MITRE ATT&CK mappings.

## Skills Demonstrated

- Linux security log analysis
- SSH authentication monitoring
- SIEM event investigation
- Wazuh Threat Hunting
- Authentication failure detection
- Source IP correlation
- MITRE ATT&CK mapping
- Security incident documentation

## Future Improvements

- Investigate repeated SSH authentication failures.
- Explore Wazuh correlation rules for multiple failed logins.
- Configure SSH authentication alert dashboards.
- Evaluate SSH key-based authentication and access restrictions.
- Test additional Linux security detection scenarios.

## Detection Evidence

The Wazuh SIEM successfully detected an SSH authentication attempt against a nonexistent Linux account.

### Alert Details

| Field | Value |
|---|---|
| Endpoint | ubuntu-homelab |
| Source IP | 192.168.4.33 |
| Service | SSH |
| Wazuh Rule ID | 5710 |
| Alert Level | 5 |
| Description | sshd: Attempt to login using a non-existent user |
| Detection Date | November 7, 2026 |

### Wazuh Alert Screenshot

![Linux SSH Authentication Failure Detection](linux-ssh-alert.png)

### Security Analysis

The SSH authentication logs showed that a nonexistent Linux account was used during an attempted login.

Wazuh detected the event using rule 5710 and generated a level 5 alert.

The source IP address was consistent between the original Ubuntu logs and the Wazuh event.

This confirms that the homelab can collect and analyze Linux authentication activity.

An invalid login attempt alone does not prove malicious activity. Repeated failures, unexpected sources, or suspicious authentication patterns would warrant additional investigation.

## Investigation Summary

### Initial Detection

Wazuh generated a level 5 alert after detecting an SSH login attempt using a nonexistent Linux account.

### Investigation Findings

- Affected endpoint: ubuntu-homelab
- Source IP: 192.168.4.33
- Detection rule: 5710
- Event category: SSH authentication failure
- Alert severity: Level 5
- Activity source: Controlled homelab test

### Assessment

The authentication failures were generated during authorized testing.

The alert confirms that Linux authentication activity is visible within the Wazuh SIEM.

### Conclusion

**Classification:** Authorized security testing

**Outcome:** Detection validated; no confirmed compromise.

The observed events were expected during the controlled test. No evidence from the reviewed alerts alone establishes unauthorized access.

### Recommended Follow-Up

Monitor repeated SSH authentication failures, unfamiliar source IP addresses, unusual login times, and successful authentication events following multiple failures.
