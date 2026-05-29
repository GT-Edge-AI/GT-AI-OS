# Getting Started

> **Note:** These instructions are placeholders and have not been QA'd. Full and correct Super Admin instructions will be provided in v2.0.37.

Welcome to the GT AI OS Control Panel. This guide will help you get oriented and understand the key areas of the Super Admin interface.

## Overview

The Control Panel is where Super Admins manage the entire GT AI OS platform. From here you can:

- Manage tenants (organizations) and their settings
- Create and manage user accounts
- Configure AI models and inference providers
- Set up email functionality
- Monitor access and security
- Manage licenses and billing

## Interface Overview

The Control Panel interface consists of:

- **Sidebar** (left): Navigate between different management sections
- **Main Content Area** (center): Where you perform configuration and management tasks
- **User Menu** (top right): Access your profile settings and logout

## First Steps

After installation, complete these tasks in order:

| Step | What to Do | Where |
|------|------------|-------|
| 1 | Create your own admin account | Users page |
| 2 | Delete the default admin account | Users page |
| 3 | Enable two-factor authentication | Settings page |
| 4 | Configure email (SMTP) | Email Settings page |
| 5 | Activate your license | License page |
| 6 | Add AI provider API keys | Models page |

For detailed step-by-step instructions, see the [Deployment Checklist](deployment-checklist).

## Quick Reference

| Page | What It Does |
|------|--------------|
| **Tenants** | View and edit tenant organizations |
| **Users** | Create and manage user accounts |
| **Models** | Configure AI models and inference providers |
| **Financial Controls** | Set pricing and budget limits |
| **Email Settings** | Configure SMTP for password reset and welcome emails |
| **License** | View deployment ID and activate licenses |
| **Access Logs** | Monitor authentication and session activity |
| **Compliance Mode** | Configure compliance frameworks |
| **Instructions Settings** | Set external documentation links |
| **Email Templates** | Customize welcome and notification emails |
| **Settings** | Configure your personal 2FA |

## Default Credentials

If this is a fresh installation, use these credentials:

- **Email:** `gtadmin@test.com`
- **Password:** `Test@123`

These credentials work for both Control Panel (http://localhost:3001) and Tenant App (http://localhost:3002).

## Security Notice

The default account is publicly known. You must create your own admin account and delete the default one immediately after first login. See the [Deployment Checklist](deployment-checklist) for instructions.

## Getting Help

- **GT AI OS Super Admin Instructions**: You're reading it now - use the sidebar to navigate topics
- **Troubleshooting**: See [Troubleshooting](troubleshooting) for common issues
- **Support**: Contact GT Edge AI support for Enterprise assistance

## Next Steps

- [Deployment Checklist](deployment-checklist) - Complete post-installation setup
- [User Management](user-management) - Create and manage users
- [License Management](license-management) - Activate your Enterprise license
