# ubuntu-service-troubleshooting-lab
Working to enhance my Linux troubleshooting skills.
# Ubuntu Service Troubleshooting Lab

This repository documents a hands-on Ubuntu lab I built to practice Linux troubleshooting in scenarios similar to real support and operations work.

The lab focuses on core areas that come up often in Linux and open source environments:

- systemd service dependencies
- DNS resolution failures
- service bind/address issues
- host firewall blocking
- application-to-database connectivity testing

I built and tested these scenarios on Ubuntu VMs, using common Linux tools to diagnose issues and verify fixes.

## Goals

The purpose of this lab is to practice a structured troubleshooting approach:

1. verify the symptom
2. isolate the failing layer
3. identify root cause
4. apply a fix
5. confirm resolution

## Tools used

- `systemctl`
- `journalctl`
- `ss`
- `curl`
- `resolvectl`
- `ufw`
- `nc` / netcat
- `ping`
- `ip addr`
- `ip route`

## Scenarios

- [01 - systemd dependency behavior](scenarios/01-systemd-dependency.md)
- [02 - DNS resolution failure](scenarios/02-dns-resolution-failure.md)
- [03 - bind address issue](scenarios/03-bind-address-issue.md)
- [04 - firewall blocking service access](scenarios/04-firewall-blocking-service.md)
- [05 - application to database connectivity](scenarios/05-app-to-db-connectivity.md)

## Environment

- Ubuntu VMs
- Two-node lab for client/server testing
- UFW enabled for firewall scenarios

## What I learned

- Successful local testing does not always confirm external reachability.
- DNS failures can appear at first like total network failure.
- A running service may still be unavailable if it is bound only to localhost.
- Verifying service state, socket state, routing, and firewall policy separately is important for finding root cause quickly.
- Cross-host validation is more reliable than testing only from the affected server.

## Notes

This repo is meant to show my troubleshooting process, not just final commands. I want each scenario to be reproducible and explainable end to end.
