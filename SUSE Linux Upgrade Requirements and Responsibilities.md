# SUSE Linux Enterprise Server (SLES) Upgrade from 12 SP5 to 15 SP6 Requirements and Responsibilities

Upgrading from **SLES 12 SP5** to **SLES 15 SP6** is a major version upgrade (not just a service pack update) and requires careful planning. Below are the **requirements** and **team responsibilities** for a successful migration.

## 1. Upgrade Requirements
### A. Pre-Upgrade Checks
✅ **System Compatibility**

- Verify hardware compatibility with SLES 15 SP6 [(check SUSE Hardware Compatibility List)](https://www.suse.com/suse-defines/definition/independent-hardware-vendor/)
- Ensure **64-bit architecture** (SLES 15 does not support 32-bit)

✅ **Software & Dependencies**

- Check third-party applications/drivers for **SLES 15 SP6 compatibility**
- Review **SUSE-supported upgrade paths** (direct upgrade from 12 SP5 to 15 SP6 is possible but may require intermediate steps)
- Remove **obsolete/unsupported packages** before upgrade

✅ **Backup & Recovery**

<!-- - Take **full system backup** (including `/etc`, `/home`, `/var`, and application data) -->
- Take full system backup and application data
- Document **network configurations, storage mounts, and security policies**
- Prepare **rollback plan** (snapshot if using virtualization)

✅ **Storage & Resources**

- Minimum **20GB free disk space** (for OS upgrade + temporary files)
- **Memory:** At least **4GB RAM** (8GB+ recommended for production)

### B. Upgrade Methods
SUSE provides multiple upgrade paths:

| **Method**	               | **Description**	                             | **When to Use**
|----------------------------|-----------------------------------------------|---------------------------------------
`zypper migration`           | Online upgrade using SUSE repositories	       | Best for systems with internet access
**Offline ISO Upgrade**      | Boot from SLES 15 SP6 ISO and perform upgrade | For air-gapped systems
**AutoYaST/SALT Automation** | Automated upgrades using scripts	             | Large-scale deployments

zypper migration	Online upgrade using SUSE repositories	Best for systems with internet access
Offline ISO Upgrade	Boot from SLES 15 SP6 ISO and perform upgrade	For air-gapped systems
AutoYaST/SALT Automation	Automated upgrades using scripts	Large-scale deployments

<!--
⚠ Note:
- **Leapp tool** (used for RHEL upgrades) is **not applicable** for SLES.
- **In-place upgrade** is supported, but **fresh install is recommended** for critical systems.
-->
## 2. Team Responsibilities
### A. System Administrators
✔ Perform **pre-upgrade checks** (disk space, dependencies, backups)  </br>
✔ Execute **upgrade process** (using `zypper migration` or ISO)    </br>
✔ Verify **post-upgrade system stability** (services, networking, storage)  </br>
✔ Troubleshoot **boot issues, package conflicts, or dependency errors**  </br>
✔ Apply **post-upgrade patches & configurations**  </br>

### B. Security Team
✔ Review **SELinux/AppArmor policies** (SLES 15 uses different defaults)  </br>
✔ Update **firewall rules (firewalld)** and **SSH configurations**    </br>
✔ Verify **compliance with security policies (STIG, CIS benchmarks)**    </br>

### C. Application Owners
✔ Test **critical applications** on SLES 15 SP6 before production upgrade    </br>
✔ Update **application dependencies** (Java, Python, DB connectors)      </br>
✔ Modify **startup scripts/systemd units** if needed    </br>

### D. Database Team
✔ Backup **databases (MySQL, PostgreSQL, Oracle)** before upgrade    </br>
✔ Verify **DB compatibility** (e.g., MariaDB 10.5+ in SLES 15)    </br>
✔ Test **replication & performance** post-upgrade    </br>

### E. Network Team
✔ Update **network configurations (ifcfg → wicked/nmcli in SLES 15)**  </br>
✔ Verify **NFS/Samba/CIFS mounts** post-upgrade  </br>
✔ Test **VPN & firewall rules**  </br>

### F. Management/Project Team
✔ Approve **downtime window**    </br>
✔ Coordinate **communication between teams**    </br>
✔ Ensure **rollback plan is tested**    </br>

### 3. Post-Upgrade Tasks
🔹 **Verify system integrity** (zypper verify, journalctl -xe)    </br>
🔹 **Update remaining packages** (zypper update)    </br>
🔹 **Re-enable third-party repositories** (if disabled during upgrade)  </br>
🔹 **Test all critical services** (HTTP, DB, authentication)    </br>
🔹 **Monitor system logs** for errors (/var/log/messages, dmesg)  </br>

# ⚠ Key Risks & Mitigations
|**Risk**                       |	**Mitigation**
|-------------------------------|-----------------------------------------------------
**Boot failure after upgrade**	| Keep **rescue ISO** ready, test in staging first
**Package conflicts**           |	Use `zypper dup --no-allow-vendor-change` carefully
**Application incompatibility** |	Test in a **non-production environment** first
**Network service failure**	    | Reapply custom network configs post-upgrade

<!--
## Conclusion
Upgrading from **SLES 12 SP5 → 15 SP6** requires:    </br>
✅ **Proper planning (backups, compatibility checks)**  </br>
✅ **Team coordination (SysAdmins, Security, DB, Networking)**    </br>
✅ **Post-upgrade validation (services, security, performance)**    </br>

Would you like a **step-by-step upgrade guide** or **troubleshooting tips** for common issues?
-->
