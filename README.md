# Monero

This role sets up a [Monero](https://www.getmonero.org/) full node using docker.

## Requirements

This role relies on `docker` being available on the host and the [`community.general.docker_container` module](https://docs.ansible.com/ansible/2.10/collections/community/general/docker_container_module.html) in ansible.

[`geerlingguy.docker` role](https://galaxy.ansible.com/geerlingguy/docker) can be used to setup docker.
For the `docker_container` python module, [`geerlingguy.pip` role](https://galaxy.ansible.com/geerlingguy/pip) can be used to install Python's [`docker` package](https://pypi.org/project/docker/).

## Role Variables

- **`monero__version`** (optional, default: _0.18.1.0_): Image version tag to use.
- **`monero__hash`** (optional (required if using non-default monero__version), defaults to the correct/signed hash for the default version)
- **`monero__container_name`** (optional, default: _monerod-node_): Name to use for the container created by the role.
- **`monero__data_dir`** (optional, default _/var/monero/_): Folder to use for persistent files.
- **`monero__p2p_port`** (optional, default: _18080_): Port on which the peer to peer port will be exposed on the host machine.
- **`monero__rpc_port`** (optional, default: _18081_): Port on which the rpc port will be exposed on the host machine.

## Custom monerod.conf settings
Customize your monerod.conf by providing your own monderod.conf.j2 file in a templates folder that ansible is aware of. A default one is provided by the role but you are encouraged to provide your own.

You can also customize the Dockerfile used by creating your own Dockerfile.j2 in a templates folder.
## Example Playbook

The following would be a fairly common role usage example:

```yaml
- host: monerod.my-domain.com
  roles:
    - role: salessandri.monero
```

## License

MIT

## Author Information

This role was created in 2021 by [Santiago Alessandri](https://rambling-ideas.salessandri.name).

Forked by Brandon Shipley 9/2022 to:
- remove/lessen reliance on docker hub
- use ansible/jinja templating to remove necessity for keeping separate Dockerfile repo
- So I can practice ansible / get more into monero & obviously setup a public node 