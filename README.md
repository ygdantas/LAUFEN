# LAUFEN

LAUFEN is an engine for automating the computation of security artifacts from safety artifacts
- assets
- damage scenarios
- threat scenarios
- attack paths

LAUFEN has been implemented in DLV, a logic programming language based on the Answer Set Programming paradigm.

## Purpose of this README file

This README file provides instructions (from the user perspective) on how to run LAUFEN.
 
## Setup

The instruction listed in this file have been tested in a Linux operating system (Ubuntu 18.04 desktop 64-bit).

## Files
- *bin/* includes the DLV binaries for Linux, Windows and MacOS
- *example/apollo.dlv* contains the apollo architecture and selected safety elements
- *utils/utils.dlv* contains auxiliary functions
- *m2m/af3.dlv* contains auxiliary functions for the model-2-model transformation from AutoFOCUS3 (AF3) to LAUFEN
- *security/safety2security.dlv* contains the rules for deriving security artifacts from safety artifacts
- *security/outsider_intruder_reachability.dlv* contains the reachability rules (outsider intruder)
- *security/outsider_intruder_attack_paths.dlv* contains the attacker rules (outsider intruder), including the enumeration of attack paths using the minimal path set method
- *security/insider_intruder.dlv* contains the reachability and attacker rules (insider intruder)
- *paper_results/outsider_attack.dlv* contains the attack paths from the outside 
- *paper_results/insider_attack.dlv* contains the attack paths from the inside

You may download the DLV2 binaries at

https://dlv.demacs.unical.it/

## Instructions for running LAUFEN

The commands for running LAUFEN can be found below. The results will be printed out on the console. If the execution time of LAUFEN is required append '--stats=verbosity' to each of the following commands.

### Outsider intruder
The following command runs LAUFEN to enumerate attack paths from the outside (outsider intruder) 

```
./bin/dlv-2.1.1-linux-x86.bin example/apollo.dlv utils/utils.dlv m2m/af3.dlv security/safety2security.dlv security/outsider_intruder_reachability.dlv security/outsider_intruder_attack_paths.dlv --filter=outsider_intruder/1
```

Each attack path consists of a list of ports from hardware units (public interfaces, ECUs, network interfaces). The list shall be read from left to right.
- outsider_intruder([SOURCE_PORT,....,TARGET_PORT]).

The following command prints the information regarding the source of the attack path (i.e., public interface) and the target of the intruder (i.e., the affected topic)
- outsider_intruder_from_to(PUBLIC_INTERFACE,AFFECTED_TOPIC).

```
./bin/dlv-2.1.1-linux-x86.bin example/apollo.dlv utils/utils.dlv m2m/af3.dlv security/safety2security.dlv security/outsider_intruder_reachability.dlv security/outsider_intruder_attack_paths.dlv --filter=outsider_intruder_from_to/2
```

### Insider intruder

The following command runs LAUFEN to enumerate attack paths from the inside (insider intruder) 

```
./bin/dlv-2.1.1-linux-x86.bin example/apollo.dlv utils/utils.dlv m2m/af3.dlv -n 1 security/safety2security.dlv security/insider_intruder.dlv --filter=insider_intruder/3
```
Each attack path consists of three elements:
- insider_intruder(PUBLISHER,SUBSCRIBER,AFFECTED_TOPIC).

