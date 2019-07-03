# ngic-bess

## Pre-reqs

To follow instructions, you need

* Docker CE >= 17.06
* Hugepages mounted at `/dev/hugepages` or updated location in [`docker_setup.sh`](docker_setup.sh)
* Update mode for devices: `dpdk`, `af_xdp`, `af_packet` in [`docker_setup.sh`](docker_setup.sh),
    along with device details
* Update [`docker_setup.sh`](docker_setup.sh) and [`conf/spgwu.bess`](conf/spgwu.bess) to run iltrafficgen tests

## Init

To run BESS daemon with custom NGIC modules' code

```bash
./docker_setup.sh
```

To init the pipeline or reflect changes to [`conf/spgwu.bess`](conf/spgwu.bess)
or [`conf/spgwu.json`](conf/spgwu.json)

```bash
docker exec bess /conf/reload.sh
docker exec bess bessctl show pipeline > pipeline.txt
```

## Operate Pipeline

Control program(s) to dynamically configure BESS modules

| Functionality | Controller |
|---------------|------------|
| Routes | [route_control.py](conf/route_control.py) |
| UE sessions | Static trafficgen only in `spgwu.bess` |

## Observe

To view the pipeline, open [http://[hostip]:8000](http://[hostip]:8000)
in a browser

To drop into BESS shell

```bash
docker exec -it bess bessctl
```
