---
id: staking-ssn-setup
title: Setting up the SSN
keywords:
  - staking
  - getting started
  - seed node
  - launching node
  - zilliqa
description: Setting up the SSN
---

---

import Tabs from '@theme/Tabs'; import TabItem from '@theme/TabItem';

!!! info

    The Mainnet has been upgraded to support staking phase 1.1. You can now start to run a staked seed node on the Mainnet.

## Default Port Requirements for SSNs

Before preparing to host an SSN, please note that these are the ports that
**must** be enabled in the SSN:

| Type     | Default  | Purpose                                                                   |
| -------- | -------- | ------------------------------------------------------------------------- |
| Inbound  | 33133    | Protocol level port for receiving network data                            |
| Inbound  | 4201/443 | [API service](https://dev.zilliqa.com/api/introduction/api-introduction/) |
| Inbound  | 4501     | Staking API service                                                       |
| Outbound | 443      | For getting initial node data for syncing                                 |

Additionally, there are ports that **may** be enabled in the SSN:

| Type    | Default | Purpose                                                                             |
| ------- | ------- | ----------------------------------------------------------------------------------- |
| Inbound | 4401    | [WebSocket service](../../../developers/developer-toolings/dev-tools-websockets.md) |

## Preparing the Node

Launching a seed node for staking is similar to launching a normal seed node
using
[key whitelisting mode (option 1)](../../../exchanges/exchange-integration/getting-started/exchange-key-whitelisting-1.md),
with some additional configuration steps.

1. First, please verify that your SSN meets the
   [minimum hardware requirements](../../../exchanges/exchange-integration/getting-started/exchange-introduction.md#minimum-hardware-requirements).
1. Follow the steps for launching a seed node using
   [key whitelisting mode (option 1)](../../../exchanges/exchange-integration/getting-started/exchange-key-whitelisting-1.md),
   except use `ssn-configuration.tar.gz` instead of `seed-configuration.tar.gz`.

!!! caution

    Step 2 above includes generating a key pair for launching the seed
    node. We highly recommend **not** to use the same key pair for depositing stake,
    withdrawing stake and withdrawing reward.

### Configuring Domain Name

Once your seed node is fully set up, it is time to configure your domain name to
point to the address of your seed node.

- If your seed node is not behind a load balancer, you can set an `A record`
  in your domain registrar to point your domain/subdomain to your seed node’s
  IP address.
- If your seed node is behind a load balancer, you can set a `CNAME record` in
  your domain registrar to point your domain/subdomain to the hostname of your
  load balancer.

### SSL/TLS Configuration

As the staked seed nodes are for public consumption, we expect these nodes to
have high availability and be secure and reliable. As such, all operators are
required to support serving of API and raw data requests over SSL/TLS.

## Advanced Setup

Different node operators may wish to have a different setup to secure their SSN.
It is possible as long as:

1. JSON-RPC port (by default 4201) and WebSocket port are accessible by anyone
   without any restriction
1. Staking API port (by default 4501) is accessible by the verifier to check the
   SSN

SSN operators are allowed to:

- Change the default port numbers (please inform us)
- Add a load balancer in front of their node
- Add additional services such as Cloudflare proxy in front of the node
- Run more than 1 SSN node behind a load balancer (these will collectively be
  treated as a single SSN)

SSN operators are not allowed to:

- Outsource API service to other node operators or Zilliqa seed nodes
- Restrict or censor any API service to the public or any region
