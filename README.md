# ansible-nfs-mounter

This ansible role mounts an NFS drive to the local filesystem, and ensures that it will remain mounted after restarts.

## Requirements

Really this should work on any debian based system, but has been tested on a Raspberry Pi running Raspbian (Stretch).

## Role Variables

- `nfs_share_mounts`
  - An array of mounts, allowing you to mount multiple nfs systems.

A mount consists of:
- `what`
  - The address for the NFS you want to mount
  - Ex. `192.168.1.23:/nfs/you-share`
- `where`
  - The mount point within your local file system
  - Ex `/mnt/my-nfs-share`
- `opts`
  - As described in the [`mount`](https://docs.ansible.com/ansible/latest/modules/mount_module.html) module
- `passno`
  - As described in the [`mount`](https://docs.ansible.com/ansible/latest/modules/mount_module.html) module

## Dependencies

Have an NFS drive on your network, likely with a static IP.

## Example Playbook

```yml
    - hosts: pi
      roles:
        - role: mpataki.nfs_mounter
          tags: nfs
          vars:
            nfs_share_mounts:
              - what: 192.168.1.23:/nfs/share
                where: /mnt/share
```

