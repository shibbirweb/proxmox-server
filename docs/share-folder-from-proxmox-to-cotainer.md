# `pct set` Command – Bind Mount Example

## Example Command
```bash
pct set 107 -mp0 /mnt/pve/Desktop,mp=/shared
```

## Description

This command modifies the configuration of an existing **LXC container** (VMID `107`) in **Proxmox VE** by adding a **bind mount** from the Proxmox **host** to the **container**.

It allows the container to access a specific directory from the host file system.

---

## Syntax

```bash
pct set <vmid> -mp<N> <host_path>,mp=<container_path>[,options]
```

### Components:

* `<vmid>`: The numeric ID of the container you want to configure.
* `-mp<N>`: Mount point index (e.g., `-mp0`, `-mp1`, etc.).
* `<host_path>`: Absolute path on the **Proxmox host** that will be mounted into the container.
* `mp=<container_path>`: Path **inside the container** where the host path will be mounted.
* `[options]`: (Optional) Additional flags such as `ro=1` for read-only access.

### Example with optional flags:

```bash
pct set 107 -mp0 /mnt/data,mp=/data,ro=1
```

This mounts `/mnt/data` from the host into the container as `/data` with **read-only** access.

---

## Parameters

| Parameter          | Description                                                                |
| ------------------ | -------------------------------------------------------------------------- |
| `pct`              | Proxmox command-line tool for managing LXC containers.                     |
| `set`              | Modifies the configuration of an existing container.                       |
| `107`              | VMID (numeric ID) of the container to configure.                           |
| `-mp0`             | Mount point index (0 in this case; you can use `-mp1`, `-mp2`, etc.).      |
| `/mnt/pve/Desktop` | **Source path** on the Proxmox **host** — the directory to share.          |
| `mp=/shared`       | **Mount point** inside the container where the host directory will appear. |

---

## Result

After running this command, the container with VMID `107` will have access to the host's `/mnt/pve/Desktop` directory at the path `/shared` inside the container.

---

## Use Cases

* Sharing host files with a container (e.g., media, config files, scripts).
* Providing persistent storage inside a container.
* Enabling container-based backup or processing tools to access host data.

---

## Important Notes

* The host path (`/mnt/pve/Desktop`) **must exist**.
* The container should be **restarted** for changes to apply.
* The container must have **read/write permissions** to the mounted directory, depending on your needs.
* If the source path is on a Proxmox storage volume (e.g., an NFS share), the storage must allow content type `rootdir`.
* Use multiple `-mpX` parameters to mount more than one directory (e.g., `-mp1`, `-mp2`, etc.).

---

## Example Inside the Container

Once the container is running:

```bash
ls /shared
```

This will list the contents of `/mnt/pve/Desktop` from the host.

---

## Related Commands

* `pct config <vmid>` – View full configuration of the container.
* `pct start <vmid>` / `pct restart <vmid>` – Start or restart the container.
* `pct mount <vmid>` – Mount container root file system for inspection (offline).
* `pct exec <vmid> -- <command>` – Run a command inside the container.

---

## References

* [Proxmox LXC Bind Mounts Documentation](https://pve.proxmox.com/wiki/Linux_Container#_bind_mount_points)

```

---

Let me know if you'd like a version tailored for your organization's internal documentation format (e.g., HTML, PDF, or custom markdown styling).
```
