# dMoney Newman 2026

## Project Summary

This project automates API tests for **dMoney**, a mobile financial service (MFS) API. The tests are a Postman collection that runs from the command line with **Newman**. After each run, an HTML report is created with **newman-reporter-htmlextra**.

The collection covers the main flows for three user roles:

| Role         | Covered APIs |
|--------------|--------------|
| **Admin**    | Login, get user list, create customer, update customer, search customer by ID, create agent, update agent |
| **Agent**    | Login, verify OTP, deposit money to a customer |
| **Customer** | Login, verify OTP, check balance, send money |

Requests pass data to each other through collection variables such as tokens, user IDs, emails and phone numbers. Test scripts check status codes and response bodies.

## Technologies

- [Postman](https://www.postman.com/) – to design the API collection and write test scripts
- [Node.js](https://nodejs.org/) – the runtime
- [Newman](https://www.npmjs.com/package/newman) `^6.2.2` – runs Postman collections from the command line
- [newman-reporter-htmlextra](https://www.npmjs.com/package/newman-reporter-htmlextra) `^1.23.1` – creates the HTML report
- JavaScript – Postman test scripts and the runner script (`report.js`)

## Project Structure

```
dmoney-newman-2026-practise/
├── collection/
│   └── dmoney-2026-postman-collection-part2   # Exported Postman collection (JSON)
├── Reports/                                   # HTML report is created here (git-ignored)
├── report.js                                  # Runs the collection with Newman
├── package.json
└── README.md
```

## Prerequisites

- [Node.js](https://nodejs.org/) (LTS version recommended) and npm
- [Git](https://git-scm.com/)
- The dMoney API server running locally at `http://localhost:5000`. This is the collection's `baseUrl` variable.

## How to Clone

```bash
git clone https://github.com/bappy2194/dmoney-newman-2026-practise.git
cd dmoney-newman-2026-practise
```

## How to Install

Install the project dependencies (Newman and the htmlextra reporter):

```bash
npm install
```

## How to Run

Run the full collection and create the HTML report:

```bash
npm test
```

This command runs `node report.js`. It runs the collection once and saves the report to:

```
Reports/report.html
```

Open `Reports/report.html` in a browser to see the results.

### Run with the Newman CLI (optional)

You can also run the collection straight from the Newman CLI:

```bash
npx newman run ./collection/dmoney-2026-postman-collection-part2 -r cli,htmlextra --reporter-htmlextra-export ./Reports/report.html
```

## Configuration

The collection stores its settings in **collection variables**. Change them in Postman if needed:

| Variable     | Description |
|--------------|-------------|
| `baseUrl`    | API base URL (default: `http://localhost:5000`) |
| `partnerKey` | Partner key sent in the request headers |
| `admin_token`, `agent_token`, `customer_token` | Set automatically after each login |
| `customer_email`, `customer_phoneNumber`, `agent_email`, `agent_phoneNumber` | Generated randomly (with `lodash`) in pre-request scripts before a user is created |
| `customer_id`, `agent_id` | Saved from the response after a user is created |

> **Note:** The API server must be running before you start the tests, or every request will fail.

## Report

A sample HTML report from a Newman run:

<img width="722" alt="Newman htmlextra report" src="https://github.com/user-attachments/assets/08615905-f3d1-4faf-a44d-475eab5f05e9" />
