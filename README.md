# CoreOS Cluster Prepared for Fleet Provisioning

```
vagrant up --provider virtualbox
```

```                                                                       
┌────────────────────────────────────────────────────────────────────────────┐
│                                  10.10.10                                  │
└─────────┬────────────┬────────────┬──────────────┬────────────┬────────────┤
          │            │            │              │            │            │
       .11│         .12│        .13 │          .101│        .102│        .103│
          │            │            │              │            │            │
     ┌────┤       ┌────┤       ┌────┤         ┌────┤       ┌────┤       ┌────┤
     │eth1│       │eth1│       │eth1│         │eth1│       │eth1│       │eth1│
┌────┴────┤  ┌────┴────┤  ┌────┴────┤    ┌────┴────┤  ┌────┴────┤  ┌────┴────┤
│         │  │         │  │         │    │         │  │         │  │         │
│ etcd-01 │  │ etcd-01 │  │ etcd-01 │    │ node-01 │  │ node-02 │  │ node-03 │
│         │  │         │  │         │    │         │  │         │  │         │
│ fleet   │  │ fleet   │  │ fleet   │    │ fleet   │  │ fleet   │  │ fleet   │
│         │  │         │  │         │    │         │  │         │  │         │
│ etcd    │  │ etcd    │  │ etcd    │    │         │  │         │  │         │
│         │  │         │  │         │    │         │  │         │  │         │
└─────────┘  └─────────┘  └─────────┘    └─────────┘  └─────────┘  └─────────┘
```

```
$ fleetctl --endpoint http://10.10.10.11:2379 list-machines
MACHINE		  IP		        METADATA
06cca858...	10.10.10.101	role=node
37d11029...	10.10.10.100	role=node
6718adff...	10.10.10.12	  role=etcd
8bf292ae...	10.10.10.102	role=node
ae7ca4c8...	10.10.10.11	  role=etcd
b38c4afe...	10.10.10.13	  role=etcd
$
```

### Configuration (Head of Vagrantfile)

```
members = {
  #  Name     #, CPU,  RAM, 1ST_IP
  'etcd' => [ 3,   1,  256,     11 ],
  'node' => [ 3,   2, 2048,    100 ],
}
PREFIX             = "10.10.10"
```
