# Awesome FreeSWITCH [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> Software defined telecom stack for voice, video and messaging applications.

FreeSWITCH gives you a modular media engine with call control over a socket. What you put around it, the interface, the SIP edge, the monitoring, the speech engines, comes from the ecosystem. This list covers that ecosystem, plus the SIP and media components FreeSWITCH is normally deployed alongside.

Every entry was checked against its own repository before being listed. Projects with no commits in the last year are left out, and come out when that becomes true, because a directory that lists dead software costs people more time than it saves.

## Contents

- [Official](#official)
- [Distributions and web interfaces](#distributions-and-web-interfaces)
- [Platforms built on FreeSWITCH](#platforms-built-on-freeswitch)
- [Containers and deployment](#containers-and-deployment)
- [Event Socket libraries](#event-socket-libraries)
- [Streaming call audio and voice AI](#streaming-call-audio-and-voice-ai)
- [SIP proxies and session border control](#sip-proxies-and-session-border-control)
- [Media and RTP](#media-and-rtp)
- [Testing, monitoring and troubleshooting](#testing-monitoring-and-troubleshooting)
- [Security](#security)
- [Contact centre, dialling and fax](#contact-centre-dialling-and-fax)
- [Billing](#billing)
- [WebRTC and endpoints](#webrtc-and-endpoints)
- [Learning](#learning)

## Official

- [FreeSWITCH](https://github.com/signalwire/freeswitch) - The softswitch itself. Modules, dialplan, the Event Socket and the media core everything else is built on.
- [FreeSWITCH documentation](https://developer.signalwire.com/freeswitch/) - The current home of the documentation, including the module reference and the Event Socket protocol.
- [freeswitch-docs](https://github.com/signalwire/freeswitch-docs) - Source for that documentation, so fixes can go in as pull requests.
- [Sofia-SIP](https://github.com/freeswitch/sofia-sip) - The SIP user agent library FreeSWITCH is built on, maintained by the project since the original upstream went quiet.
- [SpanDSP](https://github.com/freeswitch/spandsp) - DSP library behind mod_spandsp, covering fax modulation, tone detection and echo cancellation.
- [FreeSWITCH community forum](https://forum.signalwire.community/) - Where the maintainers and long-time users answer questions.

## Distributions and web interfaces

- [FusionPBX](https://github.com/fusionpbx/fusionpbx) - The multi-tenant web interface most people run on top of FreeSWITCH: domains, extensions, IVR, queues, call recordings and a dialplan editor. MPL-1.1, stated in the file headers rather than a LICENSE file.
- [ICTPBX Community Edition](https://github.com/ictinnovations/ictpbx-community-edition) - Multi-tenant PBX packaging FreeSWITCH and FusionPBX with a REST API and an Angular front end, for people who want to build on the PBX rather than only administer it.

## Platforms built on FreeSWITCH

Projects where FreeSWITCH is the media engine under something larger. Useful both as products and as worked examples of how to drive it at scale.

- [jambonz](https://github.com/jambonz/jambonz-feature-server) - Open source CPaaS combining drachtio for SIP and FreeSWITCH for media, with a webhook and WebSocket API in the style of the commercial platforms.
- [BigBlueButton](https://github.com/bigbluebutton/bigbluebutton) - Web conferencing for teaching, which uses FreeSWITCH for its audio mixing. The biggest single deployment base of FreeSWITCH conferencing.
- [ICTCore](https://github.com/ictinnovations/ictcore) - Communications framework exposing FreeSWITCH voice, fax and messaging as a REST API and programmable call flows.

## Containers and deployment

- [freeswitch-docker](https://github.com/PatrickBaus/freeswitch-docker) - Alpine based image built from source, small enough for development and rebuilt as upstream moves.
- [Official Dockerfiles](https://github.com/signalwire/freeswitch/tree/master/docker) - Debian based images kept in the FreeSWITCH repository itself.
- [fusionpbx-install.sh](https://github.com/fusionpbx/fusionpbx-install.sh) - The maintained install scripts for FreeSWITCH plus FusionPBX on Debian, and the closest thing to a reference build.
- [ansible-role-ictpbx](https://github.com/ictinnovations/ansible-role-ictpbx) - Ansible role that installs FreeSWITCH, FusionPBX and ICTCore as a working multi-tenant PBX.

## Event Socket libraries

The Event Socket is how external code controls FreeSWITCH. The bindings that ship in tree cover C, Python, Lua, Java, PHP, Perl, Ruby and Tcl. The ones below are separate projects that are still maintained.

- [ESL in tree](https://github.com/signalwire/freeswitch/tree/master/libs/esl) - The reference client library and fs_cli, with the SWIG bindings for the languages above.
- [greenswitch](https://github.com/EvoluxBR/greenswitch) - Python client built on gevent, used in production dialers for years.
- [eslgo](https://github.com/percipia/eslgo) - Go library covering inbound and outbound socket modes with typed events.
- [freeswitch-esl-node](https://github.com/ictinnovations/freeswitch-esl-node) - Dependency-free typed client for Node.js.
- [freeswitch-esl](https://github.com/ZmoleCristian/freeswitch-esl) - Async client for Rust.

## Streaming call audio and voice AI

Getting live call audio into your own process is the starting point for transcription, agent assist and voice agents.

- [mod_audio_stream](https://github.com/amigniter/mod_audio_stream) - Streams a channel's audio to a WebSocket and plays returned audio back, which is the usual bridge between FreeSWITCH and a speech service.
- [Whisper](https://github.com/openai/whisper) - Speech recognition models that changed what is affordable in this space.
- [whisper.cpp](https://github.com/ggml-org/whisper.cpp) - The port that made Whisper practical on ordinary CPUs, which is what most people run next to a switch.
- [Vosk](https://alphacephei.com/vosk/) - Lightweight offline speech recognition with streaming support and small models, well suited to telephony audio.
- [Piper](https://github.com/OHF-Voice/piper1-gpl) - Fast local neural text to speech, light enough to run per channel.

## SIP proxies and session border control

Signalling at carrier volume is a different job from running a switch, and putting a proxy in front of FreeSWITCH is how most large deployments are built.

- [Kamailio](https://github.com/kamailio/kamailio) - SIP proxy, registrar and router built for very high signalling throughput.
- [OpenSIPS](https://github.com/OpenSIPS/opensips) - The other branch of the same lineage, strong on session border control and provider-side routing.
- [drachtio-server](https://github.com/drachtio/drachtio-server) - SIP server controlled from Node.js, and the signalling half of jambonz.
- [Routr](https://github.com/fonoster/routr) - Newer SIP server built around a declarative configuration and an API.

## Media and RTP

- [rtpengine](https://github.com/sipwise/rtpengine) - Kernel assisted RTP proxy and media relay, handling NAT traversal, recording and transcoding at volume.
- [coturn](https://github.com/coturn/coturn) - The STUN and TURN server nearly every WebRTC deployment ends up running.
- [libsrtp](https://github.com/cisco/libsrtp) - The SRTP implementation FreeSWITCH links against for encrypted media.
- [bcg729](https://github.com/BelledonneCommunications/bcg729) - Open source G.729 codec, now patent free, which is what the community G.729 modules wrap.

## Testing, monitoring and troubleshooting

- [SIPp](https://github.com/SIPp/sipp) - Traffic generator and test tool for SIP. Still the standard way to load test a signalling path.
- [sngrep](https://github.com/irontec/sngrep) - Terminal SIP capture with call flow diagrams. The fastest way to see what is happening on a box you are logged into.
- [sipexer](https://github.com/miconda/sipexer) - Command line SIP client for sending arbitrary requests, useful for scripted checks against a switch.
- [HOMER](https://github.com/sipcapture/homer) - SIP capture and correlation across a whole estate, so you can reconstruct one call across every hop.
- [heplify](https://github.com/sipcapture/heplify) - Lightweight HEP capture agent that feeds HOMER.
- [VoIPmonitor](https://github.com/voipmonitor/sniffer) - Packet sniffer that records SIP and RTP and scores call quality. The sniffer is GPL-2.0; the web interface usually paired with it is commercial.
- [freeswitch_exporter](https://github.com/florentchauveau/freeswitch_exporter) - Prometheus exporter that polls FreeSWITCH over the Event Socket, for dashboards and alerting on call volume.
- [pbx-mcp](https://github.com/ictinnovations/pbx-mcp) - MCP server that lets an AI assistant query a live FreeSWITCH over the Event Socket: channels, registrations and gateway status. Read-only by default.

## Security

- [SIPVicious](https://github.com/EnableSecurity/sipvicious) - The security tool suite for auditing SIP systems. Run it against your own before someone else does.
- [SIPPTS](https://github.com/Pepelux/sippts) - Actively developed toolkit for scanning, enumerating and testing SIP services, including checks for published VoIP CVEs.
- [Mr.SIP](https://github.com/meliht/Mr.SIP) - SIP audit and attack toolkit for testing how a deployment holds up against enumeration, spoofing and flooding.

## Contact centre, dialling and fax

- [mod_callcenter](https://developer.signalwire.com/freeswitch/FreeSWITCH-Explained/Modules/mod_callcenter_1049389/) - The in-tree queue and agent module, which is further along than most people expect before they reach for something external.
- [ICTDialer](https://github.com/ictinnovations/ictdialer) - Voice broadcasting and auto dialler over FreeSWITCH, with SMS and fax campaigns on the same contact lists.
- [ICTFax](https://github.com/ictinnovations/ictfax) - Fax server over FreeSWITCH and mod_spandsp, with T.38, a web interface and a REST API.

## Billing

- [CGRateS](https://github.com/cgrates/cgrates) - Real-time rating and charging engine with a FreeSWITCH agent, for prepaid balances and per-call rating without writing your own.

## WebRTC and endpoints

- [Verto](https://developer.signalwire.com/freeswitch/FreeSWITCH-Explained/Modules/mod_verto_3964934/) - FreeSWITCH's own WebRTC signalling module and JavaScript client, which skips SIP entirely between browser and switch.
- [JsSIP](https://github.com/versatica/JsSIP) - JavaScript SIP over WebSocket library for building browser phones against mod_sofia.
- [SIP.js](https://github.com/onsip/SIP.js) - The other widely used JavaScript SIP library, with a simpler API for common cases.
- [Linphone](https://github.com/BelledonneCommunications/linphone-desktop) - SIP client across desktop and mobile with encrypted voice and video, and a library you can embed.
- [baresip](https://github.com/baresip/baresip) - Modular SIP user agent, useful both as a scriptable endpoint and as a base for custom clients.
- [Telephone](https://github.com/64characters/Telephone) - Native macOS SIP client, still actively developed, which is rarer on that platform than it should be.

## Learning

- [ClueCon](https://www.cluecon.com/) - The FreeSWITCH developer conference. Past talks are the best long-form material on the internals.
- [sip-resources](https://github.com/miconda/sip-resources) - Curated links on SIP, RTP and WebRTC from the Kamailio lead, which is the protocol background FreeSWITCH work assumes.

## Footnotes

This list is maintained by [ICT Innovations](https://www.ictinnovations.com), who also build some of the software on it. Entries we maintain are `ictpbx-community-edition`, `ictcore`, `ictfax`, `ictdialer`, `freeswitch-esl-node`, `pbx-mcp` and `ansible-role-ictpbx`. They are held to the same bar as everything else and can be challenged in an issue like any other entry.

## Contributing

Contributions are welcome. Read the [contribution guidelines](contributing.md) first, and please open one pull request per entry.
