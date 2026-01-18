# Vulnerabilty-Management-Program

In this project, we simulate the implementation of a comprehensive vulnerability management program, from inception to completion.

_**Inception State:**_ the organization has no existing policy or vulnerability management practices in place.

_**Completion State:**_ a formal policy is enacted, stakeholder buy-in is secured, and a full cycle of organization-wide vulnerability remediation is successfully completed.

---

<img width="1000" alt="image" src="https://github.com/user-attachments/assets/cfc5dbcf-3fcb-4a71-9c13-2a49f8bab3e6">

# Technology Utilized
- Tenable (enterprise vulnerability management platform)
- Azure Virtual Machines (Nessus scan engine + scan targets)
- PowerShell & BASH (remediation scripts)

---


# Table of Contents

- [Vulnerability Management Policy Draft Creation](#vulnerability-management-policy-draft-creation)
- [Mock Meeting: Policy Buy-In (Stakeholders)](#step-2-mock-meeting-policy-buy-in-stakeholders)
- [Policy Finalization and Senior Leadership Sign-Off](#step-3-policy-finalization-and-senior-leadership-sign-off)
- [Mock Meeting: Initial Scan Permission (Server Team)](#step-4-mock-meeting-initial-scan-permission-server-team)
- [Initial Scan of Server Team Assets](#step-5-initial-scan-of-server-team-assets)
- [Vulnerability Assessment and Prioritization](#step-6-vulnerability-assessment-and-prioritization)
- [Distributing Remediations to Remediation Teams](#step-7-distributing-remediations-to-remediation-teams)
- [Mock Meeting: Post-Initial Discovery Scan (Server Team)](#step-8-mock-meeting-post-initial-discovery-scan-server-team)
- [Mock CAB Meeting: Implementing Remediations](#step-9-mock-cab-meeting-implementing-remediations)
- [Remediation Round 1: Outdated Wireshark Removal](#remediation-round-1-outdated-wireshark-removal)
- [Remediation Round 2: Insecure Protocols & Ciphers](#remediation-round-2-insecure-protocols--ciphers)
- [Remediation Round 3: Guest Account Group Membership](#remediation-round-3-guest-account-group-membership)
- [Remediation Round 4: Windows OS Updates](#remediation-round-4-windows-os-updates)
- [First Cycle Remediation Effort Summary](#first-cycle-remediation-effort-summary)

---

### Vulnerability Management Policy Draft Creation

This phase focuses on drafting a Vulnerability Management Policy as a starting point for stakeholder engagement. The initial draft outlines scope, responsibilities, and remediation timelines, and may be adjusted based on feedback from relevant departments to ensure practical implementation before final approval by upper management.  
[Draft Policy](https://docs.google.com/document/d/1VV2mMPlssL418bRR9Jw179rKej5fFEKZgVF30G_UGmg/edit?tab=t.0)

---

### Step 2) Mock Meeting: Policy Buy-In (Stakeholders)

In this phase, a meeting with the server team introduces the draft Vulnerability Management Policy and assesses their capability to meet remediation timelines. Feedback leads to adjustments, like extending the critical remediation window from 48 hours to one week, ensuring collaborative implementation.

**Policy Remediation Timeline Discussion**

**Emanuel:**  
Hey, good morning, Jimmy. How’s everything been lately? I know everyone’s been pretty busy these last few weeks.

**Jimmy:**  
Good morning, Emanuel. Yeah, it’s been a bit hectic, but we’re hanging in there. Thanks for asking. I had a chance to read through the policy draft, and overall it makes sense. However, with our current staffing, we can’t realistically meet the aggressive remediation timelines—especially the 48-hour window for critical vulnerabilities.

**Emanuel:**  
I totally understand. That timeline *is* pretty aggressive, especially to start. Maybe we can extend the remediation window for critical vulnerabilities to one week as a compromise. Then we can reserve the 48-hour window for truly severe cases, like zero-day vulnerabilities.

**Jimmy:**  
That sounds reasonable. We really appreciate the flexibility. Would it be possible to have some leeway in the beginning while we get used to the remediation and patching process—maybe for the first few months?

**Emanuel:**  
Absolutely. Once the policy is finalized, we’ll officially launch the program, but we’re planning to give all departments about six months to adjust and get comfortable with the new process. Does that sound fair?

**Jimmy:**  
Yes, that sounds fair. Thanks, Josh. We’ll do our best. I really appreciate you including us in the decision-making process—it helps us feel like we’re part of the solution.

**Emanuel:**  
Of course. We’re all in this together. Thanks for working with us.

**Jimmy:**  
No problem. Thanks for the short meeting.

**Emanuel:**  
Those are my favorite kind.

**Jimmy:**  
Bye for now.

**Emanuel:**  
See you later.

---

### Step 3) Policy Finalization and Senior Leadership Sign-Off

After gathering feedback from the server team, the policy is revised, addressing aggressive remediation timelines. With final approval from upper management, the policy now guides the program, ensuring compliance and reference for pushback resolution.  
[Finalized Policy](https://docs.google.com/document/d/1Eeum0_ypjv9Zr3gVo4zX3Olz1kbpR333-bslWKD187k/edit?tab=t.0)
<div style="text-align: center;">
    <img src="https://github.com/user-attachments/assets/9afcdbc1-0493-4af2-9287-1cb9b8f59b40" alt="image" width="400">
</div>

---

### Step 4) Mock Meeting: Initial Scan Permission (Server Team)

The team collaborates with the server team to initiate scheduled credential scans. A compromise is reached to scan a single server first, monitoring resource impact, and using just-in-time Active Directory credentials for secure, controlled access.  

**Vulnerability Scanning Kickoff Discussion**

**Emanuel:**  
Morning, Jimmy.

**Jimmy:**  
Good morning. I heard you’re ready to start conducting some scans.

**Emanuel:**  
Yep. Now that our vulnerability management policy is in place, I wanted to get started with scheduled credentialed scans of your environment.

**Jimmy:**  
Sounds good to me. What’s involved, and how can we help?

**Emanuel:**  
We’re planning to schedule weekly scans of the server infrastructure. We estimate it’ll take about 4–6 hours to scan all 200 assets. We’ll need you to provide administrative credentials that allow the scan engine to remotely log into the targets so it can perform a more thorough assessment.

**Jimmy:**  
Whoa—hold on. What exactly does the scanning entail? I’m a bit concerned about resource utilization. Also, providing admin credentials to 200 machines doesn’t sound very safe.

**Emanuel:**  
Those are valid concerns. The scan engine sends specific traffic to the servers to check for the presence of known vulnerabilities. This includes inspecting registry settings, identifying outdated software, and checking for insecure protocols or cipher suites. That’s why credentials are required—it allows for deeper, more accurate assessment.

**Jimmy:**  
I see. As long as it doesn’t bring the servers offline, I think we should be okay.

**Emanuel:**  
Absolutely. To be safe, let’s start by scanning a single server and closely monitor resource utilization.

**Jimmy:**  
That’s not a bad idea.

**Emanuel:**  
Great. Regarding credentials, could you set up a dedicated Active Directory account for us? You can leave it disabled until we’re ready to run the scan, enable it during the scan window, and then disable or deprovision it afterward—similar to a just-in-time access approach.

**Jimmy:**  
That sounds good. I’ll ask Susan to get started on automating the account provisioning.

**Emanuel:**  
Awesome. Let’s touch base soon.

**Jimmy:**  
Sounds good. I’ll get back to you once the credentials are set up.

**Emanuel:**  
See you later.

**Jimmy:**  
See you later.

---

### Step 5) Initial Scan of Server Team Assets

In this phase, an insecure Windows Server is provisioned to simulate the server team's environment. After creating vulnerabilities, an authenticated scan is performed, and the results are exported for future remediation steps.  

<img width="635" alt="image" src="https://github.com/user-attachments/assets/937cccbd-36bb-4445-97b9-e915085cda81" style="border: 2px solid black;">

[Scan 1 - Initial Scan](https://drive.google.com/file/d/1RBPVj_azKJMwmRZ8QILlb4hxIjQU3wQ7/view?usp=drive_link)




---

### Step 6) Vulnerability Assessment and Prioritization

We assessed vulnerabilities and established a remediation prioritization strategy based on ease of remediation and impact. The following priorities were set:

1. Third Party Software Removal (Wireshark)
2. Windows OS Secure Configuration (Protocols & Ciphers)
3. Windows OS Secure Configuration (Guest Account Group Membership)
4. Windows OS Updates

---

### Step 7) Distributing Remediations to Remediation Teams

The server team received remediation scripts and scan reports to address key vulnerabilities. This streamlined their efforts and prepared them for a follow-up review.  

<img width="635" alt="image" src="https://github.com/user-attachments/assets/bbf9478f-e1d1-4898-846e-b510ec8c6f72">

[Remediation Email](https://github.com/joshmadakor1/lognpacific-public/blob/main/misc/remediation-email.md)

---

### Step 8) Mock Meeting: Post-Initial Discovery Scan (Server Team)

The server team reviewed vulnerability scan results, identifying outdated software, insecure accounts, and deprecated protocols. The remediation packages were prepared for submission to the Change Control Board (CAB). 

**Vulnerability Scan Results Review**

**Emanuel:**  
Morning, Jimmy. How are you doing?

**Jimmy:**  
Not bad for a Monday. How about yourself?

**Emanuel:**  
Still alive, so I can’t complain. Before we get into the vulnerabilities, how did the scan go on your end? Did you notice any outages, overutilization, or other issues?

**Jimmy:**  
The scan went well. We monitored everything closely, and aside from the increased number of open connections, we wouldn’t have known a scan was taking place.

**Emanuel:**  
That’s good news—and about what I expected. We’ll continue monitoring going forward, but I don’t anticipate any resource utilization issues. Do you mind if I dive into the vulnerability findings?

**Jimmy:**  
Yeah, absolutely.

**Emanuel:**  
Great. I’m going to share my screen really quick.  
The majority of the findings are related to Wireshark being installed. As you can see, there are multiple instances, and it’s simply very out of date.

One interesting finding is that the local **Guest** account on the servers belongs to a group. After looking deeper, it turns out it’s a member of the local **Administrators** group, which is unexpected.

Some of the other findings—like the Microsoft Edge (Chromium) vulnerabilities—may be automatically resolved through Windows Updates. I’m not entirely sure about a couple of these yet, but they may also be addressed that way. We don’t need to worry about the self-signed certificate finding, since it’s just the system’s own certificate.

However, the medium-strength cipher suites and TLS 1.0 and 1.1 findings are more important. These are deprecated cipher suites and protocols, and I think we should plan to remediate them.

So overall, we’re looking at:
- Removing outdated Wireshark installations  
- Disabling deprecated protocols and cipher suites  
- Removing the Guest account from the local Administrators group

**Jimmy:**  
Very interesting. The good news is I suspect most of our servers will have the same vulnerabilities. Hopefully that makes remediation easier.

**Emanuel:**  
That’s actually good news—having a uniform server configuration usually makes remediation much smoother. Do you foresee any issues remediating any of these items, particularly the cipher suites or insecure protocols?

**Jimmy:**  
I highly doubt there will be any issues. We’ll run the changes through the next Change Control Board. Uninstalling Wireshark and fixing the Guest account shouldn’t be a problem—those shouldn’t be on the servers in the first place. I’ll need to talk with our CIS admins about it.

**Emanuel:**  
That’s great to hear. I’ll go ahead and start building remediation packages to make things easier when it’s time to implement the fixes.

**Jimmy:**  
That sounds great.

**Emanuel:**  
One quick question—do you already have something in place to address Windows Update–related vulnerabilities? Is patch management already configured?

**Jimmy:**  
Yes, that’s already handled. Windows Updates should resolve those automatically by next week. We have patch management in place.

**Emanuel:**  
Excellent. I’ll start researching the best way to remediate the remaining findings and get back to you before the next Change Control Board.

**Jimmy:**  
Sounds good. Talk to you soon.

**Emanuel:**  
Talk to you soon.

---

### Step 9) Mock CAB Meeting: Implementing Remediations

The Change Control Board (CAB) reviewed and approved the plan to remove insecure protocols and cipher suites. The plan included a rollback script and a tiered deployment approach.  

**Change Advisory Board (CAB) – Vulnerability Remediation Review**

**Chair:**  
Next up on the agenda are two vulnerability remediation items for the server team:
1. Removal of insecure protocols  
2. Removal of insecure cipher suites  

It looks like Emanuel from the Risk Department is working in conjunction with Jimmy from Infrastructure on this effort. Jimmy, would you like to walk us through the technical aspects of the changes being implemented?

**Jimmy:**  
Normally I would, but do you mind if Emanuel takes this one? He actually built the solution for us, and we’re still getting used to the new process.

**Emanuel:**  
Sure, I can explain.  
Insecure cipher suites and protocols simply mean the system is capable of negotiating and using algorithms or protocols that have been deprecated. If a system connects to another server that only supports those deprecated protocols, it’s possible the system could fall back and use them.

These settings are controlled through the Windows registry. The remediation itself is straightforward—we developed a PowerShell script that:
- Disables all insecure protocols and cipher suites  
- Enables only modern, standardized, and secure protocols and cipher suites  

Overall, it’s a very simple and controlled change.

**CAB Member:**  
That sounds good, but what happens if something goes wrong? Do we have a rollback plan in place?

**Emanuel:**  
Yes, absolutely. We’ve accounted for that in a few ways.  
First, we’re using a tiered deployment approach:
- Pilot group (small subset of systems)  
- Pre-production  
- Production  

Additionally, we’ve built fully automated rollback scripts for each remediation. If any unexpected issues arise, the rollback script will restore the original protocol and cipher settings.

**CAB Member:**  
That sounds reasonable. Since these are just registry changes, I’m not too concerned.

**Emanuel:**  
Exactly. That’s correct.

**Chair:**  
Any additional questions from anyone?

*(No further questions)*

**Chair:**  
Great. That wraps things up for this week’s CAB meeting. See you all next week.

**Group:**  
See you later.

---
### Step 10 ) Remediation Effort

#### Remediation Round 1: Outdated Wireshark Removal

The server team used a PowerShell script to remove outdated Wireshark. A follow-up scan confirmed successful remediation.  
[Wireshark Removal Script](https://github.com/joshmadakor1/lognpacific-public/blob/main/automation/remediation-wireshark-uninstall.ps1)  

<img width="634" alt="image" src="https://github.com/user-attachments/assets/7b4f9ab2-d230-4458-ac0f-c0ff070ae79a">

[Scan 2 - Third Party Software Removal](https://drive.google.com/file/d/1UiwPPTtuSZKk02hiMyXf31pXUIeC5EWt/view?usp=drive_link)


#### Remediation Round 2: Insecure Protocols & Ciphers

The server team used PowerShell scripts to remediate insecure protocols and cipher suites. A follow-up scan verified successful remediation, and the results were saved for reference.  
[PowerShell: Insecure Protocols Remediation](https://github.com/joshmadakor1/lognpacific-public/blob/main/automation/toggle-protocols.ps1)
[PowerShell: Insecure Ciphers Remediation](https://github.com/joshmadakor1/lognpacific-public/blob/main/automation/toggle-cipher-suites.ps1)

<img width="630" alt="image" src="https://github.com/user-attachments/assets/0e96120d-8ec9-4f76-8e42-79c752200010">

[Scan 3 - Ciphersuites and Protocols](https://drive.google.com/file/d/1Qc6-ezQvwReCGUZNtnva0kCZo_-zW-Sm/view?usp=drive_link)


#### Remediation Round 3: Guest Account Group Membership

The server team removed the guest account from the administrator group. A new scan confirmed remediation, and the results were exported for comparison.  
[PowerShell: Guest Account Group Membership Remediation](https://github.com/joshmadakor1/lognpacific-public/blob/main/automation/toggle-guest-local-administrators.ps1)  

<img width="627" alt="image" src="https://github.com/user-attachments/assets/870a3eac-3398-44fe-91c0-96f3c2578df4">

[Scan 4 - Guest Account Group Removal](https://drive.google.com/file/d/1jVgikjfrV1YjOcL3QRT_oUB0Y82w22V7/view?usp=drive_link)


#### Remediation Round 4: Windows OS Updates

Windows updates were re-enabled and applied until the system was fully up to date. A final scan verified the changes  

<img width="627" alt="image" src="https://github.com/user-attachments/assets/870a3eac-3398-44fe-91c0-96f3c2578df4">

[Scan 5 - Post Windows Updates](https://drive.google.com/file/d/1tmDjeHl5uiGitRwWy8kFRi33q-nGi1Zt/view?usp=drive_link)

---

### First Cycle Remediation Effort Summary

The remediation process reduced total vulnerabilities by 80%, from 30 to 6. Critical vulnerabilities were resolved by the second scan (100%), and high vulnerabilities dropped by 90%. Mediums were reduced by 76%. In an actual production environment, asset criticality would further guide future remediation efforts.  

<img width="1920" alt="image" src="https://github.com/user-attachments/assets/51f0aae8-7f36-4d90-b29f-5257e57155f9">

[Remediation Data](https://docs.google.com/spreadsheets/d/1FTtFfZYmFsNLU6pm8nTzsKyKE-d2ftXzX_DPwcnFNfA/edit?gid=0#gid=0)

---

### On-going Vulnerability Management (Maintenance Mode)

After completing the initial remediation cycle, the vulnerability management program transitions into **Maintenance Mode**. This phase ensures that vulnerabilities continue to be managed proactively, keeping systems secure over time. Regular scans, continuous monitoring, and timely remediation are crucial components of this phase. (See [Finalized Policy](https://docs.google.com/document/d/1rvueLX_71pOR8ldN9zVW9r_zLzDQxVsnSUtNar8ftdg/edit?usp=drive_link) for scanning and remediation cadence requirements.)

Key activities in Maintenance Mode include:
- **Scheduled Vulnerability Scans**: Perform regular scans (e.g., weekly or monthly) to detect new vulnerabilities as systems evolve.
- **Patch Management**: Continuously apply security patches and updates, ensuring no critical vulnerabilities remain unpatched.
- **Remediation Follow-ups**: Address newly identified vulnerabilities promptly, prioritizing based on risk and impact.
- **Policy Review and Updates**: Periodically review the Vulnerability Management Policy to ensure it aligns with the latest security best practices and organizational needs.
- **Audit and Compliance**: Conduct internal audits to ensure compliance with the vulnerability management policy and external regulations.
- **Ongoing Communication with Stakeholders**: Maintain open communication with teams responsible for remediation, ensuring efficient coordination.

By maintaining an active vulnerability management process, organizations can stay ahead of emerging threats and ensure long-term security resilience.
