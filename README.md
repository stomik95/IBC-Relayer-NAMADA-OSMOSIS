# IBC-Relayer-NAMADA-OSMOSIS
# Description:

**Namada <--> Osmosis IBC-Relayer**

**Category:**  
Operating IBC/ Interoperability infrastructure  

**Description:**  
Operate a Shielded Expedition-compatible Osmosis testnet relayer

**Evidence:**  
Created channel:  

**Namada SE  <-->  Osmosis osmo-test-5**<br>
**channel-701  <-->  channel-6186**


> :white_check_mark: **IBC Create Client Confirmation**<br>
> https://www.mintscan.io/osmosis-testnet/tx/72DCA9DCA3BEEE7FF317FF71FD27AB3D4DFDC354427CAB3FC5BE84E2E4F16AFD?height=5934339

> :white_check_mark: **IBC Namada Confirmation**<br>
> https://www.mintscan.io/osmosis-testnet/tx/9E2930A00EDB8E7579342DF582EEF657361160F6244E31E7B447ADA693C27889?height=5934434

> :white_check_mark: **IBC Osmosis Confirmation**<br>
> https://www.mintscan.io/osmosis-testnet/tx/5DB790D54072613163B93E9C0EAC40237367C8E9A254A5C6C2B4E16158DFDB4A?height=5934447

**SE account:**
tpknam1qrhmhyxrdq03jxnjuzz7f7q6ecdu57cx0qlygpc9fr30veyuy9pjg50dn7j

**Osmo account:**
osmo1ngx9y78ut98y0xxfnzmtl562y9q8hwt6lzg34n

# Hermes Config⚙️
```
[[chains]]
id = 'shielded-expedition.88f17d1d14'
type = 'Namada'
rpc_addr = 'http://127.0.0.1:26657'
grpc_addr = 'http://127.0.0.1:9090'
event_source = { mode = 'push', url = 'ws://127.0.0.1:26657/websocket', batch_delay = '500ms' }
account_prefix = 'namada'
key_name = 'stomik'
store_prefix = 'ibc'
gas_price = { price = 0.1, denom = 'tnam1qxvg64psvhwumv3mwrrjfcz0h3t3274hwggyzcee' }
#gas_multiplier = 1.2
#default_gas = 40000000
#max_gas = 20000000000
rpc_timeout = '30s'

[[chains]]
id = 'osmo-test-5'
type = 'CosmosSdk'
rpc_addr = 'https://rpc.testnet.osmosis.zone'  # set the IP and the port of the chain
grpc_addr = 'https://grpc.testnet.osmosis.zone'
event_source = { mode = 'push', url = 'wss://rpc.testnet.osmosis.zone:443/websocket', batch_delay = '500ms' }
account_prefix = 'osmo'
key_name = 'stomik_osmo'
address_type = { derivation = 'cosmos' }
store_prefix = 'ibc'
default_gas = 400000
max_gas = 120000000
gas_price = { price = 0.1, denom = 'uosmo' }
gas_multiplier = 1.2
max_msg_num = 30
```
# Create IBC channel✅
**Start Hermes**
```
hermes --config $HERMES_CONFIG create channel --a-chain shielded-expedition.88f17d1d14 --b-chain osmo-test-5 --a-port transfer --b-port transfer --new-client-connection --yes
```
**Result Execution**
```
2024-03-11T04:14:04.281284Z  INFO ThreadId(01) running Hermes v1.7.4+38f41c6
2024-03-11T04:14:05.412297Z  INFO ThreadId(01) Creating new clients, new connection, and a new channel with order ORDER_UNORDERED
2024-03-11T04:14:26.326888Z  INFO ThreadId(01) foreign_client.create{client=osmo-test-5->shielded-expedition.88f17d1d14:07-tendermint-0}: 🍭 client was created successfully id=07-tendermint-2426
2024-03-11T04:14:28.931006Z  INFO ThreadId(01) foreign_client.create{client=shielded-expedition.88f17d1d14->osmo-test-5:07-tendermint-0}: 🍭 client was created successfully id=07-tendermint-2750
2024-03-11T04:21:30.684628Z  INFO ThreadId(01) 🎊  shielded-expedition.88f17d1d14 => OpenAckChannel(OpenAck { port_id: transfer, channel_id: channel-701, connection_id: connection-1156, counterparty_port_id: transfer, counterparty_channel_id: channel-6186 }) at height 0-109410
2024-03-11T04:21:43.002042Z  INFO ThreadId(01) 🎊  osmo-test-5 => OpenConfirmChannel(OpenConfirm { port_id: transfer, channel_id: channel-6186, connection_id: connection-2502, counterparty_port_id: transfer, counterparty_channel_id: channel-701 }) at height 5-5934447
2024-03-11T04:21:46.059036Z  INFO ThreadId(01) channel handshake already finished for Channel { ordering: ORDER_UNORDERED, a_side: ChannelSide { chain: BaseChainHandle { chain_id: shielded-expedition.88f17d1d14 }, client_id: 07-tendermint-2426, connection_id: connection-1156, port_id: transfer, channel_id: channel-701, version: None }, b_side: ChannelSide { chain: BaseChainHandle { chain_id: osmo-test-5 }, client_id: 07-tendermint-2750, connection_id: connection-2502, port_id: transfer, channel_id: channel-6186, version: None }, connection_delay: 0ns }
SUCCESS Channel {
    ordering: Unordered,
    a_side: ChannelSide {
        chain: BaseChainHandle {
            chain_id: ChainId {
                id: "shielded-expedition.88f17d1d14",
                version: 0,
            },
            runtime_sender: Sender { .. },
        },
        client_id: ClientId(
            "07-tendermint-2426",
        ),
        connection_id: ConnectionId(
            "connection-1156",
        ),
        port_id: PortId(
            "transfer",
        ),
        channel_id: Some(
            ChannelId(
                "channel-701",
            ),
        ),
        version: None,
    },
    b_side: ChannelSide {
        chain: BaseChainHandle {
            chain_id: ChainId {
                id: "osmo-test-5",
                version: 5,
            },
            runtime_sender: Sender { .. },
        },
        client_id: ClientId(
            "07-tendermint-2750",
        ),
        connection_id: ConnectionId(
            "connection-2502",
        ),
        port_id: PortId(
            "transfer",
        ),
        channel_id: Some(
            ChannelId(
                "channel-6186",
            ),
        ),
        version: None,
    },
    connection_delay: 0ns,
}
```

# Testing IBC Transfer
**Use SE channel-701**
```
namadac ibc-transfer --source tnam1qzesekwfv4ajwmcu5t9lpdfqj5nxy7snzvutl5p3 --receiver osmo1ngx9y78ut98y0xxfnzmtl562y9q8hwt6lzg34n --token naan --amount 100 --channel-id channel-701 --memo tpknam1qrhmhyxrdq03jxnjuzz7f7q6ecdu57cx0qlygpc9fr30veyuy9pjg50dn7j --signing-keys stomik --node https://rpc-nam-stomik.online
```
**Got Confirmation**
```
Transaction added to mempool.
Wrapper transaction hash: 4F8DDBF9B9A152139D54B2C362C9A6CDBE2A3623E2B7CE0E89F104095F926425
Inner transaction hash: 8B0911C5B335B5EFB8D79E61F723D118850FC3DE2CEFF4EB691ED0D18CC446A0
Wrapper transaction accepted at height 109594. Used 26 gas.
Waiting for inner transaction result...
Transaction was successfully applied at height 109595. Used 6193 gas.
```
**Transaction Hash**
> :white_check_mark: Namada <br>
> https://namada-explorer.validatorvn.com/txs/4F8DDBF9B9A152139D54B2C362C9A6CDBE2A3623E2B7CE0E89F104095F926425

> :white_check_mark: Osmosis <br>
> https://www.mintscan.io/osmosis-testnet/tx/C63045CF38C5E4118B0506ECC7709102E05324C11ABA4087205E79E25264B3D1?height=5934949

**Namada &lt;--> Osmosis IBC Relayer Shield Expedition**
