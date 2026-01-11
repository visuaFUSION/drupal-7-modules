# LDAP Integration (ldap) for Drupal 7.x

The LDAP module provides comprehensive LDAP integration for Drupal, enabling authentication, authorization, user provisioning, and data synchronization with LDAP directories.

## Features

- **LDAP Authentication** — Authenticate users against LDAP/Active Directory
- **LDAP Authorization** — Map LDAP groups to Drupal roles and Organic Groups
- **LDAP User Provisioning** — Create/sync Drupal accounts from LDAP entries
- **LDAP Entry Provisioning** — Create/sync LDAP entries from Drupal accounts
- **LDAP Servers** — Configure multiple LDAP server connections
- **LDAP Query** — Execute custom LDAP queries
- **LDAP Views** — Expose LDAP data to Views module
- **LDAP Feeds** — Import LDAP data via Feeds module

---

## Versions

| Directory | Version | Status |
|-----------|---------|--------|
| `ldap-7.x-2.6/` | 7.x-2.6 | Original from drupal.org |
| `ldap-7.x-2026.04/` | 7.x-2026.04 | Updated for Drupal 7 LTSR |

---

## Changes in 7.x-2026.04

### PHP 8.2 Compatibility

PHP 8.2 deprecated the creation of dynamic properties (assigning to `$this->property` without declaring the property first). The following fixes address all deprecation warnings:

**LdapUserConf.class.php**
- **File:** `ldap_user/LdapUserConf.class.php`
- **Properties added:** `createLDAPAccounts`, `createLDAPAccountsAdminApproval`
- **Problem:** The `load()` method was assigning to undeclared properties

**LdapServer.class.php**
- **File:** `ldap_servers/LdapServer.class.php`
- **Properties added:** `_errorMsgText`, `type`, `export_type`
- **Problem:** Missing error property and CTools export properties

**LdapQuery.class.php**
- **File:** `ldap_query/LdapQuery.class.php`
- **Properties added:** `_errorMsgText`, `type`, `export_type`
- **Problem:** Missing error property and CTools export properties (set dynamically in constructor)

**LdapAuthorizationConsumerAbstract.class.php**
- **File:** `ldap_authorization/LdapAuthorizationConsumerAbstract.class.php`
- **Properties added:** `mappingDirections`
- **Problem:** Constructor was assigning to undeclared property

---

## Submodules

| Module | Description |
|--------|-------------|
| **LDAP Servers** | Core server configuration and connection management |
| **LDAP User** | User provisioning between Drupal and LDAP |
| **LDAP Authentication** | Authenticate users against LDAP |
| **LDAP Authorization** | Map LDAP groups to Drupal permissions |
| **LDAP Authorization - Drupal Role** | Assign Drupal roles based on LDAP groups |
| **LDAP Authorization - OG** | Assign Organic Groups membership based on LDAP |
| **LDAP Query** | Execute and manage custom LDAP queries |
| **LDAP Views** | Views integration for LDAP data |
| **LDAP Feeds** | Feeds module integration |
| **LDAP Help** | Help and documentation |
| **LDAP Test** | Testing utilities (development only) |

---

## Requirements

- PHP 7.4+ (PHP 8.0+ recommended, PHP 8.2+ compatible)
- PHP LDAP extension (`php-ldap`)
- Drupal 7 LTSR

---

## Security Notes

- Store LDAP bind credentials securely
- Use TLS/SSL (LDAPS or StartTLS) for LDAP connections
- Restrict LDAP server configuration to trusted administrators
- Review LDAP authorization mappings regularly
