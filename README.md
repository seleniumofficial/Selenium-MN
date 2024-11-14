
---

# Masternode Setup Guide

This guide will walk you through the essential steps to set up your masternode. Please follow each step carefully, using the wallet and console commands provided.

---

### Step 1: Prepare Your Addresses

Gather the following addresses from your wallet. Each address has a specific role:

- **Masternode Collateral Address**: `SRrfbPvmgds7XFvU4xhsCVegDM4Do6EyYp`
- **Fee Address**: `SHu7BFFtfsU3FgfUX1y5JnAQNVZ28348UK`
- **Owner Address**: `S6ZhT7SR1BQSUYrab3isCGEmJGwndSxGod`
- **Voting Address**: `S5HXmW9iYzZq89LdH8eUXEzSwwwEaQ3XKS`
- **Masternode Reward Address**: `SLvahoF6T7b8NY5wACtDoS9NzWPjRhNKuL`

Each address has a unique function, so make sure to keep them organized.

---

### Step 2: Create Collateral and Fee Transactions

Use your wallet to initiate both the collateral and fee transactions. These transactions are essential to set up the masternode.

---

### Step 3: Generate Collateral Transaction Output

Run this command in your wallet console to get the output from your collateral transaction:

```bash
masternode outputs
```

Example output:

```json
{
 "618599438df959fc0647ad1895808ba0fef96282bf24eb177134cb0c329c8d41": "1"
}
```

Take note of both the **Transaction ID** and **Output Index** (the single-digit number).

---

### Step 4: Generate BLS Key Pair

Run this command in your wallet console to generate a BLS (Basic Lightning Storage) key pair for your masternode:

```bash
bls generate
```

Example output:

```json
{
 "secret": "5120af1f913b8a4b459e19cc3ef3f865ba891404853fa317f348635b347e12ef",
 "public": "050564992464a87643d273e87334fda1e8beb52e9605b9cef2fe73eb3a063f12c8f03a6fa4f07e26a1e9e5175e155c91"
}
```

Keep the **public key** for the next steps.

---

### Step 5: Prepare the Masternode Transaction

Use the following command to prepare your masternode transaction:

```bash
protx register_prepare 618599438df959fc0647ad1895808ba0fef96282bf24eb177134cb0c329c8d41 1 159.89.31.63:12010 S6ZhT7SR1BQSUYrab3isCGEmJGwndSxGod 050564992464a87643d273e87334fda1e8beb52e9605b9cef2fe73eb3a063f12c8f03a6fa4f07e26a1e9e5175e155c91 S5HXmW9iYzZq89LdH8eUXEzSwwwEaQ3XKS 0 SLvahoF6T7b8NY5wACtDoS9NzWPjRhNKuL SHu7BFFtfsU3FgfUX1y5JnAQNVZ28348UK
```

#### Explanation of Parameters:

- **Transaction ID** (`618599...c8d41`): From `masternode outputs`.
- **Output Index** (`1`): From `masternode outputs`.
- **VPS IP** (`159.89.31.63:12010`): Your server’s external IPv4.
- **Owner Address** (`S6ZhT7SR1BQSUYrab3isCGEmJGwndSxGod`): Address that owns the masternode.
- **Public BLS Key** (`050564...155c91`): The public key from `bls generate`.
- **Voting Address** (`S5HXmW9iYzZq89LdH8eUXEzSwwwEaQ3XKS`): Used for voting.
- **Operator Reward** (`0`): Set to `0`.
- **Reward Address** (`SLvahoF6T7b8NY5wACtDoS9NzWPjRhNKuL`): Where masternode rewards will go.
- **Fee Address** (`SHu7BFFtfsU3FgfUX1y5JnAQNVZ28348UK`): Address for the masternode fee.

---

### Step 6: Sign the ProRegTx Transaction

Use this command to sign the prepared transaction:

```bash
signmessage "SRrfbPvmgds7XFvU4xhsCVegDM4Do6EyYp" "BLvahoF6T7b8NY5wACtDoS9NzWPjRhNKuL|0|B6ZhT7SR1BQSUYrab3isCGEmJGwndSxGod|B5HXmW9iYzZq89LdH8eUXEzSwwwEaQ3XKS|c8ebf2ae235d658e0809915348718dbb262f6884473c00448ba93e7ce4648070"
```

Example signed message output:

```plaintext
ILrWvvZRZeZhnfFtNwd087rwGsiPJH28GfmoPfjSDhUcEY+joeUd82/lqVnO0FD0V1L8vpjYju92fjMPITVScGI=
```

---

### Step 7: Submit the ProRegTx Transaction

Finally, submit your ProRegTx transaction with the following command:

```bash
protx register_submit 0300010001ac7584669c70526e0e338d6a2477dc648788140dd0dcbc5915878f9c632d129b0100000000feffffff01e551cd1d000000001976a9149385c0ceafd77df3619e604f4ce7d0317bbcbfae88ac00000000d1010000000000418d9c320ccb347117eb24bf8262f9fea08b809518ad4706fc59f98d439985610100000000000000000000000000ffff9f591f3f32ac1730a9104ead8b642345c1300e81c4d78e874de6050564992464a87643d273e87334fda1e8beb52e9605b9cef2fe73eb3a063f12c8f03a6fa4f07e26a1e9e5175e155c910929cbddb56d0fbd2993de634c3ed42de5a8455700001976a914b4b5864ed646cd8591a8ed996fa6c25de0b98bce88ac8f420b431efe6e62a55533099d2e99759767d38f94461325508afe3feadd0a9f00 ILrWvvZRZeZhnfFtNwd087rwGsiPJH28GfmoPfjSDhUcEY+joeUd82/lqVnO0FD0V1L8vpjYju92fjMPITVScGI=
```

Example output (transaction ID):

```plaintext
9c76272b7ef2a7456c84158424eb138bd3636b09aa2beae973bbed921f1f7868
```

---

Your masternode should now be successfully registered. Congratulations! If you have any questions, don’t hesitate to reach out.