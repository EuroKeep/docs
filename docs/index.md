# EuroKeep

## Your Money - Your Data

EuroKeep is a self-hosted personal finance management application that gives you full control over your financial data.

Unlike cloud-based solutions, EuroKeep can be deployed on your own infrastructure. Your accounts, balances, movements and budgets remain where they belong: under your control.

This documentation provides everything you need to deploy, configure and use your own EuroKeep instance.

---

## What is EuroKeep?

EuroKeep helps you manage your personal finances in a simple and privacy-focused way.

With EuroKeep you can:

- Manage multiple accounts and currencies
- Track income, expenses and transfers
- Organize movements with categories
- Create and monitor budgets
- Analyze your monthly financial development
- Hide sensitive information with Privacy Mode
- Export monitoring information via Prometheus

The goal is not to replace complex banking software, but to provide a lightweight, transparent and self-hosted solution for managing your everyday finances.

---

## Self-Hosted by Design

EuroKeep is designed to run on your own server.

EuroKeep is delivered as a single Docker image, `eurokeep/eurokeep`, that contains the complete product:

- Angular frontend
- Nginx as web server
- PHP-FPM application runtime

The only other service it needs is a MariaDB database. The provided Docker Compose file starts one for you.

---

## Installation

All you need is two files in an empty directory:

- A Docker Compose file
- An environment file (`.env`)

Database migrations run automatically on every start, and the default data is created on the first one.

After starting the containers, administrative tasks such as user creation and password management are performed directly inside the EuroKeep container using CakePHP CLI commands.

See [Docker](setup/docker.md) for the compose file and the environment file.

---

## Getting Started

A typical setup workflow:

1. Put the compose file and the `.env` file into an empty directory
2. Start the containers with `docker compose up -d`
3. Put a TLS reverse proxy in front of port 8080 (login only works via HTTPS)
4. Create your first EuroKeep user inside the EuroKeep container
5. Configure accounts, categories and budgets
6. Start tracking your finances

For detailed instructions, see the deployment and user management sections.

---

## Core Features

### Account Management

Create and manage your financial accounts, including:

- Bank accounts
- Cash accounts
- Other balance sources
- IBAN information
- Multiple currencies

---

### Money Tracking

Record your financial activity through:

- Income
- Expenses
- Transfers between accounts
- Categories and comments
- Automatic category suggestions based on previous bookings

---

### Budget Management

Budgets allow you to define spending limits for categories and their subcategories.

EuroKeep automatically summarizes matching movements and provides an overview of:

- Current spending
- Remaining budget
- Exceeded limits
- Related transactions

---

### Privacy Mode

Your financial information should remain private.

Privacy Mode allows you to hide sensitive information such as:

- Account balances
- Money movements
- IBAN details

This makes it possible to safely use EuroKeep even when others can see your screen.

---

## Monitoring

EuroKeep includes an experimental Prometheus exporter for monitoring financial statistics.

> ⚠️ The exporter currently exposes sensitive information and should only be accessible to trusted systems.

---

## Documentation Structure

This documentation covers:

- Deployment using Docker Compose
- Container management
- User administration
- Account management
- Money tracking
- Transfers
- Budgets
- Monitoring
- Application usage

---

## The Philosophy Behind EuroKeep

Your financial data is personal.

EuroKeep follows one simple principle:

> **Your Money - Your Data**

No external service should decide where your financial information is stored.

By running EuroKeep yourself, you stay in control of your data, your infrastructure and your privacy.