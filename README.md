# Tortuga Protocol & Grail Verification Engine Specification
**Document Version:** 1.0.4-draft  
**Status:** Working Group Draft  
**Lead Architect:** V. V. Cherniak  
**Framework Integration:** Aerocap.media Architecture  

---

## 1. Executive Overview

The Tortuga Protocol defines an open, deterministic specification for linking cryptographic content provenance (C2PA v1.3) directly to HTTP-level transaction headers (x402 payment state). It solves the post-facto audit problem in cross-border synthetic and AI-generated media licensing.

The Grail Verification Engine acts as the zero-knowledge validation layer, evaluating ODRL 2.2 rights compliance at the node level before finalizing state clearing across multi-jurisdictional frameworks (UK Common Law, UAE DIFC, US Delaware).

---

## 2. Architecture Diagram

+-------------------+      1. Request Payload + Hash      +--------------------+
|  Media Consumer   | ----------------------------------> |   Tortuga Node     |
+-------------------+                                     +--------------------+
          |                                                         |
          | 2. HTTP 402 Payment Required                            | 3. Query Provenance
          |    (x402 Header with ODRL Policy Hash)                  v
          v                                               +--------------------+
+-------------------+                                     |   C2PA Manifest    |
| Payment Gateway   |                                     |  & IPFS Storage    |
+-------------------+                                     +--------------------+
          |                                                         |
          | 4. Settled Tx Hash                                      | 5. Validate Rules
          v                                                         v
+------------------------------------------------------------------------------+
|                         Grail Verification Engine                            |
|     (Validates Metadata Integrity & Triggers Multi-Party Royalty Split)       |
+------------------------------------------------------------------------------+

---

## 3. Protocol Flow & HTTP x402 Extension

When a client requests a licensed asset, the node intercepts the request and responds with an x402 header bound to the asset's C2PA manifest hash:

HTTP/1.1 402 Payment Required
X-402-Protocol-Version: 1.0-tortuga
X-402-Asset-Hash: ipfs://bafybeigdyr3225f26nn54vxm832...
X-402-ODRL-Policy: https://aerocap.media/policies/v1/commercial-use.json
X-402-Royalty-Split: 0x71C...892:0.70,0x3C4...118:0.30

### Settlement Mechanics
1. Payload Verification: Grail Engine inspects C2PA signature chain (ES256 / Ed25519).
2. Policy Evaluation: ODRL policy parameters (permitted actions, spatial constraints, redistribution rights) are compiled into a deterministic state rule.
3. Execution: Upon receipt of cryptographic proof-of-payment, funds are routed directly to split addresses without intermediary escrow delay.

---

## 4. Jurisdiction & Compliance Bindings

* UK Common Law: Contractual binding via automated digital offer-and-acceptance mechanisms.
* UAE (DIFC): Compliance with DIFC Digital Assets Law No. 2 of 2024 for digital asset tokenization and settlement.
* US (Delaware): Inter-entity corporate IP assignment compatibility under Delaware General Corporation Law (DGCL).

---

## 5. Reference Implementation & Testing

To validate a C2PA payload against a Tortuga policy header using the local Grail CLI binary:

# Install local verifier tool
curl -sSL https://raw.githubusercontent.com/aerocap/tortuga-spec/main/install.sh | bash

# Run verification check on media file
grail-cli verify --input sample_asset.mp4 --policy policy_commercial.json

---

## 6. Citation & Attribution

When citing this specification in legal or technical frameworks, please use:

Cherniak, V. V., Evans, M., Thorne, A. (2025). Practical Infrastructure for Automated Media Licensing and Cross-Border Royalty Settlement. Technical Report No. 2025-4B. International Media & Rights Working Group.
