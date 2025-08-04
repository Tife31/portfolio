+++
date = '2025-01-11T20:05:58-05:00'
title = ' Reduce Your Credit Card Mental Load with Automation'
+++

## Introduction

Have you ever seen a charge on your credit card that you didn’t recognize? Perhaps it is a late payment fee?
Are you constantly checking your statements, worrying about missing payment deadlines?

In a world where we’re juggling so many responsibilities, it helps to lighten the mental load wherever possible.
Managing credit card payments can be stressful, even for people who know their due dates. I found myself repeatedly logging in to check balances, wondering if I’d paid already, and worrying about late fees or high credit utilization.
While my billing cycle is fixed (for example 25th to 24th, with a 21-day grace period from my bank), the real problem was not lack of knowledge, it was cognitive overload.

**So what is the Goal?** 

To build a lightweight automation tool to:
* Remove the mental burden of tracking credit card payments
* Ensure timely payments to avoid late fees
* Improve credit score health by nudging toward lower utilization

This project was designed as an MVP to validate whether automation could reduce mental effort without sacrificing control.



## Project overview

I built a program using the Plaid API. It connects to my bank, pulls my credit card activity, and analyzes the billing cycle to suggest the best time to pay my bill—before the due date, and even optimized to help improve my credit score when possible.

My program uses the plaidAPI to fetech financial data from my bank, processes credit card balances, limits and other data, to attain an amount to pay my towards credit card bill.  Using this amount, a reminder is sent to my calender with a due date to ensure I keep up with my payments. 


 ## Product Thinking in Action
User Insight: Most people don’t forget their due date—they just feel overwhelmed. This tool offloads routine checking to software.

Scope Control: I focused on automation—not live payments—to reduce security risk while proving the concept.

Privacy First: Built in Plaid’s sandbox mode to model user data without needing real access or credentials.

Behavioral Design: Calendar reminders were chosen because they integrate naturally with daily routines.


## How It Works

### Retrieve Financial Data
My project connects to Plaid API to pull in bank account and credit card details.
It extracts key information: available balance, total credit limit, and current spending.

### Get Credit Usage
In my project, the data is processed to determine the amount to be sent to my calender as owing is used. 

### Schedule Payment Reminders:
My project then integrates with Google Calendar API to create reminders for my credit card due date.
It ensures that all credit cards in  my account, has its due date as well as amount owed calculated and tracked.  This information is sent to my calender in advance. 

## Disclaimer
This project works well the sandbox environment. Gaining actuall access to my account would have been jumping through some major authentication hoops. I could not justify that over simply setting reminders by myself on my phone since my due date is every 21 days. The security from the Plaid company is strong, which is what we want!


## From a security perspective.
1. Both APIs integrated into my project (Plaid API and Google calender API )handle sensitive user data. These APIs implement strict security controls to prevent unauthorized access. Both APIs use: 

2. Secure Authentication with OAuth 2.0 and encryption
    OAuth 2.0 ensures you never receive user credentials (e.g., bank passwords). Instead, you get tokens that grant permission-based access. Plaid Api requires you to get a temporary public token that will be exchanged for a permanent token to use to retrieve your bank data.

3. Limit permissions → Request only necessary API scopes to reduce attack surface. 
When you create a link_token (which initializes Plaid Link), you specify only the necessary products (e.g., transactions, auth, identity, etc.). This ensures my app does not gain excessive access.
and follows the Least Privilege Principle.

4. Use Plaid’s Webhooks Securely
Plaid suggests using webhooks to be notified when transactions are ready instead of polling repeatedly. Webhooks provide event-driven notifications, reducing the need for polling (which could expose API keys more often).

## What I Learned
Users need simple, integrated nudges, not dashboards.

Even fixed billing cycles feel unpredictable when mental load is high.

Secure APIs can be leveraged safely without building full-scale apps.

## Future Improvements
The next step is to initiate a balance transfer if sufficent funds are in my debit card, send a notification then that this amount had been paid instead of creating a todo in my calender.