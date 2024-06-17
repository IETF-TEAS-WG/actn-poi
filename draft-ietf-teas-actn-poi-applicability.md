---
title: >
  Applicability of Abstraction and Control of Traffic Engineered
  Networks (ACTN) to Packet Optical Integration (POI)
abbrev: ACTN POI
category: info

docname: draft-ietf-teas-actn-poi-applicability-latest
submissiontype: IETF  # also: "independent", "editorial", "IAB", or "IRTF"
number:
date:
consensus: true
v: 3
area: "Routing"
workgroup: "Traffic Engineering Architecture and Signaling"
keyword:
 - next generation
 - unicorn
 - sparkling distributed ledger
venue:
  group: "Traffic Engineering Architecture and Signaling"
  type: "Working Group"
  mail: "teas@ietf.org"
  arch: "https://mailarchive.ietf.org/arch/browse/teas/"
  github: "IETF-TEAS-WG/actn-poi"
  latest: "https://IETF-TEAS-WG.github.io/actn-poi/draft-ietf-teas-actn-poi-applicability.html"

author:
  -
    name: Fabio Peruzzini
    org: TIM
    email: fabio.peruzzini@telecomitalia.it
  -
    ins: J-F. Bouquier
    name: Jean-Francois Bouquier
    org: Vodafone
    email: jeff.bouquier@vodafone.com
  -
    name: Italo Busi
    org: Huawei
    email: italo.busi@huawei.com
  -
    name: Daniel King
    org: Old Dog Consulting
    email: daniel@olddog.co.uk
  -
    name: Daniele Ceccarelli
    org: Cisco
    email: daniele.ietf@gmail.com

contributor:
  -
    name: Sergio Belotti
    org: Nokia
    email: sergio.belotti@nokia.com
  -
    name: Gabriele Galimberti
    email: ggalimbe56@gmail.com
  -
    name: TBD
  -
    name: Anton Snitser
    org: Cisco
    email: asnizar@cisco.com
  -
    name: Washington Costa Pereira Correia
    org: TIM Brasil
    email: wcorreia@timbrasil.com.br
  -
    name: Michael Scharf
    org: Hochschule Esslingen - University of Applied Sciences
    email: michael.scharf@hs-esslingen.de
  -
    name: Young Lee
    org: Sung Kyun Kwan University
    email: younglee.tx@gmail.com
  -
    name: Jeff Tantsura
    org: Apstra
    email: jefftant.ietf@gmail.com
  -
    name: Paolo Volpato
    org: Huawei
    email: paolo.volpato@huawei.com
  -
    name: Brent Foster
    org: Cisco
    email: brfoster@cisco.com
  -
    ins: O. Gonzalez de Dios
    name: Oscar Gonzalez de Dios
    org: Telefonica
    email: oscar.gonzalezdedios@telefonica.com

normative:
  ITU-T_G.694.1:
    title: "Spectral grids for WDM applications: DWDM frequency grid"
    author:
      org: International Telecommunication Union
    date: October 2020
    seriesinfo: ITU-T Recommendation G.694.1
    target: https://www.itu.int/rec/T-REC-G.694.1-202010-I
  IEEE_802.1AB:
    title: >
      IEEE Standard for Local and metropolitan area networks -
      Station and Media Access Control Connectivity Discovery
    author:
      org: Institute of Electrical and Electronics Engineers
    date: March 2016
    seriesinfo: IEEE 802.1AB-2016
    target: https://ieeexplore.ieee.org/document/7433915
  IEEE_802.1AX:
    title: "IEEE Standard for Local and metropolitan area networks - Link Aggregation"
    author:
      org: Institute of Electrical and Electronics Engineers
    date: December 2014
    seriesinfo: IEEE 802.1AX-2014
    target: https://ieeexplore.ieee.org/document/7055197

informative:

--- abstract

This document considers the applicability of Abstraction and Control
of TE Networks (ACTN) architecture to Packet Optical Integration
(POI) in the context of IP/MPLS and optical internetworking. It
identifies the YANG data models defined by the IETF to support this
deployment architecture and specific scenarios relevant to Service
Providers.

Existing IETF protocols and data models are identified for each
multi-technology (packet over optical) scenario with a specific focus on
the MPI (Multi-Domain Service Coordinator to Provisioning Network
Controllers Interface)in the ACTN architecture.

--- middle

{: #intro}

# Introduction

The complete automation of the management and control of Service
Providers transport networks (IP/MPLS, optical, and microwave
transport networks) is vital for meeting emerging demand for high-bandwidth use cases, including 5G and fiber connectivity services.
The Abstraction and Control of TE Networks (ACTN) architecture and
interfaces facilitate the automation and operation of complex optical
and IP/MPLS networks through standard interfaces and data models.
This allows a wide range of network services that can be requested by
the upper layers fulfilling almost any kind of service level
requirements from a network perspective (e.g. physical diversity,
latency, bandwidth, topology, etc.)

Packet Optical Integration (POI) is an advanced use case of traffic
engineering. In wide-area networks, a packet network based on the
Internet Protocol (IP), and often Multiprotocol Label Switching
(MPLS) or Segment Routing (SR), is typically realized on top of an
optical transport network that uses Dense Wavelength Division
Multiplexing (DWDM)(and optionally an Optical Transport Network
(OTN)layer).

In many existing network deployments, the packet and the optical
networks are engineered and operated independently. As a result,
there are technical differences between the technologies (e.g.,
routers compared to optical switches) and the corresponding network
engineering and planning methods (e.g., inter-domain peering
optimization in IP, versus dealing with physical impairments in DWDM,
or very different time scales). In addition, customers needs can be
different between a packet and an optical network, and it is not
uncommon to use other vendors in both domains. The operation of these
complex packet and optical networks is often siloed, as these
technology domains require specific skill sets.

The packet/optical network deployment and operation separation are
inefficient for many reasons. First, both capital expenditure (CAPEX)
and operational expenditure (OPEX) could be significantly reduced by
integrating the packet and the optical networks. Second, multi-technology
online topology insight can speed up troubleshooting (e.g., alarm
correlation) and network operation (e.g., coordination of maintenance
events), and multi-technology offline topology inventory can improve
service quality (e.g., detection of diversity constraint violations).
Third, multi-technology traffic engineering can use the available network
capacity more efficiently (e.g., coordination of restoration). In
addition, provisioning workflows can be simplified or automated
across layers (e.g., to achieve bandwidth-on-demand or to perform
activities during maintenance windows).

This document uses packet-based Traffic Engineered (TE) service
examples. These are described as "TE-path" in this document. Unless
otherwise stated, these TE services may be instantiated using RSVP-TE-based or SR-TE-based, forwarding plane mechanisms.

The ACTN framework enables the complete multi-technology and multi-vendor
integration of packet and optical networks through a Multi-Domain
Service Coordinator (MDSC), and packet and optical Provisioning
Network Controllers (PNCs).

This document describes critical scenarios for POI from the packet
service layer perspective and identifies the required coordination
between packet and optical layers to improve POI deployment and
operation. These scenarios focus on multi-domain packet networks
operated as a client of optical networks.

This document analyses the case where the packet networks support
multi-domain TE paths. The optical networks could be either a DWDM
network, an OTN network (without DWDM layer), or a multi-layer
OTN/DWDM network. Furthermore, DWDM networks could be either fixed-grid or flexible-grid.

Multi-technology and multi-domain scenarios, based on the reference
network described in {{reference-network}} and very relevant for Service
Providers, are described in {{discovery}} and {{config}}.

For each scenario, existing IETF protocols and data models,
identified in {{restconf}} and {{yang}}, are analyzed with a particular
focus on the MPI in the ACTN architecture.

For each multi-technology scenario, the document analyzes how to use the
interfaces and data models of the ACTN architecture.

A summary of the gaps identified in this analysis is provided in
{{conclusions}}.

Understanding the level of standardization and the possible gaps will
help assess the feasibility of integration between packet and optical
DWDM domains (and optionally OTN layer) in an end-to-end multi-vendor
service provisioning perspective.

{: #terms}

## Terminology

This document uses the ACTN terminology defined in {{!RFC8453}}.

In addition, this document uses the following terminology.

Customer service:
: The end-to-end service from CE to CE.

Network service:
: The PE to PE configuration, including both the network service
layer (VRFs, RT import/export policies configuration) and the
network transport layer (e.g. RSVP-TE LSPs). This includes the
configuration (on the PE side) of the interface towards the CE
(e.g. VLAN, IP address, routing protocol etc.).

Technology domain:
: shot for "switching technology domain", defined as "region" in {{!RFC5212}}, where the term "region" is applied to (GMPLS) control domains.

PNC Domain:
: part of the network under control of a single PNC instance. It is subject to the capabilities of the PNC which technologies are controlled.

Port:
: The physical entity that transmits and receives physical signals.

Interface:
: A physical or logical entity that transmits and receives traffic.

Link:
: An association between two interfaces that can exchange traffic directly.

Intra-domain link:
: a link between two adjacent nodes that belong to the same PNC domain.

Inter-domain link:
: a link between two adjacent nodes that belong to different PNC domains.

Ethernet link:
: A link between two Ethernet interfaces.

Single-technology Ethernet link:
: An Ethernet link between between two Ethernet interfaces on physically adjacent IP routers.

Multi-technology Ethernet link:
: An Ethernet link between between two Ethernet interfaces on logically adjacent IP routers, which is supported by an underlay tunnel in a different technology domain.

Cross-technology Ethernet link:
: An Ethernet link between an Ethernet interface on an IP router and an Ethernet interface on a physically adjacent optical node.

Inter-domain Ethernet link:
: An Ethernet link between between two Ethernet interfaces on physically adjacent IP routers that belong to different P-PNC domains.

Single-technology intra-domain Ethernet link:
: An Ethernet link between between two Ethernet interfaces on physically adjacent IP routers that belong to the same P-PNC domain.

Multi-technology intra-domainEthernet link:
: An Ethernet link between between two Ethernet interfaces on logically adjacent IP routers that belong tot he same P-PNC domain, which is supported by supported by two cross-technology Ethernet links and an optical tunnel in between.

IP link:
: A link between two IP interfaces.

Single-technology intra-domain IP link:
: An IP link supported by a single-technology intra-domain Ethernet link.

Inter-domain IP link:
: An IP link supported by an inter-domain Ethernet link.

Multi-technology intra-domain IP link:
: An IP link supported a multi-technology intra-domain Ethernet link.

# Reference Network Architecture {#reference-network}

This document analyses several deployment scenarios for Packet and
Optical Integration (POI) in which ACTN hierarchy is deployed to
control a multi-technology and multi-domain network with two optical
domains and two packet domains, as shown in {{fig-ref-network}}:

{::include ./figures/reference-network.md}
{: #fig-ref-network title="Reference Network"}

The ACTN architecture, defined in {{!RFC8453}}, is used to control this
multi-technology and multi-domain network where each Packet PNC (P-PNC) is
responsible for controlling its packet domain and where each Optical
PNC (O-PNC) in the above topology is responsible for controlling its
optical domain. The packet domains controlled by the P-PNCs can be
Autonomous Systems (ASes), defined in {{?RFC1930}}, or IGP areas, within
the same operator network.

The IP routers between the packet domains can be either AS Boundary
Routers (ASBR) or Area Border Router (ABR): in this document, the
generic term Border Router (BR) is used to represent either an ASBR
or an ABR.

The MDSC is responsible for coordinating the whole multi-domain
multi-technology (packet and optical) network. A specific standard
interface (MPI) permits MDSC to interact with the different
Provisioning Network Controller (O/P-PNCs).

The MPI interface presents an abstracted topology to MDSC, hiding
technology-specific aspects of the network and hiding topology
details depending on the policy chosen regarding the level of
abstraction supported. The level of abstraction can be obtained based
on P-PNC and O-PNC configuration parameters (e.g., provide the
potential connectivity between any PE and any BR in a packet
network).

In the reference network of {{fig-ref-network}}, it is assumed that:

- The domain boundaries between the packet and optical domains are
congruent. In other words, one optical domain supports
connectivity between IP routers in one and only one packet domain;

- There are no inter-domain physical links between optical domains.
Inter-domain physical links exist only:

  - between packet domains (i.e., between BRs belonging to
  different packet domains): these links are called inter-domain
  Ethernet or IP links within this document;

  - between packet and optical domains (i.e., between routers and
  optical nodes): these links are called Cross-technology links within
  this document;

  - between customer sites and the packet network (i.e., between
  CE devices and PE routers): these links are called access
  links within this document.

-  All the physical interfaces at inter-domain links are Ethernet
physical interfaces.

Although the new optical technologies (e.g., QSFP-DD ZR 400G) allow
the operators to provide DWDM pluggable interfaces on the IP routers,
the deployment of those pluggable optics is not yet widely adopted.
The reason is that most operators are not yet ready to manage packet
and optical networks in a single unified domain. Therefore, a unified
use case analysis is outside the scope of this document.

This document analyses scenarios where all the multi-technology IP links,
supported by the optical network, are intra-domain (intra-AS/intra-area), such as PE-BR, PE-P, BR-P, P-P IP links. Therefore the inter-domain IP links are always single-technology links supported by Ethernet
physical links.

The analysis of scenarios with multi-technology inter-domain IP links is
outside the scope of this document.

Therefore, if inter-domain links between the optical domains exist,
they would be used to support multi-domain optical services, which
are outside the scope of this document.

The optical nodes within the optical domains can be either:

- WDM nodes, as defined in {{?I-D.ietf-ccamp-optical-impairment-topology-yang}}, with an integrated ROADM functions and with or without integrated optical transponders;

- OTN nodes, with integrated an OTN cross-connect function and with or without integrated ROADM functions or optical transponders.

{: #mdsc-overview}

## Multi-domain Service Coordinator (MDSC) functions

The MDSC in {{fig-ref-network}} is responsible for multi-domain and multi-technology
coordination across multiple packet and optical domains and provides
multi-layer/multi-domain L2/L3 VPN network services requested by an
OSS/Orchestration layer.

From an implementation perspective, the functions associated with
MDSC described in {{!RFC8453}} may be grouped differently.

1. The service- and network-related functions are collapsed into a
single, monolithic implementation, dealing with the end customer
service requests received from the CMI (Customer MDSC Interface)
and adapting the relevant network models. An example is represented
in Figure 2 of {{!RFC8453}}.

1. An implementation can choose to split the service-related and the
network-related functions into different functional entities, as
described in {{?RFC8309}} and in section 4.2 of {{!RFC8453}}. In this
case, MDSC is decomposed into a top-level Service Orchestrator,
interfacing the customer via the CMI, and into a Network
Orchestrator interfacing at the southbound with the PNCs. The
interface between the Service Orchestrator and the Network
Orchestrator is not specified in {{!RFC8453}}.

1. Another implementation can choose to split the MDSC functions
between an "higher-level MDSC" (MDSC-H) responsible for packet and
optical multi-technology coordination, interfacing with one Optical
"lower-level MDSC" (MDSC-L), providing multi-domain coordination
between the O-PNCs and one Packet MDSC-L, providing multi-domain
coordination between the P-PNCs (see for example Figure 9 of
{{!RFC8453}}).

1. Another implementation can also choose to combine the MDSC and the
P-PNC functions.

In the current service provider's network deployments, at the North
Bound of the MDSC, instead of a CNC, typically, there is an
OSS/Orchestration layer. In this case, the MDSC would implement only
the Network Orchestration functions, as in {{?RFC8309}} described in
point 2 above. Therefore, the MDSC deals with the network services
requests received from the OSS/Orchestration layer.

The functionality of the OSS/Orchestration layer and the interface
toward the MDSC are usually operator-specific and outside the scope
of this draft. Therefore, this document assumes that the
OSS/Orchestrator requests the MDSC to set up L2/L3 VPN network
services through mechanisms outside this document's scope.

There are two prominent workflow cases when the MDSC multi-technology
coordination is initiated:

-  Initiated by request from the OSS/Orchestration layer to setup
L2/L3 VPN network services that require multi-layer/multi-domain
coordination;

-  The MDSC initiates them to perform multi-layer/multi-domain
optimizations and/or maintenance activities (e.g. rerouting LSPs
with their associated services when putting a resource, like a
fibre, in maintenance mode during a maintenance window).
Unlike service fulfillment, these workflows are not related to a
network service provisioning request received from
the OSS/Orchestration layer.

The latter workflow cases are outside the scope of this document.

This document analyses the use cases where multi-layer coordination
is triggered by a network service request received from the
OSS/Orchestration layer.

{: #vpn-overview}

### Multi-domain L2/L3 VPN Network Services

{{fig-vpn-topo}} and {{fig-vpn-path}} provide an example of a hub & spoke multi-domain L2/L3 VPN with three PEs where the hub PE (PE13) and one spoke
PE (PE14) are within the same packet domain, and the other spoke PE
(PE23) is within a different packet domain.

{::include ./figures/vpn-topology.md}
{: #fig-vpn-topo title="Multi-domain VPN topology example"}

{::include ./figures/vpn-te-paths.md}
{: #fig-vpn-path title="Multi-domain VPN TE paths example"}

There are many options to implement multi-domain L2/L3 VPNs,
including:

1. BGP-LU ({{?RFC8277}})

1. Inter-domain RSVP-TE

1. Inter-domain SR-TE

This document analyses the inter-domain TE options for which the TE
tunnel model, defined in {{!I-D.ietf-teas-yang-te}}, could be used at the MPI for
intra-domain or inter-domain TE configuration. The analysis of other
options is outside the scope of this draft.

It is also assumed that:

- the bandwidth of each intra-domain TE path is managed by its
respective P-PNC;

- technology-specific mechanisms (in the case of inter-domain SR-TE,
the binding SID) are used for the inter-domain TE path stitching;

- each packet domain in {{fig-vpn-topo}} uses technology-specific local protection mechanisms (such as Fast Reroute (FRR) in case of MPLS-TE or Topology Independent Loop-free Alternate Fast Reroute (TI-LFA) in case of SR-TE), with the awareness of multi-layer TE path properties (e.g., SRLG).

In the case of inter-domain TE-paths, it is also assumed that each
packet domain in {{fig-vpn-topo}} and {{fig-vpn-path}} implements the same TE
technology, and the stitching between two domains is done using
inter-domain TE.

In this scenario, one of the key MDSC functions is to identify the
multi-domain/multi-layer TE paths to be used to carry the L2/L3 VPN
traffic between PEs belonging to different packet domains and to
relay this information to the P-PNCs, to ensure that the PEs'
forwarding tables (e.g., VRF) are properly configured to steer the
L2/L3 VPN traffic over the intended multi-domain/multi-layer TE
paths.

The selection of the TE path should take into account the TE
requirements and the binding requirements for the L2/L3 VPN network
service.

In general, the binding requirements for a network service (e.g.,
L2/L3 VPN) can be summarized within three cases:

1. The customer is asking for VPN isolation to dynamically create
and bind tunnels to the service so that they are not shared by
other services (e.g. VPN).

   The level of isolation can be different:

   {: type="a"}

   1.  Hard isolation with deterministic latency means L2/L3 VPN
   requires a set of dedicated TE Tunnels (neither sharing
   with other services nor competing for bandwidth with other
   tunnels), providing deterministic latency performances

   1.  hard isolation but without deterministic characteristics

   1.  Soft isolation means the tunnels associated with L2/L3 VPN
   are dedicated to that but can compete for bandwidth with
   other tunnels.

1. The customer does not ask for isolation and could request a VPN
service where associated tunnels can be shared across multiple
VPNs.

For each TE path required to support the L2/L3 VPN network service,
it is possible that:

1. A TE path that meets the TE and binding requirements already
exists in the network.

1. An existing TE path could be modified (e.g., through bandwidth
increase) to meet the TE and binding requirements:

   {: type="a"}

   1. The TE path characteristics can be modified only in the packet
   layer.

   1. One or more new underlay optical tunnels need to be setup to
   support the requested changes of the overlay TE paths (multi-layer coordination is required).

1. A new TE path needs to be setup to meet the TE and binding
requirements:

   {: type="a"}

   1. The new TE path reuses existing underlay optical tunnels;

   1. One or more new underlay optical tunnels need to be setup to
   support the setup of the new TE path  (multi-layer
   coordination is required).

This document analyses scenarios where only one TE path is used to
carry the VPN traffic between PEs. Scenarios, where multiple parallel
TE paths are used in load-balancing to carry the VPN traffic between
PEs, are possible but their analysis is outside the scope of this
document.

{: #path-computation-overview}

### Multi-domain and Multi-layer Path Computation

When a new TE path needs to be setup, the MDSC is also responsible
for coordinating the multi-layer/multi-domain path computation.

Depending on the knowledge that MDSC has of the topology and
configuration of the underlying network domains, three approaches for
performing multi-layer/multi-domain path computation are possible:

1. Full Summarization: In this approach, the MDSC has an abstracted
TE topology view of all of its packet and optical, underlying
domains.

   In this case, the MDSC does not have enough TE topology
   information to perform multi-layer/multi-domain path computation.
   Therefore the MDSC delegates the P-PNCs and O-PNCs to perform
   local path computation within their respective controlled domains.
   Then, it uses the information returned by the P-PNCs and O-PNCs to
   compute the optimal multi-domain/multi-layer path.

   This approach presents an issue to P-PNC, which does not have the
   capability of performing a single-domain/multi-layer path
   computation, since it can not retrieve the topology information
   from the O-PNCs nor delegate the O-PNC to perform optical path
   computation.

   A possible solution could include a CNC function within the P-PNC
   to request the MDSC multi-domain optical path computation, as
   shown in Figure 10 of {{!RFC8453}}.

   Another solution could be to rely on the MDSC recursive hierarchy,
   as defined in section 4.1 of {{!RFC8453}}, where, for each IP and
   optical domain pair, a "lower-level MDSC" (MDSC-L) provides the
   essential multi-layer correlation and the "higher-level MDSC"
   (MDSC-H) provides the multi-domain coordination.
   In this case, the MDSC-H can get an abstract view of the
   underlying multi-layer domain topologies from its underlying MDSC-L. Each MDSC-L gets the full view of the IP domain topology from
   P-PNC and can get an abstracted view of the optical domain
   topology from its underlying O-PNC. In other words, topology
   abstraction is possible at the MPIs between MDSC-L and O-PNC and
   between MDSC-L and MDSC-H.

1. Partial summarization: In this approach, the MDSC has complete
visibility of the TE topology of the packet network domains and an
abstracted view of the TE topology of the optical network domains.

   The MDSC then has only the capability of performing multi-domain/single-layer path computation for the packet layer (the
   path can be computed optimally for the two packet domains).

   Therefore, the MDSC still needs to delegate the O-PNCs to perform
   local path computation within their respective domains. It uses
   the information received by the O-PNCs and its TE topology view of
   the multi-domain packet layer to perform multi-layer/multi-domain
   path computation.

1. Full knowledge: In this approach, the MDSC has a complete and
enough detailed view of the TE topology of all the network domains
(both optical and packet).

   In such case MDSC has all the information needed to perform multi-domain/multi-layer path computation, without relying on PNCs.

   This approach may present, as a potential drawback, scalability
   issues and, as discussed in section 2.2. of {{!I-D.ietf-teas-yang-path-computation}},
   performing path computation for optical networks in the MDSC is
   quite challenging because the optimal paths depend also on
   vendor-specific optical attributes (which may be different in the
   two domains if different vendors provide them).

This document analyses scenarios where the MDSC uses the partial
summarization approach to coordinate multi-domain/multi-layer path
computation.

Typically, the O-PNCs are responsible for the optical path
computation of services across their respective single domains.
Therefore, when setting up the network service, they must consider
the connection requirements such as bandwidth, amplification,
wavelength continuity, and non-linear impairments that may affect the
network service path.

The methods and types of path requirements and impairments, such as
those detailed in {{?I-D.ietf-ccamp-optical-impairment-topology-yang}}, used by the O-PNC for optical path
computation are not exposed at the MPI and therefore out of scope for
this document.

{: #packet-pnc-overview}

## IP/MPLS Domain Controller and IP router Functions

Each packet domain in {{fig-ref-network}}, corresponding to either an IGP area
or an Autonomous System (AS) within the same operator network, is
controlled by a packet domain controller (P-PNC).

P-PNCs are responsible for setting up the TE paths between any two
PEs or BRs in their respective controlled domains, as requested by
MDSC,  and providing topology information to the MDSC.

For example, for inter-domain SR-TE, the setup bidirectional SR-TE
path from PE13 in domain 1 to PE23 in domain 2, as shown in {{fig-vpn-path}},
requires the MDSC to coordinate the actions of:

- P-PNC1 to push a SID list to PE13 including the Binding SID
associated to the SR-TE path in Domain 2 with PE23 as the target
destination (forward direction);

- P-PNC2 to push a SID list to PE23, including the Binding SID
associated with the SR-TE path in Domain 1 with PE13 as the target
destination (reverse direction).

With reference to {{fig-p-pnc}}, P-PNCs are then responsible:

1. To expose to MDSC their respective detailed TE topology

1. To perform single-layer single-domain local TE path computation,
when requested by MDSC between two PEs (for single-domain end-to-end TE path) or between PEs and BRs for an inter-domain TE path
selected by MDSC;

1. To configure the routers in their respective domain to setup a TE
path;

1. To configure the VRF and PE-CE interfaces (Service access points)
of the intra-domain and inter-domain network services requested by
the MDSC.

~~~~ ascii-art
          +------------------+            +------------------+
          |                  |            |                  |
          |      P-PNC1      |            |      P-PNC2      |
          |                  |            |                  |
          +--|-----------|---+            +--|-----------|---+
             | 1.TE      | 2.VPN             | 1.TE      | 2.VPN
             | Path      | Provisioning      | Path      | Provisioning
             | Config    |                   | Config    |
             V           V                   V           V
           +---------------------+         +---------------------+
      CE  / PE     TE path 1    BR\       / BR     TE path 2   PE \  CE
      o--/---o..................o--\-----/--o..................o---\--o
         \                         /     \                         /
          \        Domain 1       /       \       Domain 2        /
           +---------------------+         +---------------------+

                              End-to-end TE path
             <------------------------------------------------->
~~~~
{: #fig-p-pnc title="Domain Controller & node Functions"}

When requesting the setup of a new TE path, the MDSC provides the P-PNCs with the explicit path to be created or modified. In other
words, the MDSC can communicate to the P-PNCs the complete list of
nodes involved in the path (strict mode). In this case, the P-PNC is
just responsible to set up that explicit TE path. For example:

- with SR-TE, the P-PNC pushes to headend PE or BR the list of SIDs
to create the explicit SR-TE path, provided by the MDSC;

- with RSVP-TE, the P-PNC requests the headend PE or BR to start
signaling the explicit RSVP-TE path, provided by the MDSC.

To scale in large SR-TE packet domains, the MDSC can provide P-PNC a
loose path, together with per-domain TE constraints. The P-PNC can
then select the complete path within its domain.

In such a case, it is mandatory that P-PNC signals back to the MDSC
which path it has chosen so that the MDSC keeps track of the relevant
resources utilization.

From the {{fig-vpn-path}} example, the TE path requested by the MDSC touches
PE13 - P16 - BR12 - BR21 - PE23. P-PNC2 is aware of two paths with
the same topology metric, e.g. BR21 - P24 - PE23 and BR21 - BR22 - PE23, but with different loads. It may prefer to steer the traffic on
the latter because it is less loaded.

For the purposes of this document it is assumed that the MDSC always
provides the explicit list of all the hops to the P-PNCs to setup or
modify the TE path.

{: #optical-pnc-overview}

## Optical Domain Controller and NE Functions

The optical network provides underlay connectivity services to
IP/MPLS networks. The packet and optical multi-layer coordination is
done by the MDSC, as shown in {{fig-ref-network}}.

The O-PNC is responsible to:

- provide to the MDSC an abstract TE topology view of its underlying
optical network resources;

- perform single-domain local path computation, when requested by
the MDSC;

- perform optical tunnel setup, when requested by the MDSC.

The mechanisms used by O-PNC to perform intra-domain topology
discovery and path setup are usually vendor-specific and outside the
scope of this document.

Depending on the type of optical network, TE topology abstraction,
path computation and path setup can be single-layer (either OTN or
WDM) or multi-layer OTN/WDM. In the latter case, the multi-layer
coordination between the OTN and WDM layers is performed by the
O-PNC.

{: #mpi}

# Interface Protocols and YANG Data Models for the MPIs

This section describes general assumptions applicable to all the MPI
interfaces, between each PNC (Optical or Packet) and the MDSC, to
support the scenarios discussed in this document.

{: #restconf}

## RESTCONF Protocol at the MPIs

The RESTCONF protocol, as defined in {{!RFC8040}}, using the JSON
representation defined in {{!RFC7951}}, is assumed to be used at these
interfaces. In addition, extensions to RESTCONF, as defined in
{{!RFC8527}}, to be compliant with Network Management Datastore
Architecture (NMDA) defined in {{!RFC8342}}, are assumed to be used as
well at these MPI interfaces and also at MDSC NBI interfaces.

{: #yang}

## YANG Data Models at the MPIs

The data models used on these interfaces are assumed to use the YANG
1.1 Data Modeling Language, as defined in {{!RFC7950}}.

This section describes the YANG data models that are applicable to
the Packet and Optical MPIs. Some of these YANG data models can be
optional depending on the specific network configuration detailed
in {{discovery}} and {{config}}.

{: #common-yang}

### Common YANG Data Models at the MPIs

As required in {{!RFC8040}}, the "ietf-yang-library" YANG module defined
in {{!RFC8525}} is used to allow the MDSC to discover the set of YANG
modules supported by each PNC at its MPI.

Both Optical and Packet PNCs can use the following common topology
YANG data models at the MPI:

- The Base Network Model, defined in the "ietf-network" YANG module
of {{!RFC8345}};

- The Base Network Topology Model, defined in the "ietf-network-topology" YANG module of {{!RFC8345}}, which augments the Base Network Model;

- The TE Topology Model, defined in the "ietf-te-topology" YANG
module of {{!RFC8795}}, which augments the Base Network Topology
Model.

Optical and Packet PNCs can use the common TE Tunnel Model, defined
in the "ietf-te" YANG module of {{!I-D.ietf-teas-yang-te}}, at the MPI.

All the common YANG data models are generic and augmented by
technology-specific YANG modules, as described in the following
sections.

Both Optical and Packet PNCs can also use the Ethernet Topology
Model, defined in the "ietf-eth-te-topology" YANG module of {{!I-D.ietf-ccamp-eth-client-te-topo-yang}},
which augments the TE Topology Model with Ethernet technology-specific information.

Both Optical and Packet PNCs can use the following common
notifications YANG data models at the MPI:

- Dynamic Subscription to YANG Events and Datastores over RESTCONF
as defined in {{!RFC8650}};

- Subscription to YANG Notifications for Datastores updates as
defined in {{!RFC8641}}.

PNCs and MDSCs comply with subscription requirements as stated in
{{!RFC7923}}.

{: #optical-yang}

### YANG models at the Optical MPIs

The Optical PNC can use the following technology-specific topology
YANG data models, which augment the generic TE Topology Model:

- The WSON Topology Model, defined in the "ietf-wson-topology" YANG
module of {{!RFC9094}};

- the Flexi-grid Topology Model, defined in the "ietf-flexi-grid-topology" YANG module of {{!I-D.ietf-ccamp-flexigrid-yang}};

- the OTN Topology Model, as defined in the "ietf-otn-topology" YANG
module of {{!I-D.ietf-ccamp-otn-topo-yang}}.

The optical PNC can use the following technology-specific tunnel YANG
data models, which augments the generic TE Tunnel Model:

- The WDM Tunnel Model, defined in the "ietf-wdm-tunnel" YANG module
of {{!I-D.ietf-ccamp-wdm-tunnel-yang}};

- the OTN Tunnel Model, defined in the "ietf-otn-tunnel" YANG module
of {{!I-D.ietf-ccamp-otn-tunnel-model}}.

The optical PNC can use the generic Path Computation YANG RPC,
defined in the "ietf-te-path-computation" YANG module of
{{!I-D.ietf-teas-yang-path-computation}}.

Note that technology-specific augmentations of the generic path
computation RPC for WSON, Flexi-grid and OTN path computation RPCs
have been identified as a gap.

The optical PNC uses can use the following client signal YANG data
models:

- the CBR Client Signal Model, defined in the "ietf-trans-client-service" YANG module of {{!I-D.ietf-ccamp-client-signal-yang}};

- the Ethernet Client Signal Model, defined in the "ietf-eth-tran-service" YANG module of {{!I-D.ietf-ccamp-client-signal-yang}}.

{: #packet-yang}

### YANG data models at the Packet MPIs

The Packet PNC can use the following technology-specific topology
YANG data models:

- The L3 Topology Model, defined in the "ietf-l3-unicast-topology"
YANG module of {{!RFC8346}}, which augments the Base Network Topology
Model;

- the Packet TE Topology Mode, defined in the "ietf-te-topology-packet" YANG module of {{!I-D.ietf-teas-yang-l3-te-topo}}, which augments the generic TE
Topology Model;

- The MPLS-TE Topology Model, defined in the "ietf-te-mpls-topology"
YANG module of {{!I-D.ietf-teas-yang-te-mpls-topology}}, which augments the TE Packet
Topology Model with or without the L3 TE Topology Model, defined
in "ietf-l3-te-topology" YANG module of {{!I-D.ietf-teas-yang-l3-te-topo}};

- the SR Topology Model, defined in the "ietf-sr-mpls-topology" YANG
module of {{!I-D.ietf-teas-yang-sr-te-topo}}.

The Packet PNC can use the following technology-specific tunnel YANG
data models, which augments the generic TE Tunnel Model:

- The MPLS-TE Tunnel Model, defined in the "ietf-te-mpls" YANG
modules of {{!I-D.ietf-teas-yang-te-mpls}};

- the SR-TE Tunnel Model which is to be defined as described in
{{conclusions}}.

The packet PNC can use the following network service YANG data
models:

- L3VPN Network Model (L3NM), defined in the "ietf-l3vpn-ntw" YANG
module of {{?RFC9182}};

- L3NM TE Service Mapping, defined in the "ietf-l3nm-te-service-mapping" YANG module of {{?I-D.ietf-teas-te-service-mapping-yang}};

- L2VPN Network Model (L2NM), defined in the "ietf-l2vpn-ntw" YANG
module of {{?RFC9291}};

- L2NM TE Service Mapping, defined in the "ietf-l2nm-te-service-mapping" YANG module of {{?I-D.ietf-teas-te-service-mapping-yang}}.

{: #pcep}

## Path Computation Element Protocol (PCEP)

{{?RFC8637}} examines the applicability of a Path Computation Element
(PCE) {{?RFC5440}} and PCE Communication Protocol (PCEP) to the ACTN
framework. It further describes how the PCE architecture applies to
ACTN and lists the PCEP extensions needed to use PCEP as an ACTN
interface.  The stateful PCE {{?RFC8231}}, PCE-Initiation {{?RFC8281}},
stateful Hierarchical PCE (H-PCE) {{?RFC8751}}, and PCE as a central
controller (PCECC) {{?RFC8283}} are some of the key extensions that
enable the use of PCE/PCEP for ACTN.

Since the PCEP supports path computation in the packet and optical
networks, PCEP is well suited for inter-layer path computation.
{{?RFC5623}} describes a framework for applying the PCE-based
architecture to interlayer (G)MPLS traffic engineering. Furthermore,
section 6.1 of {{?RFC8751}} states the H-PCE applicability for inter-layer or POI.

{{?RFC8637}} lists various PCEP extensions that apply to ACTN. It also
lists the PCEP extension for the optical network and POI.

Note that the PCEP can be used in conjunction with the YANG data
models described in the rest of this document. Depending on whether
ACTN is deployed in a greenfield or brownfield, two options are
possible:

1. The MDSC uses a single RESTCONF/YANG interface towards each PNC to
discover all the TE information and request TE tunnels. It may
perform full multi-layer path computation or delegate path
computation to the underneath PNCs.

   This approach is desirable for operators from a multi-vendor
   integration perspective as it is simple. We need only one type of
   interface (RESTCONF) and use the relevant YANG data models
   depending on the operator use case considered. The benefits of
   having only one protocol for the MPI between MDSC and PNC have
   already been highlighted in {{!I-D.ietf-teas-yang-path-computation}}.

1. The MDSC uses the RESTCONF/YANG interface towards each PNC to
discover all the TE information and requests the creation of TE
tunnels. However, it uses PCEP for hierarchical path computation.

   As mentioned in Option 1, from an operator perspective, this
   option can add integration complexity to have two protocols
   instead of one unless the RESTCONF/YANG interface is added to an
   existing PCEP deployment (brownfield scenario).

{{discovery}} and {{config}} of this draft analyze the case where a single
RESTCONF/YANG interface is deployed at the MPI (i.e., option 1
above).

{: #discovery}

# Inventory, Service and Network Topology Discovery

In this scenario, the MSDC needs to discover through the underlying
PNCs:

- the network topology, at both optical and IP layers, in terms of
nodes and links, including the access links, inter-domain IP links
as well as Cross-technology links;

- the optical tunnels supporting multi-technology intra-domain IP links;

- both intra-domain and inter-domain L2/L3 VPN network services
deployed within the network;

- the TE paths supporting those L2/L3 VPN network services;

- the hardware inventory information of IP and optical equipment.

The O-PNC and P-PNC could discover and report the hardware network
inventory information of their equipment used by the different
management layers. In the context of POI, the inventory information
of IP and optical equipment can complement the topology views and
facilitate the packet/optical multi-layer view, e.g., by providing a
mapping between the lowest level LTPs in the topology view and
corresponding ports in the network inventory view.

The MDSC could also discover the entire network inventory information
of both IP and optical equipment and correlate this information with
the links reported in the network topology.

Reporting the entire inventory and detailed topology information of
packet and optical networks to the MDSC may present scalability
issues as a potential drawback. The analysis of the scalability of
this approach and mechanisms to address potential issues is outside
the scope of this document.

Each PNC provides the MDSC the topology view of the domain it
controls, as described in {{optical-topology-discovery}} and {{packet-topology-discovery}}. The MDSC uses this
information to discover the complete topology view of the multi-layer
multi-domain networks it controls.

The MDSC should also maintain up-to-date inventory, service and
network topology databases of IP and optical layers through IETF
notifications through MPI with the PNCs when any network
inventory/topology/service change occurs.

It should also be possible to correlate information from IP and
optical layers (e.g., which port, lambda/OTSi, and direction are used
by a specific IP service on the WDM equipment).

In particular, for the Cross-technology links, it is key for MDSC to
automatically correlate the information from the PNC network
databases about the physical ports from the routers (single link or
bundle links for LAG) to client ports in the ROADM.

The analysis of multi-layer fault management is outside the scope of
this document. However, the discovered information should be
sufficient for the MDSC to correlate optical and IP layers alarms to
speed-up troubleshooting easily.

Alarms and event notifications are required between MDSC and PNCs so
that any network changes are reported almost in real-time to the MDSC
(e.g., node or link failure). As specified in {{!RFC7923}}, MDSC must
subscribe to specific objects from PNC YANG datastores for
notifications.

{: #optical-topology-discovery}

## Optical Topology Discovery

The WSON Topology Model and the Flexi-grid Topology model can be used
to report the DWDM network topology (e.g., WDM nodes and OMS links),
depending on whether the DWDM optical network is based on fixed-grid
or flexible-grid or a mix of fixed-grid and flexible-grid.

It is worth noting that, as described in Appendix I of {{ITU-T_G.694.1}},
a fixed-grid can also be described as a flexible grid
with constraints: for example a 50GHz fixed-grid can be described as
a flexible-grid which supports only m=4 and values of n which are
only multiplier of 8.

As a consequence:

- A flexible-grid DWDM network topology can only be reported using
the Flexi-grid Topology model;

- A fixed-grid DWDM network topology, can be reported using either
the WSON Topology model or the Flexi-grid Topology model;

- A mixed fixed and flexible grid DWDM network topology can be
reported using either the Flexi-grid Topology model or both WSON
and Flexi-grid topology models.

Clarifying how both WSON and Flexi-grid topology models could be used
together (e.g., through multi-inheritance as described in {{?I-D.ietf-teas-te-topology-profiles}})
has been identified as a gap.

The OTN Topology Model is used to report the OTN network topology
(e.g., OTN switching nodes and links), when the OTN switching layer
is deployed within the optical domain.

To allow the MDSC to discover the complete multi-layer and multi-domain network topology and to correlate it with the hardware
inventory information, the O-PNCs report an abstract optical network
topology where:

- one TE node is reported for each optical node deployed within the
optical network domain; and

- one TE link is reported for each OMS link and, optionally, for
each OTN link.

Since the MDSC delegates optical path computation to its underlay O-PNCs, the following information can be abstracted and not reported at
the MPI:

- the optical parameters required for optical path computation, such
as those detailed in {{?I-D.ietf-ccamp-optical-impairment-topology-yang}};

- the underlay OTS links and ILAs of OMS links;

- the physical connectivity between the optical transponders and the
ROADMs.

The OTN Topology Model also reports the CBR client LTPs that
terminates the Cross-technology links: once CBR client LTP is reported for
each CBR or multi-function client interface on the optical nodes (see
sections 4.4 and 5.1 of {{?I-D.ietf-ccamp-transport-nbi-app-statement}} for the description of multi-function
client interfaces).

The Ethernet Topology Model reports the Ethernet client LTPs that
terminate the Cross-technology links: one Ethernet client LTP is reported
for each Ethernet or multi-function client interface on the optical
nodes.

The optical transponders and, optionally, the OTN access cards, are
abstracted at MPI by the O-PNC as Trail Termination Points (TTPs),
defined in {{!RFC8795}}, within the optical network topology. This
abstraction is valid independently of the fact that optical
transponders are physically integrated within the same WDM node or
are physically located on a device external to the WDM node since it
both cases the optical transponders and the WDM node are under the
control of the same O-PNC and abstracted as a single WDM TE Node at the O-MPI.

The association between the Ethernet or CBR client LTPs terminating
the Ethernet Cross-technology links and the optical TTPs is reported using
the Inter Layer Lock-id (ILL) identifiers, defined in {{!RFC8795}}.

For example, with a reference to {{fig-optical-topo}}, the ILL values X and Y are
used to associated the client LTPs (7-0) in NE11 and (8-0) in NE12
with the corresponding optical TTPs (7) in NE11 and (8) in NE12,
respectively.

{::include ./figures/multi-layer-optical-topology.md}
{: #fig-optical-topo title="Multi-layer optical topology discovery"}

The intra-domain optical links are discovered by O-PNCs, using
mechanisms which are outside the scope of this document, and reported
at the MPIs within the optical network topology.

In case of a multi-layer DWDM/OTN network domain, multi-layer intra-domain OTN links are supported by underlay WDM tunnels: this
relationship is reported by the mechanisms described in {{optical-path-discovery}}.

{: #optical-path-discovery}

## Optical Path Discovery

The WDM Tunnel Model is used to report all the WDM tunnels
established within the optical network.

When the OTN switching layer is deployed within the optical domain,
the OTN Tunnel Model is used to report all the OTN tunnels
established within the optical network.

The Ethernet client signal model and the Transparent CBR client
signal model are used to report all the connectivity services
provided by the underlay optical tunnels between Ethernet or CBR
client LTPs, depending on whether the connectivity service is frame-based or transparent. The underlay optical tunnels can be either WDM
tunnels or, when the optional OTN switching layer is deployed, OTN
tunnels.

The WDM tunnels can be used to support either Ethernet or CBR client
signals or multi-layer intra-domain OTN links. In the latter case,
the hierarchical-link container, defined in {{!I-D.ietf-teas-yang-te}}, associates
the underlay WDM tunnel with the supported multi-layer intra-domain
OTN link and it allows discovery of the multi-layer path supporting
all the connectivity services provided by the optical network.

The O-PNCs report in their operational datastores all the Ethernet
and CBR client connectivities and all the optical tunnels deployed
within their optical domain regardless of the mechanisms being used to
set them up, such as the mechanisms described in {{multi-technology-link-setup}}, as well
as other mechanism (e.g., static configuration), which are outside
the scope of this document.

{: #packet-topology-discovery}

## Packet Topology Discovery

The L3 Topology Model is used report the IP network topology.

The L3 Topology Model, SR Topology Model, TE Topology Model and the
TE Packet Topology Model are used together to report the SR-TE
network topology, as described in Figure 2 of {{!I-D.ietf-teas-yang-sr-te-topo}}.

The TE Topology Model, TE Packet Topology Model and MPLS-TE Topology
Model are used together to report the MPLS-TE network topology, as
described in {{!I-D.ietf-teas-yang-te-mpls-topology}}.

As described in {{!I-D.ietf-teas-yang-l3-te-topo}}, the relationship between the IP network
topology and the MPLS-TE network topology depends on whether the two
network topologies are congruent or not: in the latter case, the L3
TE Topology Model is used, together with the L3 Topology Model to
provide the association between the two network topologies.

To allow the MDSC to discover the complete multi-layer and multi-domain network topology and to correlate it with the hardware
inventory information as well as to perform multi-domain TE path
computation, the P-PNCs report the full packet network, including all
the information that the MDSC requires to perform TE path
computation. In particular, one TE node is reported for each IP router
and one TE link is reported for each intra-domain IP link. The packet
topology also reports the IP LTPs terminating the inter-domain IP
links.

The Ethernet Topology Model is used to report the intra-domain
Ethernet links supporting the intra-domain IP links as well as the
Ethernet LTPs that might terminate Cross-technology links, inter-domain
Ethernet links or access links, as described in detail in {{inter-domain-link-discovery}}
and in {{multi-technology-link-discovery}}.

All the intra-domain Ethernet and IP links are discovered by the
P-PNCs, using mechanisms, such as LLDP {{IEEE_802.1AB}}, which are
outside the scope of this document, and reported at the MPIs within
the Ethernet or the packet network topology.

{: #te-path-discovery}

## TE Path Discovery

We assume that the discovery of existing TE paths, including their
bandwidth, at the MPI is done using the generic TE tunnel YANG data
model, defined in {{!I-D.ietf-teas-yang-te}}, with packet technology-specific (e.g.,
MPLS-TE or SR-TE) augmentations.

Note that technology-specific augmentations of the generic path TE
tunnel model for SR-TE path setup and discovery is outlined in
section 1 of {{!I-D.ietf-teas-yang-te}} but are currently identified as a gap in
{{conclusions}}.

To enable MDSC to discover the full end-to-end TE path configuration,
the technology-specific augmentation of the {{!I-D.ietf-teas-yang-te}} should allow
the P-PNC to report the TE path within its domain (e.g., the SID list
assigned to an SR-TE path).

For example, considering the L3VPN in {{fig-vpn-topo}}, the TE path 1 in one
direction (PE13-P16-PE14) and the TE path in the reverse direction
(between PE14 and PE13) should be reported by the P-PNC1 to the MDSC
as TE primary and primary-reverse paths of the same TE tunnel
instance. The bandwidth of these TE paths represents the bandwidth
allocated by P-PNC1 to the two TE paths, which can be symmetric or
asymmetric in the two directions.

The P-PNCs use the TE tunnel model to report, at the MPI, all the TE
paths established within their packet domain regardless of the
mechanism being used to set them up; i.e., independently on whether
the mechanisms described in {{te-path-config}} or other means, such as
static configuration, which are outside the scope of this document,
are used.

{: #inter-domain-link-discovery}

## Inter-domain Link Discovery

In the reference network of {{fig-ref-network}}, there are three types of
inter-domain links:

- Inter-domain Ethernet links supporting inter-domain IP links
between two adjacent IP domains;

- Cross-technology links between an an IP domain and an adjacent optical
domain;

- Access links between a CE device and a PE router.

All the three types of links are Ethernet links.

It is worth noting that the P-PNC may not be aware whether an
Ethernet interface terminates a Cross-technology link, an inter-domain
Ethernet link or an access link. The TE Topology Model supports the
discovery for all these types of links with no need for the P-PNC to
know the type of inter-domain link.

There are two possible models to report the access links between CEs
and PEs: the TE Topology Model, defined in {{!RFC8795}}, or the Service
Attachment Points (SAP) Model, defined in  {{?RFC9408}}.

Although the discovery of access links is outside the scope of this
document, clarifying the relationship between these two models has
been identified as a gap.

The inter-domain Ethernet links and Cross-technology links are discovered
by the MDSC using the plug-id attribute, as described in section 4.3
of {{!RFC8795}}.

More detailed description of how the plug-id can be used to discover
inter-domain links is also provided in section 5.1.4 of {{?I-D.ietf-ccamp-transport-nbi-app-statement}}.

The plug-id attribute can also be used to discover the access-links,
but the analysis of the access-link discovery is outside the scope of
this document.

This document considers the following two options for discovering
inter-domain links:

1. Static configuration

2. LLDP {{IEEE_802.1AB}} automatic discovery

Other options are possible but not described in this document.

As outlined in {{?I-D.ietf-ccamp-transport-nbi-app-statement}}, the encoding of the plug-id namespace and the
specific LLDP information reported within the plug-id value, such as
the Chassis ID and Port ID mandatory TLVs, is implementation specific
and needs to be consistent across all the PNCs within the network.

The static configuration requires an administrative burden to
configure network-wide unique identifiers: it is therefore more
viable for inter-domain Ethernet links. For the Cross-technology links, the
automatic discovery solution based on LLDP snooping is preferable
when possible.

The routers exchange standard LLDP packets as defined in {{IEEE_802.1AB}}
and the optical nodes snoop the LLDP packets received from the
local Ethernet interface and report to the O-PNCs the extracted
information, such as the Chassis ID, the Port ID, System Name TLVs.

Note that the optical nodes do not actively participate in the LLDP
packet exchange and does not send any LLDP packets.

### Cross-technology link Discovery {#cross-technology-link-discovery}

The MDSC can discover a Cross-technology link by matching the plug-id
values of the two LTPs reported by two adjacent O-PNC and P-PNC: in
case LLDP snooping is used, the P-PNC reports the LLDP information
sent by the corresponding Ethernet interface on the IP router while the
O-PNC reports the LLDP information received by the corresponding
Ethernet interface on the optical node, e.g., between LTP 5-0 on PE13
and LTP 7-0 on NE11, as shown in {{fig-cross-technology-link}}.

{::include ./figures/cross-technology-link.md}
{: #fig-cross-technology-link title="Cross-technology Ethernet link discovery"}

As described in {{optical-topology-discovery}}, the LTP terminating a Cross-technology link
is reported by an O-PNC in the Ethernet topology or in the OTN
topology model or in both models, depending on the type of
corresponding physical port on the optical node.

It is worth noting that the discovery of Cross-technology links is based
only on the LLDP information sent by the Ethernet interfaces of the
routers and received by the Ethernet interfaces of the optical nodes.
Therefore the MDSC can discover these links also before optical
paths, supporting overlay multi-technology IP links, are setup.

{: #ip-inter-domain-link-discovery}

### Inter-domain IP Link Discovery

The MDSC can discover an inter-domain Ethernet link which supports an
inter-domain IP link, by matching the plug-id values of the two
Ethernet LTPs reported by the two adjacent P-PNCs: the two P-PNCs
report the LLDP information being sent and being received from the
corresponding Ethernet interfaces, e.g., between the Ethernet LTP 3-1
on BR11 and the Ethernet LTP 4-1 on BR21 shown in {{fig-inter-domain-link}}.

{::include ./figures/inter-domain-link.md}
{: #fig-inter-domain-link title="Inter-domain Ethernet and IP link discovery"}

Different information is required to be encoded by the P-PNC within
the plug-id attribute of the Ethernet LTPs to discover cross-technology Ethernet
links and inter-domain Ethernet links.

If the P-PNC does not know a priori whether an Ethernet interface on
an IP router terminates a Cross-technology link or an inter-domain Ethernet
link, it has to report at the MPI two Ethernet LTPs representing the
same Ethernet interface, e.g., both the Ethernet LTP 3-0 and the
Ethernet LTP 3-1, supported by LTP 3-0, shown in {{fig-inter-domain-link}}:

- The physical Ethernet LTP (e.g., LTP 3-0 in BR11, as shown in
{{fig-inter-domain-link}}) is used to represent the physical adjacency between the
Ethernet interface on an IP router and the Ethernet interface on its physically adjacent node,
which can be either an IP router
(in case of a single-technology Ethernet link) or an optical
node (in case of a multi-technology Ethernet link).
Therefore, as described in {{cross-technology-link-discovery}}, the P-PNC reports,
within the plug-id attribute of this LTP, the LLDP information
sent by the corresponding Ethernet interface on the IP router; such as the
{BR11,3} and {BR21,4} plug-id values reported, respectively, by
the Ethernet LTP 3-0 on BR11 and by the Ethernet LTP 4-0 on BR21,
as shown in {{fig-inter-domain-link}};

- The logical Ethernet LTP (e.g., LTP 3-1 in BR11, as shown in
{{fig-inter-domain-link}}), supported by a physical Ethernet LTP (e.g., LTP 3-0 in
BR11, as shown in {{fig-inter-domain-link}}), is used to discover the logical
adjacency between the Ethernet interfaces on IP routers, which can be either
single-technology or multi-technology. Therefore, the P-PNC reports, within
the plug-id attribute of this LTP, the LLDP information sent and
received by the corresponding Ethernet interface on the IP router; such as
the {BR11,3,BR21,4} plug-id values reported by the Ethernet LTP 3-1 on BR11 and by the Ethernet LTP 4-1 on BR21, as shown in {{fig-inter-domain-link}}.

It is worth noting that in case of an inter-domain Ethernet links, the MDSC cannot discover, using the the LLDP
information reported in the plug-id attributes, the physical
adjacency between the two Ethernet interfaces on physically adjacent IP routers, because these
two plug-id values do not match, such as the plug-id values {BR11,3}
and {BR21,4} shown in {{fig-inter-domain-link}}. However, the MDSC may infer the
physical intra-domain Ethernet links if it knows a priori, using
mechanisms which are outside the scope of this document, that the
Ethernet interfaces on the IP routers either terminates a cross-technology
link or a single-technology (intra-domain or inter-domain) Ethernet link,
e.g., as shown in {{fig-inter-domain-link}}.

The P-PNC can omit reporting the physical Ethernet LTPs when it
knows, by mechanisms which are outside the scope of this document,
that the corresponding Ethernet interfaces terminate inter-domain Ethernet links.

The MDSC can then discover an inter-domain IP link between the two IP
LTPs that are supported by the two Ethernet LTPs terminating an
inter-domain Ethernet link, discovered as described in {{ip-inter-domain-link-discovery}},
e.g., between the IP LTP 3-2 on BR21 and the IP LTP 4-2 on BR22,
supported respectively by the Ethernet LTP 3-1 on BR11 and by the
Ethernet LTP 4-1 on BR21, as shown in {{fig-inter-domain-link}}.

{: #multi-technology-link-discovery}

## Multi-technology IP Link Discovery

A multi-technology intra-domain IP link and its supporting multi-technology
intra-domain Ethernet link are discovered by the P-PNC like any other
intra-domain IP and Ethernet links, as described in {{packet-topology-discovery}}, and
reported at the MPI within the packet and the Ethernet network
topologies, e.g., as shown in {{fig-multi-technology-link}}.

{::include ./figures/multi-technology-intra-domain-link.md}
{: #fig-multi-technology-link title="Multi-technology intra-domain Ethernet and IP link discovery"}

The P-PNC does not report any plug-id information on the logical
Ethernet LTPs terminating intra-domain Ethernet links, such as the
LTP 5-1 on PE13 and LTP 6-1 in BR11 shown in {{fig-multi-technology-link}}, since these
links are discovered by the PNC.

In addition, the P-PNC also reports the physical Ethernet LTPs that
terminate the Cross-technology links supporting the multi-technology intra-domain Ethernet links, e.g., the Ethernet LTP 5-0 on PE13 and the
Ethernet LTP 6-0 on BR11, shown in {{fig-multi-technology-link}}.

The MDSC discovers, using the mechanisms described in {{inter-domain-link-discovery}},
which Ethernet Cross-technology links support the multi-technology intra-domain
Ethernet links, e.g., the link between LTP 5-0 on PE13 and LTP 7-0 on
NE11, shown in {{fig-multi-technology-link}}.

The MDSC also discovers, from the information provided by the O-PNC
and described in {{optical-path-discovery}}, which optical tunnels support the
multi-technology intra-domain IP links and therefore the path within the
optical network that supports a multi-technology intra-domain IP link,
e.g., as shown in {{fig-multi-technology-link}}.

{: #single-technology-link-discovery-discovery}

### Intra-domain single-technology IP Links

It is worth noting that the P-PNC may not be aware of whether an
Ethernet interface on the IP router terminates a multi-technology or a
single-technology intra-domain Ethernet link.

In this case, the P-PNC, always reports two Ethernet LTPs for each
Ethernet interface on the IP router, e.g., the Ethernet LTP 1-0 and 1-1
on PE13, shown in {{fig-intra-domain-link}}.

{::include ./figures/single-technology-intra-domain-link.md}
{: #fig-intra-domain-link title="Single-technology intra-domain Ethernet and IP link discovery"}

It is worth noting that in case of an intra-domain single-technology
Ethernet links, the MDSC cannot discover, using the LLDP information
reported in the plug-id attributes, the physical adjacency
between the two Ethernet interfaces on physically adjacent IP routers,
because the two plug-id values do
not match, such as the plug-id values {PE13,1} and {P16,2} shown in
{{fig-intra-domain-link}}. However, the MDSC may infer the physical intra-domain
Ethernet links, e.g., between LTP 1-0 on PE13 and LTP 2-0 on P16, as
shown in {{fig-intra-domain-link}}, if it knows a priori, using mechanisms which are
outside the scope of this document, that all the Ethernet interfaces
on the IP routers either terminates a cross-technology or a single-technology
(intra-domain or inter-domain) Ethernet link, e.g., as shown in
{{fig-intra-domain-link}}.

The P-PNC can omit reporting the physical Ethernet LTP if it knows,
by mechanisms which are outside the scope of this document, that the
intra-domain Ethernet link is single-technology.

{: #lag-discovery}

## LAG Discovery

The P-PNCs can discover the configuration of the LAG groups within
its domain and report each intra-domain LAG as an Ethernet bundle
link, within the Ethernet topology exposed at the MPI.

This is done bundling multiple single-domain Ethernet links, as shown
in {{fig-lag}}. For example, the Ethernet bundled link between the
Ethernet LTP 5-1 on BR21 and the Ethernet LTP 6-1 on P24, is built
from the Ethernet links setup respectively:

- between the Ethernet LTP 1-1 on BR21 and the Ethernet LTP 2-1 on
P24; and

- between the Ethernet LTP 3-1 on BR21 and the Ethernet LTP 4-1 on
P24.

{::include ./figures/lag.md}
{: #fig-lag title="LAG"}

The mechanisms used by the MDSC to discover single-technology and multi-technology intra-domain LAG link is the same (the only difference being
whether the bundled links are single-technology or multi-technology).

Instead, the mechanisms used by the MDSC to discover single-technology
inter-domain LAG links between two BRs are different and outside the
scope of this document since they do not imply any cross-technology
coordination between packet and optical domains.

As described in {{packet-topology-discovery}}, the mechanisms used by the P-PNC to
discover the configuration of the LAG groups within its domain, such
as LLDP {{IEEE_802.1AB}}, are outside the scope of this document.

However, it is worth noting that according to {{IEEE_802.1AB}}, LLDP
can be configured on a LAG group (Aggregated Port) and/or on any
number of its LAG members (Aggregation Ports).

If LLDP is enabled on both LAG members and groups, two types of LLDP
packets are transmitted by the routers and received by the optical
nodes on some Cross-technology links: one sent for the LLDP session
configured at LAG member (Aggregation Port)level and another one for
the LLDP session configured at LAG group (Aggregated Port)level. This
could cause some issues when LLDP snooping is used to discover the
Cross-technology links, as defined in {{cross-technology-link-discovery}}.

The Cross-technology link discovery is based only on the LLDP session
configured on the LAG members (Aggregation Ports) to allow discovery
of these links independently from the configuration of the underlay
optical tunnel or from the LAG group.

To avoid any ambiguity on how the optical nodes can identify which LLDP
packets belong to which LLDP session, the P-PNC can disable the LLDP
sessions on the LAG groups configured by the MDSC (e.g., the multi-technology single-domain LAG groups configured using the mechanisms
described in {{lag-setup}}), keeping the LLDP sessions on the LAG
members enabled.

Another option is to rely on other mechanisms (e.g., the Port type
field in the Link Aggregation TLV defined in Annex F of {{IEEE_802.1AX}})
that allow the optical node to identify which LLDP packets
belong to which LLDP session: the O-PNC can then use only the LLDP
information from the LLDP sessions configured on the LAG members to
support the Cross-technology link discovery mechanisms defined in {{cross-technology-link-discovery}}.

{: #vpn-discovery}

## L2/L3 VPN Network Services Discovery

The P-PNC reports the L2/L3 VPN services configured within its
domain, using the L2NM and L3NM network service models, and which
packet TE tunnels (e.g., MPLS-TE or SR-TE) are used by each L2/L3 VPN
service, using the L2NM and L3NM TE service mapping models.

The MDSC can use the information mentioned above together with the
packet TE path, packet topology, multi-technology IP links, optical
topology and optical path information discovered as described in the
previous sections, to discover the multi-technology path used to carry the
traffic for each L2/L3 VPN service.

{: #inventory-discovery}

## Inventory Discovery

The are no YANG data models in IETF that could be used to report at
the MPI the whole inventory information discovered by a PNC.

{{!RFC8345}} had foreseen some work for inventory as an augmentation of
the network model, but no YANG data model has been developed so far.

There are also no YANG data models in IETF that could be used to
correlate topology information, e.g., a link termination point (LTP),
with inventory information, e.g., the physical port supporting an
LTP, if any.

Inventory information through MPI and correlation with topology
information is identified as a gap requiring further work and outside
of the scope of this draft.

{: #config}

# Establishment of L2/L3 VPN Services with TE Requirements

In this scenario the MDSC needs to setup a multi-domain L2VPN or a
multi-domain L3VPN with some SLA requirements.

The MDSC receives the request to setup a L2/L3 VPN network service
from the OSS/Orchestration layer (see {{additional-scenarios}}).

The MDSC translates the L2/L3 VPN SLA requirements into TE
requirements (e.g., bandwidth, TE metric bounds, SRLG disjointness,
nodes/links/domains inclusion/exclusion) and find the TE paths that
meet these TE requirements (see {{vpn-overview}}).

For example, considering the L3VPN in {{fig-vpn-topo}} and {{fig-vpn-path}}, the MDSC
finds that:

- PE13-P16-PE14 TE path already exists but have not enough bandwidth
to support the new L3VPN, as described in {{te-path-discovery}};, and that:

   - the IP link(s) between PE13 and P16 has not enough bandwidth
   to support increasing the bandwidth of that TE path, as
   described in {{packet-topology-discovery}};

   - a new underlay optical tunnel could be setup to increase the
   bandwidth of the IP link(s) between PE13 and P16 to support
   increasing the bandwidth of that overlay TE path, as described
   in {{optical-path-computation}}. The dimensioning of the underlay optical
   tunnel is decided by the MDSC based on the TE requirements
   (e.g., the bandwidth) requested by the TE path and on its
   multi-layer optimization policy, which is an internal MDSC
   implementation issue;

   - a new multi-domain TE path needs to be setup between PE13 and
   PE23, e.g., either because existing TE paths between PE13 and
   PE23 are not able to meet the TE and binding requirements of
   the L2/L3 VPN service or because there is no TE path between
   PE13 and PE23.

As described in {{path-computation-overview}}, with partial summarization, the MDSC
will use the TE topology information provided by the P-PNCs and the
results of the path computation requests sent to the O-PNCs, as
described in {{optical-path-computation}}, to compute the multi-layer/multi-domain
path between PE13 and PE23.

For example, the multi-layer/multi-domain performed by the MDSC could
require the setup of:

- a new underlay optical tunnel between PE13 and BR11, supporting a
new IP link, as described in {{multi-technology-link-setup}};

- a new underlay optical tunnel between BR21 and P24 to increase the
bandwidth of the IP link(s) between BR21 and P24, as described in
{{multi-technology-link-setup}}.

When the setup of the L2/L3 VPN network service requires multi-domain
and multi-layer coordination, the MDSC is also responsible for
coordinating the network configuration required to realize the
request network service across the appropriate optical and packet
domains.

The MDSC would therefore request:

- the O-PNC1 to setup a new optical tunnel between the ROADMs
connected to PE13 and P16, as described in {{multi-technology-link-setup}};

- the P-PNC1 to update the configuration of the existing IP link, in
case of LAG, or configure a new IP link, in case of Equal Cost Multi-Path (ECMP), between
PE13 and P16, as described in {{multi-technology-link-setup}};

- the P-PNC1 to update the bandwidth of the selected TE path between
PE13 and PE14, as described in {{te-path-config}}.

After that, the MDSC requests P-PNC2 to setup a TE path between BR21
and PE23, with an explicit path (BR21, P24, PE23) to constrain this
new TE path to use the new underlay optical tunnel setup between BR21
and P24, as described in {{te-path-config}}. The P-PNC2 properly configures
the routers within its domain to setup the requested path and returns
to the MDSC the information which is needed for multi-domain TE path
stitching. For example, in case of inter-domain SR-TE, the P-PNC2,
knowing the node and the adjacency SIDs assigned within its domain,
can install the proper SR policy, or hierarchical policies, within
BR21 and returns to the MDSC the binding SID it has assigned to this
policy in BR21.

Then the MDSC requests P-PNC1 to setup a TE path between PE13 and
BR11, with an explicit path (PE13, BR11) to constrain this new TE
path to use the new underlay optical tunnel setup between PE13 and
BR11, specifying also which inter-domain link should be used to send
traffic to BR21 and the information to be used for the multi-domain
TE path stitching, as described in {{te-path-discovery}} (e.g., in case of
inter-domain SR-TE, the binding SID  that has been assigned by P-PNC2
to the corresponding SR policy in BR21). The P-PNC1 properly
configures the routers within its domain to setup the requested path
and the multi-domain TE path stitching. For example, in case of
inter-domain SR-TE, the P-PNC1, knowing also the node and the
adjacency SIDs assigned within its domain and the EPE SID assigned by
P-PNC1 to the inter-domain link between BR11 and BR21, and the
binding SID assigned by P-PNC2, installs the proper policy, or
policies, within PE13.

Once the TE paths have been selected and, if needed, setup/modified,
the MDSC can request to both P-PNCs to configure the L3VPN and its
binding with the selected TE paths, as described in {{vpn-setup}}.

{: #optical-path-computation}

## Optical Path Computation

As described in {{path-computation-overview}}, the optical path computation is
usually performed by the O-PNCs.

When performing multi-layer/multi-domain path computation, the MDSC
can delegate the O-PNC for single-domain optical path computation.

As described in {{optical-topology-discovery}}, {{inter-domain-link-discovery}} and {{multi-technology-link-discovery}}, there is a one-to-one
relationship between a multi-layer intra-domain IP link and its
underlay optical tunnel. Therefore, the properties of an optical path
between two optical TTPs, as computed by the O-PNC, can be used by
the MDSC to infer the properties of the associated multi-layer
single-domain IP link.

As discussed in {{!I-D.ietf-teas-yang-path-computation}}, there are two options to request an
O-PNC to perform optical path computation: either via a "compute-only" TE tunnel path, using the generic TE tunnel YANG data model
defined in {{!I-D.ietf-teas-yang-te}} or via the path computation RPC defined in
{{!I-D.ietf-teas-yang-path-computation}}.

This draft assumes that the path computation RPC is used.

There are no YANG data models in IETF that could be used to augment
the generic path computation RPC with technology-specific attributes.

Optical technology-specific augmentation for the path computation RPC
is identified as a gap requiring further work outside of this draft's
scope.

{: #multi-technology-link-setup}

## Multi-technology IP Link Setup

As described in {{optical-path-computation}}, there is a one-to-one relationship
between a multi-technology intra-domain IP link and its underlay optical
tunnel.

Therefore, to setup a new multi-technology intra-domain IP link, the MDSC
requires the O-PNC to setup the  optical tunnel (using either the WDM
Tunnel model or the OTN Tunnel model, if the optional OTN switching
is supported) within the optical network and to steer the client
traffic between the two Cross-technology links over that optical tunnel,
using either the Ethernet Client Signal Model (for frame-based
transport) or the Transparent CBR Client Signal Model (for
transparent transport).

For example, with a reference to {{fig-multi-technology-link-2}}, the MDSC can request the
O-PNC1 to setup an optical tunnel between the optical TTPs (7) on
NE11 and (8) on NE12 and to steer over this tunnel the client traffic
between LTP (7-0) on NE11 and LTP (8-0) on NE12.

{::include ./figures/multi-technology-intra-domain-link.md}
{: #fig-multi-technology-link-2 title="Multi-technology IP link setup"}

Note: {{fig-multi-technology-link-2}} is an exact copy of {{fig-multi-technology-link}}.

After the optical tunnel has been setup and the client traffic
steering configured, the two IP routers can exchange Ethernet frames
between themselves, including LLDP messages.

If LLDP {{IEEE_802.1AB}} or any other discovery mechanisms, which are
outside the scope of this document, is used between the adjacency
between the two IP routers' ports, the P-PNC can automatically discover
the underlay multi-technology single-domain Ethernet link being set up by
the MDSC and report it to the P-PNC, as described in {{multi-technology-link-discovery}}.

Otherwise, if there are no automatic discovery mechanisms, the MDSC
can configure this multi-technology single-domain Ethernet link at the MPI
of the P-PNC.

The two Ethernet LTPs terminating this multi-technology single-domain
Ethernet link are supported by the two underlay Ethernet LTPs
terminating the two Cross-technology links, e.g., the LTP 5-1 on PE13 and
6-1 on BR11 shown in {{fig-multi-technology-link-2}}.

After the multi-technology single-domain Ethernet link has been configured
by the MDSC or discovered by the P-PNC, the corresponding multi-technology
single-domain IP link can also be configured either by the MDSC or by
the P-PNC.

This document assumes that this IP link is configured by the P-PNC.

It is worth noting that if LAG is not supported within the domain
controlled by the P-PNC, the P-PNC can configure the multi-technology
single-domain IP link as soon as the underlay multi-technology single-domain Ethernet link is either discovered by the P-PNC or configured
by the MDSC at the MPI. However, if LAG is supported the P-PNC has
not enough information to know whether the discovered/configured
multi-technology single-domain Ethernet link would be:

1. Used to support a multi-technology single-domain IP link;

2. Used to create a new LAG group;

3. Added to an existing LAG group.

Therefore the P-PNC does not take any further action after a multi-technology single-domain Ethernet link is discovered or configured by the
MDSC at the MPI.

The MDSC can request the P-PNC to configure a new multi-technology single-domain IP link, supported by the the just discovered or configured
multi-technology single-domain Ethernet link, by creating an IP link
within the running datastore of the P-PNC MPI. Only the IP link, IP
LTPs and the reference to the supporting multi-technology single-domain
Ethernet link are configured by the MDSC. All the other configuration
is provided by the P-PNC.

For example, with a reference to {{fig-multi-technology-link-2}}, the MDSC can request the
P-PNC1 to setup a multi-technology single-domain IP Link between IP LTP 5-2 on PE13 and IP LTP 6-2 on BR11 supported by the multi-technology single-domain Ethernet link between ETH LTP 5-1 on PE13 and ETH LTP 6-1 on
BR11.

The P-PNC configures the requested multi-technology single-domain IP link
and, once finished, reports it to the MDSC within the IP topology
exposed at its MPI.

{: #lag-setup}

### Multi-technology LAG Setup

The P-PNC configures a new LAG group between two routers when the
MDSC creates at the MPI a new Ethernet bundled link (using the
bundled-link container defined in {{!RFC8795}}) bundling the multi-technology
single-domain Ethernet link(s) being created, as described above.

When a new LAG link is created, it is also recommended to configure
the minimum number of active member links required to consider the
LAG link as being up. For example, a LAG link with three members can
be considered up when only one member link fails and down when at
least two member links fail.

The attribute required to configure the minimum number of active
member links is missing in {{!I-D.ietf-ccamp-eth-client-te-topo-yang}} and this is identified as a
gap in {{conclusions}}.

It is worth noting that a new LAG group can be created to bundle one
or more multi-technology single-domain Ethernet link(s).

For example, with a reference to {{fig-lag}}, the MDSC can request the
P-PNC2 to setup an Ethernet bundled link between the Ethernet LTP 5-1
on BR21 and the Ethernet LTP 6-1 on P24, bundling the multi-technology
single-domain Ethernet link between the Ethernet LTP 1-1 on BR21 and
the Ethernet LTP 2-1 on P24.

It is worth noting that the MDSC needs to create also the Ethernet
LTPs terminating the Ethernet bundled link.

The MDSC can request the P-PNC to configure a new multi-technology single-domain IP link, supported by the the just configured Ethernet bundled
link, following the same procedure described in {{multi-technology-link-setup}} above.

For example, with a reference to {{fig-lag}}, the MDSC can request the
P-PNC2 to setup a multi-technology single-domain IP Link between IP LTP 5-2 on BR21 and IP LTP 6-2 on P24 supported by the Ethernet bundle link
between ETH LTP 5-1 on BR21 and the Ethernet LTP 6-1 on P24.

### Multi-technology LAG Update

The P-PNC adds new member(s) to an existing LAG group when the MDSC
updates at the MPI the configuration of an existing Ethernet bundled
link adding the multi-technology single-domain Ethernet link(s) being
created, as described above.

When member links are added or removed from a LAG link, the minimum
number of active member links required to consider the LAG link as
being up may also need to be updated.

For example, with a reference to {{fig-lag}}, the MDSC can request the
P-PNC2 to add the multi-technology single-domain Ethernet link setup
between the Ethernet LTP 3-1 on BR21 and the Ethernet LTP 4-1 on P24
to the existing Ethernet bundle link setup between the Ethernet LTP
5-1 on node BR21 and the Ethernet LTP 6-1 on node P24.

After the LAG configuration has been updated, the P-PNC can also
update the bandwidth information of the multi-technology single-domain IP
link supported by the updated Ethernet bundled link.

{: #multi-technology-path-properties}

### Multi-technology TE path properties Configuration

The MDSC can discover the TE path properties (e.g., the list of
SRLGs, the delay) of a multi-technology IP link from the TE properties of:

- the IP LTPs terminating the multi-technology IP link (e.g., the list of
SRLGs reported by the P-PNC using the packet TE topology model);

- the optical path (e.g., the list of SRLGs reported by the O-PNC
using the WDM or OTN tunnel model); and

- the cross-domain links (e.g., the list of SRLGs reported by the O-PNC and P-PNC respectively, using the WSON and/or flexi-grid, the
OTN and the packet TE topology models).

The MDSC can also report this information to the P-PNC by properly
configuring the multi-technology IP link properties using the packet TE
topology model at the packet PNC MPI.

This information is used by the P-PNC at least when computing the
local protection path, as described in {{te-path-config}}, e.g., to ensure
that the local protection path is SRLG disjoint with the primary
path.

It is worth noting that the list of SRLGs for a multi-technology IP link
can be quite long. Implementation-specific mechanisms can be
implemented by the MDSC or by the O-PNC to summarize the SRLGs of an
optical tunnel. These mechanisms are implementation-specific and have
no impact on the YANG models nor on the interoperability at the MPI,
but cares have to be taken to avoid missing information.

{: #te-path-config}

## TE Path Setup and Update

This version of the draft assumes that TE path setup and update at
the MPI could be done using the generic TE tunnel YANG data model,
defined in {{!I-D.ietf-teas-yang-te}}, with packet technology-specific
augmentations, described in {{packet-yang}}.

When a new TE path needs to be setup, the MDSC can use the {{!I-D.ietf-teas-yang-te}}
model to request the P-PNC to set it up, properly specifying
the path constraints, such as the explicit path, to force the P-PNC
to setup an TE path that meets the end-to-end TE and binding
constraints and uses the optical tunnels setup by the MDSC for the
purpose of supporting this new TE path.

The {{!I-D.ietf-teas-yang-te}} model supports requesting the setup of both end-to-end as well as segment TE tunnels (within one domain).

In the latter case, the technology-specific augmentations should
allow the configuration of the information needed for multi-domain TE
path stitching.

For example, the SR-TE specific augmentations of the {{!I-D.ietf-teas-yang-te}}
model should be defined to allow the MDSC to configure the binding
SIDs to be used for the multi-domain SR-TE path stitching and to
allow the P-PNC to report the binding SID assigned to the segment TE
paths. Note that the assigned binding SID should be persistent in
case IP router or P-PNC rebooting.

The MDSC can also use the {{!I-D.ietf-teas-yang-te}} model to request the P-PNC to
increase the bandwidth allocated to an existing TE path, and, if
needed, also on its reverse TE path. The {{!I-D.ietf-teas-yang-te}} model supports
both symmetric and asymmetric bandwidth configuration in the two
directions.

\[Editor's Note:] Add some text about the protection options (to
further discuss whether to put this text here or in {{multi-technology-link-setup}}).

The MDSC also request the P-PNC to configure local protection mechanisms. For example, the FRR local protection, as defined in {{?RFC4090}} in case of MPLS-TE domain or the TI-LFA local protection, as defined in {{?I-D.ietf-rtgwg-segment-routing-ti-lfa}} in case of SR-TE domain. The  mechanisms to request the configuration TI-LFA local protection for SR-TE paths using the {{!I-D.ietf-teas-yang-te}} are a gap in the current YANG models.

The requested local protection mechanisms within the P-PNC domain are
configured by the P-PNC through implementation specific mechanisms
which are outside the scope of this document.

The P-PNC takes into account the multi-layer TE path properties
(e.g., SRLG information), configured by the MDSC as described in
{{multi-technology-path-properties}}, when computing the protection configuration (e.g., in
case of SR-TE domains, the TI-LFA post-convergence path or, in case of MPLS-TE domain, the FRR backup tunnel) for multi-technology single-domain IP links.

SR-TE path setup and update (e.g., bandwidth increase) through MPI is
identified as a gap requiring further work, which is outside of the
scope of this draft.

{: #vpn-setup}

## L2/L3 VPN Network Service Setup

The MDSC can use the L2NM and L3NM network service models to request
the P-PNCs to setup L2/L3 VPN services and the L2NM and L3NM TE
service mapping models to request the P-PNCs to configure the PE
routers to steer the L2/L3 VPN traffic to the selected TE tunnels
(e.g., MPLS-TE or SR-TE).

It is worth noting that the L2NM and L3NM TE service mapping models,
defined in {{?I-D.ietf-teas-te-service-mapping-yang}}, provide a list of TE tunnel(s) that should be used
to forward L2/L3 VPN traffic between the two PEs terminating the
listed TE tunnel(s). If the list contains more than one TE tunnel for
the same pair of PEs, these TE tunnels are used for load balancing
the associated L2/L3 VPN traffic between the same set of two PEs.

The possibility to request splitting the traffic, between multiple TE
tunnels for the same PEs pair, in a different way than load balancing
is identified as a gap requiring further work and outside of the
scope of this draft.

{: #conclusions}

# Conclusions

The analysis provided in this document has shown that the IETF YANG
models described in 3.2 provides useful support for Packet Optical
Integration (POI) scenarios for resource discovery (network topology,
service, tunnels and network inventory discovery) as well as for
supporting multi-layer/multi-domain L2/L3 VPN network services.

Few gaps have been identified to be addressed by the relevant IETF
Working Groups:

- how both WSON and Flexi-grid topology models could be used
together (through multi-inheritance): this gap has been identified
in {{optical-topology-discovery}};.

- network inventory model: this gap has been identified in
{{inventory-discovery}} and the solution in {{?I-D.ietf-ivy-network-inventory-yang}} has been proposed to
resolve it;

- technology-specific augmentations of the path computation RPC,
defined in {{!I-D.ietf-teas-yang-path-computation}} for optical networks: this gap has been
identified in {{optical-path-computation}} and the solution in {{?I-D.ietf-ccamp-optical-path-computation-yang}}
has been proposed to resolve it;

- relationship between a common discovery mechanisms applicable to
access links, inter-domain IP links and Cross-technology links and the
UNI topology discover mechanism defined in {{?RFC9408}}: this gap has
been identified in {{packet-topology-discovery}};

- a mechanism applicable to the P-PNC NBI to configure the SR-TE
paths. Technology-specific augmentations of TE Tunnel model,
defined in {{!I-D.ietf-teas-yang-te}}, are foreseen in section 1 of {{!I-D.ietf-teas-yang-te}}
but not yet defined: this gap has been identified in {{te-path-config}};

- an attribute, which is used to configure the minimum number of
active member links required to consider the LAG link as being up,
is missing from the topology model defined in {{!I-D.ietf-ccamp-eth-client-te-topo-yang}}: this
gap has been identified in {{lag-setup}};

- a mechanism to configure splitting the L2/L3 VPN traffic, between
multiple TE tunnels for the same PEs pair, in a different way than
load balancing: this gap has been identified in {{vpn-setup}};

- a mechanism to report client connectivity constraints imposed by
some muxponder design: this gap has been identified in {{muxponder}}.

Although not applicable to this document, it has been noted that
being able to use WSON and Flexi-grid topology models together
(through multi-inheritance) is not only useful in cases of mixed
fixed-grid and flexible-grid DWDM network topology but also the only
viable option in case of a mixed CWDM and DWDM network topology.

Although not applicable to this document, it has been noted that the
WDM tunnel model would support also optical tunnel setup in case of a
mixed CWDM and DWDM network topology.

Although not analysed in this document, it has been noted that the TE
Tunnel model, defined in {{!I-D.ietf-teas-yang-te}}, needs also to be enhanced to
support scenarios where multiple parallel TE paths are used in load-balancing to carry the traffic between two end-points (e.g., VPN
traffic between two PEs).

# Security Considerations {#security}

This document highlights how the ACTN architecture can deploy packet
over optical infrastructure services. It highlights how existing IETF
protocols and data models may be used for multi-layer services. It
reuses several existing IETF protocols and data models for the MPI
interfaces between each PNC (Optical or Packet) and the MDSC,
including:

- RESTCONF

- NETCONF

- PCEP

- YANG

Several existing authentication and encryption practices and
techniques may be used to help secure these MPI interfaces. These
mechanisms include using Transport Layer Security (TLS) to provide
secure transport for RESTCONF, NETCONF and PCEP. Furthermore, access
control techniques can also provide additional security. NETCONF
supports an Access Control Model (NACM), and RESCONF supports Role
Based Access Control (RBAC), which should also ensure that MDSC to
PNC communication is based on authorised use and granular control of
connectivity and resource requests.

## LLDP Snooping Security Considerations

Earlier in the document, LLDP is discussed as a mechanism for the PNCs to discover the intra-domain Ethernet and IP links. While LLDP provides valuable information for network management and troubleshooting, it also presents several security issues:

- Eavesdropping: LLDP transmissions are not encrypted. Potentially, LLDP packets could be captured using a packet sniffer. An attacker can leverage this information to gain insights into the network topology, device types, and configurations, which could be used for further attacks;

- Unauthorized Access: Information disclosed by LLDP can include device types, software versions, and network configuration details. This might help an attacker identify vulnerable devices or configurations that can be exploited to gain unauthorized access or escalate privileges within the network;

- Data Manipulation: If an attacker gains access to a network device, they could manipulate LLDP information to advertise false device information, leading to potential misconfigurations or trust relationships being exploited. This can disrupt network operations or redirect traffic to malicious devices;

- Denial of Service (DoS): By flooding the network with fake LLDP packets, an attacker could overwhelm network devices or management systems, potentially leading to a denial of service where legitimate network traffic is disrupted;

- Spoofing: An attacker could spoof LLDP packets to impersonate other network devices. Potentially, this might lead to incorrect network mappings or trust relationships being established with malicious devices;

- Lack of Authentication: LLDP does not include mechanisms for authenticating the source of LLDP messages, which means that devices accept LLDP information from any source as legitimate.

To mitigate these security issues, network administrators might implement several security measures, including:

- Disabling LLDP on ports where it is not needed, especially those facing untrusted networks;

- Using network segmentation and Access Control Lists (ACLs) to limit who can send and receive LLDP packets;

- Employing network monitoring and anomaly detection systems to identify unusual LLDP traffic patterns that may indicate an attack;

- Regularly updating and patching network devices to address known vulnerabilities that could be exploited through information gathered via LLDP.

# Operational Considerations

This document has identified the need and enabling components for automating the management and control of multi-layer Service Providers' transport networks, combining the optical and microwave transport layer with the packet (IP/MPLS) layer to create a more efficient and scalable network infrastructure. This approach is particularly beneficial for Service Providers and large enterprises dealing with high bandwidth demands and looking for cost-effective ways to expand their networks. However, integrating these two traditionally separate network layers involves several operational considerations:

- Network Design and Capacity Planning: Deciding the degree of integration between the packet and optical layers is critical. Furthermore, this includes determining whether to pursue a loose integration (keeping layers distinct but coordinated) or a tight integration (combining layers more closely, potentially at the hardware level) coordinated via the MDSC. Accurate forecasting and planning will also be essential to ensure that the integrated ACTN infrastructure can handle future capacity demand without excessive over-provisioning;

- System Interoperability: Networks often comprise equipment from various vendors. Ensuring that packet and optical devices can interoperate seamlessly and the PNCs can manage them is crucial for a successful integration. The Service Provider must also check with the vendors to ensure they support the IETF-based technologies outlined in this document;

- Performance Monitoring: The integrated POI network will require comprehensive monitoring solutions that can provide visibility to the PNCs across both packet and optical layers. Identifying and diagnosing issues may become more complex with integrated layers. Telemetry data may also be required to collect lower-layer networking health and consider network and service performance. This topic is further discussed in [ACTN Assurance];

- Fault Management and Recovery: The POI networks should be resilient, including considerations for automatic protection switching and fast reroute mechanisms that span both layers. Fault isolation and recovery may become more challenging, as issues in one layer can have cascading effects on the other. Effective fault management strategies must be in place to quickly identify and rectify such issues. This topic is further discussed in [ACTN Assurance];

Specific Security Considerations are discussed in {{security}}.

# IANA Considerations

This document requires no IANA actions.

--- back

{: #additional-scenarios}

# Additional Scenarios

## OSS/Orchestration Layer

The OSS/Orchestration layer is a vital part of the architecture
framework for a service provider:

- to abstract (through MDSC and PNCs) the underlying transport
network complexity to the Business Systems Support layer;

- to coordinate NFV, Transport (e.g. IP, optical and microwave
networks), Fixed Acess, Core and Radio domains enabling full
automation of end-to-end services to the end customers;

- to enable catalogue-driven service provisioning from external
applications (e.g. Customer Portal for Enterprise Business
services), orchestrating the design and lifecycle management of
these end-to-end transport connectivity services, consuming IP
and/or optical transport connectivity services upon request.

As discussed in {{mdsc-overview}}, in this document, the MDSC interfaces
with the OSS/Orchestration layer and, therefore, it performs the
functions of the Network Orchestrator, defined in {{?RFC8309}}.

The OSS/Orchestration layer requests the creation of a network
service to the MDSC specifying its end-points (PEs and the interfaces
towards the CEs) as well as the network service SLA and then proceeds
to configuring accordingly the end-to-end customer service between
the CEs in the case of an operator managed service.

### MDSC NBI

As explained in {{reference-network}}, the OSS/Orchestration layer can request
the MDSC to setup L2/L3VPN network services (with or without TE
requirements).

Although the OSS/Orchestration layer interface is usually operator-specific, typically it would be using a RESTCONF/YANG interface with
a more abstracted version of the MPI YANG data models used for
network configuration (e.g. L3NM, L2NM).

{{fig-service-request}} shows an example of possible control flow between the
OSS/Orchestration layer and the MDSC to instantiate L2/L3 VPN network
services, using the YANG data models under the definition in {{?I-D.ietf-teas-actn-vn-yang}},
{{?RFC9291}}, {{?RFC9182}} and {{?I-D.ietf-teas-te-service-mapping-yang}}.

{::include ./figures/service-request.md}
{: #fig-service-request title="Service Request Process"}

- The VN YANG data model, defined in {{?I-D.ietf-teas-actn-vn-yang}}, whose primary focus is
the CMI, can also provide VN Service configuration from an
orchestrated network service point of view when the L2/L3 VPN
network service has TE requirements. However, this model is not
used to setup L2/L3 VPN service with no TE requirements.

   - It provides the profile of VN in terms of VN members, each of
   which corresponds to an edge-to-edge link between customer
   end-points (VNAPs). It also provides the mappings between the
   VNAPs with the LTPs and the connectivity matrix with the VN
   member. The associated traffic matrix (e.g., bandwidth,
   latency, protection level, etc.) of VN member is expressed
   (i.e., via the TE-topology's connectivity matrix).

   - The model also provides VN-level preference information (e.g.,
   VN member diversity) and VN-level admin-status and
   operational-status.

- The L2NM and L3NM YANG data models, defined in {{?RFC9291}} and
{{?RFC9182}}, whose primary focus is the MPI, can also be used to
provide L2VPN and L3VPN network service configuration from a
orchestrated connectivity service point of view.

- The TE & Service Mapping YANG data model {{?I-D.ietf-teas-te-service-mapping-yang}} provides TE-service
mapping.

- TE-service mapping provides the mapping between a L2/L3 VPN
instance and the corresponding VN instances.

- The TE-service mapping also provides the binding requirements
as to how each L2/L3 VPN/VN instance is created concerning the
underlay TE tunnels (e.g., whether they require a new and
isolated set of TE underlay tunnels or not).

- Site mapping provides the site reference information across
L2/L3 VPN Site ID, VN Access Point ID, and the LTP of the
access link.

## Multi-layer and Multi-domain Resiliency

### Maintenance Window

Before planned maintenance operation on DWDM network takes place, IP
traffic should be moved hitless to another link.

MDSC must reroute IP traffic before the events takes place. It should
be possible to lock IP traffic to the protection route until the
maintenance event is finished, unless a fault occurs on such path.

### Router Port Failure

The focus is on client-side protection scheme between IP router and
reconfigurable ROADM. Scenario here is to define only one port in the
routers and in the ROADM muxponder board at both ends as back-up
ports to recover any other port failure on client-side of the ROADM
(either on the IP router port side or on the muxponder side or on the link
between them). When client-side port failure occurs, alarms are
raised to MDSC by IP-PNC and O-PNC (port status down, LOS etc.). MDSC
checks with OP-PNC(s) that there is no optical failure in the optical
layer.

There can be two cases here:

1. LAG was defined between the IP routers at the two ends. MDSC, after checking
that optical layer is fine between the two edge WDM nodes, triggers
the WDM edge node re-configuration so that the IP router's back-up port with its
associated muxponder port can reuse the WDM tunnel that was already in
use previously by the failed IP router port and adds the new link to
the LAG on the failure side.

   While the ROADM reconfiguration takes place, IP/MPLS traffic is
   using the reduced bandwidth of the IP link bundle, discarding
   lower priority traffic if required. Once back-up port has been
   reconfigured to reuse the existing WDM tunnel and the new link has been added
   to the LAG then original Bandwidth is recovered between the end
   routers.

   Note: in this LAG scenario let assume that BFD is running at LAG
   level so that there is nothing triggered at MPLS level when one of
   the link member of the LAG fails.

1. If there is no LAG then the scenario is not clear since a IP router
port failure would automatically trigger (through BFD failure)
first a sub-50ms protection at MPLS level :FRR (MPLS RSVP-TE case)
or TI-LFA (MPLS based SR-TE case) through a protection port. At
the same time MDSC, after checking that optical network connection
is still fine, would trigger the reconfiguration of the back-up
port of the IP router and of the muxponder to re-use the same
WDM tunnel as the one used originally for the failed IP router port. Once
everything has been correctly configured, MDSC Global PCE could
suggest to the operator to trigger a possible re-optimization of
the back-up MPLS path to go back to the  MPLS primary path through
the back-up port of the IP router and the original WDM tunnel if overall
cost, latency etc. is improved. However, in this scenario, there
is a need for protection port PLUS back-up port in the IP router
which does not lead to clear port savings.

{: #muxponder}

## Muxponders

The setup of a client connectivity service between two transponders
is relatively clear and its implementation simple.

There is a one to one relationship between the tranponder's client
and trunk (or DWDM) port. The client port bitrate determines the
trunk port bit rate which will also determine the Baud-rate, the
modulation format, the FEC etc.

The controller, when asked to set up a client connectivity service,
needs to find a WDM tunnel suitable to comply the DWDM port
parameters.

The setup of a client connectivity service between two muxponders is
different since there is a one to many relationship between the
muxponder's trunk (or DWDM) port and client ports. For example, there
might be a 100Gb/s trunk port shared by ten 10GE client ports.

The controller, when asked to set a 10GE client connectivity service
between two muxponder's client ports, needs first to check whether
there is already an existing WDM tunnel between the two muxponders
and then take different actions:

1. if the WDM tunnel already exists, the controller needs only to
enable the 10GE client ports to establish the 10GE client
connectivity service;

2. if the WDM tunnel does not exist, the controller has to first
establish the WDM tunnel, finding a proper optical path matching
the optical parameters of the two muxponders' trunk ports (e.g.,
an OTSi carrying an OTU4), and then enable the 10GE client ports
to establish the 10GE client connectivity service.

Since multiple client connectivity services are sharing the same WDM
tunnel, a multiplexing label shall be assigned to each client
connectivity service. The multiplexing label can either be a standard
label (e.g., an OTN timeslot) or a vendor-specific label. The
multiplexing label can be either configurable (flexible
configuration) or assigned by design to each muxponder's client port
(fixed configuration). In the former case, any muxponder client port
can be connected with any other client port of the peer muxponder
(for example client port 1 on one muxponder can be connected with
client port 5 on the peer muxponder) while in the latter case only
client ports with the same port number can be connected (for example
client port 2 on one muxponder can be connected only with client port
2 on the peer muxponder and not with any other client port).

In case of flexible configuration, since the two muxponders are under
the control of the same O-PNC, the configuration of the multiplexing
label, regardless of whether it is a standard or vendor-specific
label, can be done by the O-PNC using mechanisms which are vendor-specific and outside the scope of this document. The MDSC can just
request the O-PNC to setup a client connectivity service over a WDM
tunnel.

In case of fixed configuration, the multiplexing label is assigned by
the muxponder but the O-PNC and MDSC needs to be aware of the
connectivity constraints to avoid try and fail.

It is worth noting that the current WSON and Flexi-grid topology
models in {{!RFC9094}} and {{!I-D.ietf-ccamp-flexigrid-yang}} do not provide sufficient
information to the MDSC about this connectivity constraint and this
is identified as a gap.

{: numbered="false"}

# Acknowledgments

Some of this analysis work was supported in part by the European
Commission funded H2020-ICT-2016-2 METRO-HAUL project (G.A. 761727).

Previous versions of document were prepared using 2-Word-v2.0.template.dot.

This document was prepared using kramdown.
