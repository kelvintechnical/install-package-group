markdown# Install Package Group (RHEL 9)
### RHCSA EX200 Lab | Part of [linux-ops-mastery](https://github.com/kelvintechnical/linux-ops-mastery)
> Use dnf to list, inspect, and install a complete group of related software packages in a single command.

![RHCSA](https://img.shields.io/badge/RHCSA-EX200-EE0000?style=flat&logo=redhat&logoColor=white)
![Topic](https://img.shields.io/badge/Topic-Package_Management-blue)

---

## 📋 Scenario

On **Node1**, use `dnf` to explore available package groups, inspect the contents of a group before installing, and install a complete group of related software in a single command.

---

## 🎯 Lab Description

This lab teaches you how Linux organizes software into **package groups** — named collections of related RPM packages bundled together for a specific purpose or workload. Instead of researching and installing dozens of individual packages manually, `dnf group install` handles the entire dependency chain in one command.

On the RHCSA exam, you may be asked to install a specific group by name — for example, enabling "Development Tools" to get `gcc`, `make`, and related compilers. This lab walks you through the full workflow: discovering what groups exist, inspecting their contents before committing, installing a group, and verifying it landed correctly.

By the end of this lab you will understand:
- How package groups are structured (mandatory, default, optional packages)
- How to find the exact group name before using it in a command
- How to verify a group installation persists and is recognized by dnf

---

## 🎯 Requirements

1. List all available package groups.
2. Inspect the contents of a specific group.
3. Install a complete package group.
4. Verify the group was installed successfully.

---

## ✅ Tasks

- Use `dnf group list` to see available groups
- Use `dnf group info` to inspect group contents
- Use `dnf group install` to install a group
- Verify with `dnf group list --installed`

---

## 📚 Command Decision Map

| Lab Phrase | Question Being Asked | Tool |
|------------|---------------------|------|
| "List available groups" | How do I see all package groups? | `dnf group list` |
| "Inspect group contents" | What packages are in a group? | `dnf group info "Group Name"` |
| "Install a complete group" | How do I install many packages at once? | `dnf group install "Group Name"` |
| "Verify installation" | How do I confirm a group is installed? | `dnf group list --installed` |

---

## 🧠 Big Concept — Package Groups

A package group is a named collection of related RPM packages bundled together for a specific purpose. Instead of installing 10 individual packages one at a time, you install the whole group in one command.

**Three types of packages inside a group:**

| Type | Meaning |
|------|---------|
| Mandatory | Always installed with the group |
| Default | Installed unless you opt out |
| Optional | Not installed by default — must request explicitly |

---

## Step 1 — List all available package groups

```bash
sudo dnf group list
```

**Expected output (sample):**
Available Environment Groups:
Server with GUI
Server
Minimal Install
Available Groups:
RPM Development Tools
Development Tools
System Tools
Security Tools
...

**Show hidden groups too:**
```bash
sudo dnf group list --hidden
```

---

## Step 2 — Inspect a group before installing

```bash
sudo dnf group info "System Tools"
```

**Expected output:**
Group: System Tools
Description: This group is a collection of various tools for the system.
Mandatory Packages:
hdparm
lsof
...
Default Packages:
mc
...
Optional Packages:
...

> Always inspect before installing — groups can pull in dozens of packages.

---

## Step 3 — Install a package group

```bash
sudo dnf group install "System Tools" -y
```

> Installs all mandatory and default packages in the group in one command.

**Install optional packages too:**
```bash
sudo dnf group install --with-optional "System Tools" -y
```

---

## Step 4 — Verify the group is installed

```bash
sudo dnf group list --installed
```

**Expected output:**
Installed Groups:
System Tools

---

## 🧠 Key Concepts

| Concept | What it means |
|---------|--------------|
| `dnf group list` | Lists all available and installed groups |
| `dnf group info` | Shows mandatory, default, and optional packages in a group |
| `dnf group install` | Installs all mandatory + default packages in a group |
| `--with-optional` | Also installs optional packages in the group |
| `--installed` | Filters `group list` to show only installed groups |
| Mandatory packages | Always installed — cannot be skipped |
| Default packages | Installed unless explicitly excluded |
| Optional packages | Skipped by default — use `--with-optional` to include |

---

## ⚠️ Pitfalls

- **Group names with spaces need quotes** → `dnf group install System Tools` fails — always use `"System Tools"`
- **Forgetting `--installed` to verify** → `dnf group list` alone shows everything; filter with `--installed` to confirm
- **Group names differ between RHEL versions** → always run `dnf group list` first to confirm exact names on your system
- **`dnf group remove`** → removes the group marker but may leave packages behind; use `dnf autoremove` to clean up orphans

---

## ✅ Lab Checklist

- `dnf group list` shows available groups ✓
- `dnf group info "System Tools"` displays package breakdown ✓
- `dnf group install "System Tools" -y` installs the group ✓
- `dnf group list --installed` confirms installation ✓

---

## 🔗 Related Labs

- [Configure Repository Access](https://github.com/kelvintechnical/Configure-Repository-Access-)
- [Full RHCSA/RHCE Study Guide →](https://github.com/kelvintechnical/linux-ops-mastery)

---

## 👤 Author

**Kelvin R. Tobias** — [kelvinintech.com](https://kelvinintech.com) | [GitHub](https://github.com/kelvintechnical) | [LinkedIn](https://www.linkedin.com/in/kelvin-r-tobias-211949219)
