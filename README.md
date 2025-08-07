# 🚀 ACI Automation with Ansible

This repository contains Ansible roles and playbooks to automate Cisco ACI configurations, including querying system information, creating tenants, application profiles (APs), endpoint groups (EPGs), and handling contracts.

---

## 📦 Roles Overview

### `aci_magic`
Automates the creation of ACI components for a demo tenant.

**Tasks include:**
- Querying system information from ACI controllers.
- Creating a new tenant (`demo-tenant-ehsan`).
- Adding an Application Profile (`workshop`).
- Creating multiple Endpoint Groups (EPGs): `web`, `app`, and `db`.

### `contract_handler`
Handles contract-related operations in the `common` tenant.

**Tasks include:**
- Querying existing contracts.
- Extracting specific contract details using `json_query`.

---

## 🛠️ Requirements
- Ansible 2.9+
- Cisco ACI modules (`cisco.aci`)
- Access to Cisco ACI fabric
- Python packages:
  - `ansible.utils`
  - `community.general`
  - `jmespath` (required for `json_query` filters)

> ⚠️ Ensure the `jmespath` Python module is installed in the same Python environment used by Ansible. You can install it using:
```bash
pip install jmespath
```

## ▶️ Running the Playbooks
To run the roles individually:

```bash
ansible-playbook aci_magic_playbook.yml --ask-vault-pass
ansible-playbook contract_handler_playbook.yml --ask-vault-pass
```
Or combine them in a master playbook:

```yaml
# master_playbook.yml
- import_playbook: aci_magic_playbook.yml
- import_playbook: contract_handler_playbook.yml
```

Then run:

```bash
ansible-playbook master_playbook.yml --ask-vault-pass
```

---

## 📁 Directory Structure

```bash
.
├── roles/
│   ├── aci_magic/
│   │   └── tasks/
│   │       └── main.yml
│   ├── contract_handler/
│   │   └── tasks/
│   │       └── main.yml
├── aci_magic_playbook.yml
├── contract_handler_playbook.yml
├── master_playbook.yml
└── README.md
```

## 📌 Notes
- SSL certificate validation is disabled (validate_certs: false) for simplicity. Enable it in production environments.
- The contract query uses json_query to extract specific attributes. You can customize this to fit your needs.
- One or more files are encrypted using ansible-vault, so --ask-vault-pass is required when running playbooks.

## 🤝 Contributing

Feel free to fork, improve, and submit pull requests. Suggestions and improvements are welcome!
