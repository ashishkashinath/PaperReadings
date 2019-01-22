# Mimicry Attacks on Host-Based Instrusion Detection Systems

### Terms
mimicry attacks
IDS, semantic nops, 

### Introduction
IDS is similar to a watchful burglar alarm, an attack should trigger it to bring the attention of the security administrator.

**Challenge** : 
* *Adaptive Adversarial Attacks:* The attackers adapt in response to the defensive measueres deployed. IDS is like a *game of chess* (analogy) that should anticipate the moves the attacker might make and ensure the system remains secure against all the attacker's possible responses.
* Attacks originate from scripts, which the attackers will adapt as the IDS is deployed to routinely evade it.

There are 2 kinds of IDS: Network-based IDS and Host-based IDS. This paper deals with host-based IDS.

Host-based IDS can be classified into two categories: Signature-based schemes and anomaly detection. 

- Signature-based schemes are tyically trivial to bypass by varying the attack ever so slightly similar to polymorphic viruses evading virus checkers.
- Anomaly Detection systems are studied here using the principles of language and automata theory. Conversion of an off-the shelf exploit into one that evades detection is shown.

### Host-based IDS

- The scheme considered here belongs to Forrest et. al.
- The interaction of the application with the underlying OS is observed. Security-based interactions take the form of system calls.
    *   **Learning Phase:** IDS gathers system call schemes from times when the system is not under attack to learn the normal behavior. Extracts the subtraces from these which consists of 6 consecutive system calls, and creates a database of these observed subtraces.

    *   **Monitoring Phase:** Abnormality is measured by counting how many anomlaous subtraces it contains. 
    
* The authors experience is that attacks appear as  *radically abnormal traces*. 
* Somayaji and Forrest's pH intrusion detection system is used as the testcase. 
* The goal is that the techniques developed by the authors can be used not only to System call sequences but also to data mining, neural networks, finite automata, hidden Markov Models, pattern matching and so on.

### Building Blocks for Evasion

Assumptions:
* that the attacker know how the IDS works -- "security by obscurity"
* that the attacker is able to readily obtain an approximate databases on the target host by examining other hosts of the same type.
* The attacker can launch an attack without being detected. Eg., a buffer overflow does not generate new traces, since only the control flow of the program is different. This is a reasonable assumption since most anomaly-based IDS's are used to detect the harmful effects of the penetration and not the penetration event itself.


Strategies/Ideas to avoid detection:
* Slip under the radar: Try not to use system calls. Such attacks are extremely limited.
* Be patient: Wait for a time when the malicious sequence will be accepted by the IDS as normal behavior. This is possible since simulating the IDS is easy. A limitation is that this comes with the assumption that patience will eventually pay off. Another limitation is that, after the malicious sequence has been executed, resuming application may lead to abnormal systel call trace. The attacker can try to default the attack to appear to come from a generic bug such as Blue Screen of Death or Coredump.
* Be patient, but make your own luck: Rather than embedding a trojan horse into the application and crouching, waiting for the right time to execute the malicious sequence, the attacker discard the applucation completely, and simulates the application by looking for the most favourable path of execution. This can be done by offline , precomputed analysis. The **mimicry attacks** involve mimicking the application, but with a malicious twist. Note that the attacker needn't restrict himself to execution of the application alone, he needs to make sure that the traces are accepted by the IDS. This can be done since the computation/simulation is done offline.
* Replace system call parameters: Replace benign parameters with malicious ones.
* Inserting Nops: Even if the original sequence is not accepted by the IDS, some modified sequence with appropriate number of nops embedded might well be accepted without triggering alarms.
* Generate equivalent attacks: Variations on the malicious code sequence. E.g,  Any call to read() is same as mmap() followed by a memory access. E.g, Split the attack into two threads by using fork(), so that the IDS thinks each of the individual exploit sequences is benign. 










