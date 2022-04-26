[![OpenDev Zuul Builds - Ansible Collection OpenStack](https://zuul-ci.org/gated.svg)](http://zuul.opendev.org/t/openstack/builds?project=openstack%2Fansible-collections-openstack#)

# Ansible Collection: openstack.cloud


This repo hosts the `openstack.cloud` Ansible Collection.

The collection includes the Openstack modules and plugins supported by Openstack community to help the management of Openstack infrastructure.

:warning: **WARNING:**
This collection is currently being ported to the upcoming OpenStack SDK 1.\* release. SDK version 1.\* introduces
numerous API changes which break backward compatibility with previous 0.\* releases. Since keeping a single collection
release compatible with both SDK series is not sustainable, our collection codebase has been split:
Branch stable/1.0.0 and 1.\*.\* releases of the collection are compatible with previous OpenStack SDK 0.\* releases
only. The master branch and upcoming 2.\*.\* releases of this collection will be compatible with SDK 1.\* only. Both
branches will continue to be maintained for now. Patches from master will be backported to stable/1.0.0 on a best effort
basis but expect new features to be introduced in the master branch only. Contributions are welcome for both branches!
:warning:

## Installation and Usage

### Installing dependencies

For using the Openstack Cloud collection firstly you need to install `ansible` and `openstacksdk` Python modules on your Ansible controller.
For example with pip:

```bash
pip install "ansible>=2.9" "openstacksdk>=0.99.0"
```

OpenStackSDK has to be available to Ansible and to the Python interpreter on the host, where Ansible executes the module (target host).
Please note, that under some circumstances Ansible might invoke a non-standard Python interpreter on the target host.
Using Python version 3 is highly recommended for OpenstackSDK and strongly required from OpenstackSDK version 0.39.0.

---

#### NOTE

OpenstackSDK is better to be the last stable version. It should NOT be installed on Openstack nodes,
but rather on operators host (aka "Ansible controller"). OpenstackSDK from last version supports
operations on all Openstack cloud versions. Therefore OpenstackSDK module version doesn't have to match
Openstack cloud version usually.

---

### Installing the Collection from Ansible Galaxy

Before using the Openstack Cloud collection, you need to install the collection with the `ansible-galaxy` CLI:

`ansible-galaxy collection install openstack.cloud`

You can also include it in a `requirements.yml` file and install it through `ansible-galaxy collection install -r requirements.yml` using the format:

```yaml
collections:
- name: openstack.cloud
```

### Playbooks

To use a module from the Openstack Cloud collection, please reference the full namespace, collection name, and module name that you want to use:

```yaml
---
- name: Using Openstack Cloud collection
  hosts: localhost
  tasks:
    - openstack.cloud.server:
        name: vm
        state: present
        cloud: openstack
        region_name: ams01
        image: Ubuntu Server 14.04
        flavor_ram: 4096
        boot_from_volume: True
        volume_size: 75
```

Or you can add the full namespace and collection name in the `collections` element:

```yaml
---
- name: Using Openstack Cloud collection
  hosts: localhost
  collections:
    - openstack.cloud
  tasks:
    - server_volume:
        state: present
        cloud: openstack
        server: Mysql-server
        volume: mysql-data
        device: /dev/vdb
```

### Usage

See the collection docs at Ansible site:

* [openstack.cloud collection docs (version released in Ansible package)](https://docs.ansible.com/ansible/latest/collections/openstack/cloud/index.html)

* [openstack.cloud collection docs (devel version)](https://docs.ansible.com/ansible/devel/collections/openstack/cloud/index.html)

## Contributing

For information on contributing, please see [CONTRIBUTING](https://opendev.org/openstack/ansible-collections-openstack/src/branch/master/CONTRIBUTING.rst)

There are many ways in which you can participate in the project, for example:

- Submit [bugs and feature requests](https://storyboard.openstack.org/#!/project/openstack/ansible-collections-openstack), and help us verify them
- Submit and review source code changes in [Openstack Gerrit](https://review.opendev.org/#/q/project:openstack/ansible-collections-openstack)
- Add new modules for Openstack Cloud

We work with [OpenDev Gerrit](https://review.opendev.org/), pull requests submitted through GitHub will be ignored.

## Testing and Development

If you want to develop new content for this collection or improve what is already here, the easiest way to work on the collection is to clone it into one of the configured [`COLLECTIONS_PATHS`](https://docs.ansible.com/ansible/latest/reference_appendices/config.html#collections-paths), and work on it there.

### Testing with `ansible-test`

We use `ansible-test` for sanity:

```bash
tox -e linters
```

## More Information

TBD

## Communication

We have a dedicated Interest Group for Openstack Ansible modules.
You can find other people interested in this in `#openstack-ansible-sig` on [OFTC IRC](https://www.oftc.net/).

## License

GNU General Public License v3.0 or later

See [LICENCE](https://opendev.org/openstack/ansible-collections-openstack/src/branch/master/COPYING) to see the full text.
