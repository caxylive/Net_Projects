# Why VLANs Exist

Why VLANs were invented:
- Switches used to connect everyone in one big flat network → chaos: too much broadcast, poor security, no segmentation.

- VLANs = virtual walls inside a switch. They separate groups logically (Finance, HR, IT, Guests).

Learning Goal:

- Understand what a broadcast domain is

- What happens when no VLANs are configured

- How VLANs isolate traffic

- Why routing is needed to let them talk

🧠 Goal: by the end of this section, you’ll be able to explain VLANs to someone else — without touching a command yet.itches used to connect everyone in one big flat network

## Key Components

The parts that are involved:

- Access ports → where PCs connect (belong to one VLAN)

- Trunk ports → where switches connect (carry multiple VLANs)

- Native VLAN → default VLAN on a trunk

- VLAN IDs → numbers like 10, 20, 100 that represent logical groups

We’ll visualize this with ASCII diagrams (so you see the topology).

## Hands-On Practice (Base VLAN Configuration)

